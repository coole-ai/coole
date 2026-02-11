# Coole CLI

The command-line tool for deploying and managing apps on the [Coole](https://coole.ai) platform.

## Install

```bash
curl -fsSL https://get.coole.ai | sh
```

This works on Linux and macOS (both Intel and Apple Silicon).

To install a specific version:

```bash
curl -fsSL https://get.coole.ai | sh -s -- --version 0.3.0
```

## Update

```bash
coole update
```

## Quick start

```bash
# Log in to your account
coole login

# Go to your project directory and initialize it
cd my-app
coole init

# Deploy
coole deploy
```

## Commands

| Command | What it does |
|---------|-------------|
| `coole login` | Log in to your Coole account |
| `coole init` | Set up a new project in the current directory |
| `coole deploy` | Deploy your app |
| `coole logs` | Stream your app's logs |
| `coole status` | Check your app and deployment status |
| `coole env set KEY=VALUE` | Set an environment variable |
| `coole db` | Manage databases |
| `coole scale` | View or change scaling settings |
| `coole rollback` | Roll back to a previous deployment |
| `coole open` | Open your app in the browser |

Run `coole --help` to see all available commands.

## Uninstall

```bash
sudo rm /usr/local/bin/coole
```

## License

Proprietary. Copyright Coole AI.
