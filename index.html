#!/bin/sh
# Coole CLI installer
# Usage: curl -fsSL https://get.coole.ai | sh
#        curl -fsSL https://get.coole.ai | sh -s -- --version 0.3.0
set -eu

REPO="coole-ai/coole"
INSTALL_DIR="/usr/local/bin"
BINARY_NAME="coole"

main() {
    parse_args "$@"
    detect_platform
    get_version
    download_binary
    verify_checksum
    install_binary
    echo ""
    echo "Coole CLI ${VERSION} installed successfully!"
    echo "Run 'coole --help' to get started."
}

parse_args() {
    VERSION=""
    while [ $# -gt 0 ]; do
        case "$1" in
            --version)
                VERSION="$2"
                shift 2
                ;;
            --version=*)
                VERSION="${1#--version=}"
                shift
                ;;
            --help)
                echo "Usage: curl -fsSL https://get.coole.ai | sh -s -- [OPTIONS]"
                echo ""
                echo "Options:"
                echo "  --version VERSION  Install a specific version (e.g. 0.3.0)"
                echo "  --help             Show this help message"
                exit 0
                ;;
            *)
                echo "Unknown option: $1" >&2
                exit 1
                ;;
        esac
    done
}

detect_platform() {
    OS="$(uname -s)"
    ARCH="$(uname -m)"

    case "$OS" in
        Linux)  OS="linux" ;;
        Darwin) OS="darwin" ;;
        *)
            echo "Error: unsupported operating system: ${OS}" >&2
            exit 1
            ;;
    esac

    case "$ARCH" in
        x86_64|amd64)  ARCH="amd64" ;;
        aarch64|arm64) ARCH="arm64" ;;
        *)
            echo "Error: unsupported architecture: ${ARCH}" >&2
            exit 1
            ;;
    esac

    echo "Detected platform: ${OS}/${ARCH}"
}

get_version() {
    if [ -n "$VERSION" ]; then
        # Ensure version has v prefix for tag
        case "$VERSION" in
            v*) TAG="$VERSION" ;;
            *)  TAG="v${VERSION}" ;;
        esac
        echo "Installing version: ${TAG}"
        return
    fi

    echo "Fetching latest version..."
    TAG="$(curl -fsSL "https://api.github.com/repos/${REPO}/releases/latest" \
        | grep '"tag_name"' \
        | sed -E 's/.*"tag_name": *"([^"]+)".*/\1/')"

    if [ -z "$TAG" ]; then
        echo "Error: failed to determine latest version" >&2
        exit 1
    fi

    VERSION="${TAG#v}"
    echo "Latest version: ${TAG}"
}

download_binary() {
    BINARY_URL="https://github.com/${REPO}/releases/download/${TAG}/${BINARY_NAME}-${OS}-${ARCH}"
    CHECKSUMS_URL="https://github.com/${REPO}/releases/download/${TAG}/checksums.txt"
    TMP_DIR="$(mktemp -d)"
    TMP_BINARY="${TMP_DIR}/${BINARY_NAME}"
    TMP_CHECKSUMS="${TMP_DIR}/checksums.txt"

    echo "Downloading ${BINARY_NAME}-${OS}-${ARCH}..."
    if ! curl -fsSL -o "$TMP_BINARY" "$BINARY_URL"; then
        echo "Error: failed to download binary from ${BINARY_URL}" >&2
        rm -rf "$TMP_DIR"
        exit 1
    fi

    echo "Downloading checksums..."
    if ! curl -fsSL -o "$TMP_CHECKSUMS" "$CHECKSUMS_URL"; then
        echo "Warning: failed to download checksums, skipping verification" >&2
        TMP_CHECKSUMS=""
    fi
}

verify_checksum() {
    if [ -z "${TMP_CHECKSUMS:-}" ]; then
        return
    fi

    echo "Verifying checksum..."
    EXPECTED="$(grep "${BINARY_NAME}-${OS}-${ARCH}" "$TMP_CHECKSUMS" | awk '{print $1}')"

    if [ -z "$EXPECTED" ]; then
        echo "Warning: no checksum found for ${BINARY_NAME}-${OS}-${ARCH}, skipping verification" >&2
        return
    fi

    if command -v sha256sum >/dev/null 2>&1; then
        ACTUAL="$(sha256sum "$TMP_BINARY" | awk '{print $1}')"
    elif command -v shasum >/dev/null 2>&1; then
        ACTUAL="$(shasum -a 256 "$TMP_BINARY" | awk '{print $1}')"
    else
        echo "Warning: no sha256 tool found, skipping checksum verification" >&2
        return
    fi

    if [ "$EXPECTED" != "$ACTUAL" ]; then
        echo "Error: checksum mismatch" >&2
        echo "  expected: ${EXPECTED}" >&2
        echo "  actual:   ${ACTUAL}" >&2
        rm -rf "$TMP_DIR"
        exit 1
    fi

    echo "Checksum verified."
}

install_binary() {
    chmod +x "$TMP_BINARY"

    if [ -w "$INSTALL_DIR" ]; then
        mv "$TMP_BINARY" "${INSTALL_DIR}/${BINARY_NAME}"
    else
        echo "Installing to ${INSTALL_DIR} (requires sudo)..."
        sudo mv "$TMP_BINARY" "${INSTALL_DIR}/${BINARY_NAME}"
    fi

    rm -rf "$TMP_DIR"
}

main "$@"
