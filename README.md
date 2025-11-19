# JupyterLab Extension for Stata Syntax Highlighting

[![Github Actions Status](https://github.com/lutherbu/jupyterlab_stata_highlight3/workflows/Build/badge.svg)](https://github.com/lutherbu/jupyterlab_stata_highlight3/actions/workflows/build.yml)

Stata syntax highlighting for JupyterLab 4+.

## Forking and Customization

This is a customized fork of the original repository. To use your own fork:

1. **Fork the repository on GitHub**: Go to the [original repository](https://github.com/lutherbu/jupyterlab_stata_highlight3) and click "Fork" to create your own copy.

2. **Clone your fork**: Clone your forked repository to your local machine.

3. **Make your customizations**: Edit the code, styling, or configuration as needed.

4. **Push your changes**: Push your customizations to your GitHub fork.

## Requirements

- JupyterLab >= 4.0.0
- Node.js (required for building the extension during installation)
- Python >= 3.8

## Install

### Install from GitHub (Recommended for Customized Version)

To install this customized version directly from GitHub, execute:

```bash
pip install git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
```

Or for a specific branch/tag:

```bash
pip install git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git@BRANCH_NAME
```

**Note:** 
- The package will automatically build the JupyterLab extension during installation. Make sure you have Node.js installed (the build process requires it).
- After installation, you may need to rebuild JupyterLab: `jupyter lab build`

### Install from PyPI (Original Version)

To install the original extension from PyPI, execute:

```bash
pip install jupyterlab_stata_highlight3
```

### Install in Conda Environment

To install in a conda environment:

```bash
conda activate your_environment_name
pip install git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
```

Or using conda with pip:

```bash
conda install -c conda-forge pip
pip install git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
```

### Install on Remote Server

When installing on a remote server, you need Node.js installed for the build process. Here are the steps:

**Option 1: Install Node.js via Conda (Recommended)**

```bash
conda activate your_environment_name
conda install -c conda-forge nodejs
pip install git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
jupyter lab build
```

Note: `npm` is included with `nodejs` in conda-forge, so you only need to install `nodejs`.

**Option 2: Install Node.js via System Package Manager**

For Ubuntu/Debian:
```bash
sudo apt-get update
sudo apt-get install -y nodejs npm
```

For CentOS/RHEL:
```bash
sudo yum install -y nodejs npm
```

Then install the package:
```bash
pip install git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
jupyter lab build
```

**Option 3: Use Node Version Manager (nvm)**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm use --lts
pip install git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
jupyter lab build
```

**Troubleshooting:**

First, check if Node.js is installed:
```bash
node --version
npm --version
```

If these commands fail, Node.js is not installed. Use one of the options above to install it.

If you get errors during installation, ensure:
1. Node.js is installed: `node --version` and `npm --version` should work
2. JupyterLab is installed: `jupyter lab --version`
3. Build tools are available (usually included with Node.js)
4. You have write permissions in the installation directory

If the build still fails, try installing with verbose output to see the full error:
```bash
pip install --verbose git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
```

**Common Errors:**

1. **"Installing build dependencies: finished with status 'error'"**
   - This usually means Node.js is missing. Install Node.js first, then retry the pip install command.

2. **"failed to build pyzmq" or "C99 mode" errors**
   - This happens when pyzmq (a JupyterLab dependency) can't be built from source due to an old C compiler. The solution is to install pyzmq and JupyterLab via conda (which provides pre-built binaries), install build dependencies, then use `--no-build-isolation`:
   ```bash
   conda activate your_environment_name
   conda install -c conda-forge pyzmq jupyterlab nodejs
   pip install hatchling hatch-jupyter-builder hatch-nodejs-version
   pip install --no-build-isolation git+https://github.com/anguslewis/jupyterlab_stata_highlight3.git
   jupyter lab build
   ```
   - **Important**: 
     - Always install `pyzmq` and `jupyterlab` via conda on remote servers to avoid compilation issues
     - Install build dependencies (`hatchling`, `hatch-jupyter-builder`, `hatch-nodejs-version`) before using `--no-build-isolation`
     - Use `--no-build-isolation` flag with pip to tell it to use the conda-installed packages instead of trying to build them in an isolated environment
     - The pip install should only be used for your custom extension

## Uninstall

To remove the extension, execute:

```bash
pip uninstall jupyterlab_stata_highlight3
```

## Customize Keywords

![](preview.jpeg)

## Contributing

### Development install

Note: You will need NodeJS to build the extension package.

The `jlpm` command is JupyterLab's pinned version of
[yarn](https://yarnpkg.com/) that is installed with JupyterLab. You may use
`yarn` or `npm` in lieu of `jlpm` below.

```bash
# Clone the repo to your local environment
# Change directory to the jupyterlab_stata_highlight3 directory
# Install package in development mode
pip install -e "."
# Link your development version of the extension with JupyterLab
jupyter labextension develop . --overwrite
# Rebuild extension Typescript source after making changes
jlpm build
```

You can watch the source directory and run JupyterLab at the same time in different terminals to watch for changes in the extension's source and automatically rebuild the extension.

```bash
# Watch the source directory in one terminal, automatically rebuilding when needed
jlpm watch
# Run JupyterLab in another terminal
jupyter lab
```

With the watch command running, every saved change will immediately be built locally and available in your running JupyterLab. Refresh JupyterLab to load the change in your browser (you may need to wait several seconds for the extension to be rebuilt).

By default, the `jlpm build` command generates the source maps for this extension to make it easier to debug using the browser dev tools. To also generate source maps for the JupyterLab core extensions, you can run the following command:

```bash
jupyter lab build --minimize=False
```

### Development uninstall

```bash
pip uninstall jupyterlab_stata_highlight3
```

In development mode, you will also need to remove the symlink created by `jupyter labextension develop`
command. To find its location, you can run `jupyter labextension list` to figure out where the `labextensions`
folder is located. Then you can remove the symlink named `jupyterlab-stata-highlight3` within that folder.

### Packaging the extension

See [RELEASE](RELEASE.md)

## Credits and Licenses

- [jupyterlab-stata-highlight](https://github.com/kylebarron/jupyterlab-stata-highlight/): making all these possible by [kylebarron](https://github.com/kylebarron)
- [jupyterlab_stata_highlight2](https://github.com/hugetim/jupyterlab_stata_highlight2): prebuilt package on PyPI by [hugetim](https://github.com/hugetim)
- [codemirror-legacy-stata](https://github.com/ticoneva/codemirror-legacy-stata): hack by [ticoneva](https://github.com/ticoneva) based on [@codemirror/legacy-modes](https://github.com/codemirror/legacy-modes)
- [codemirror-extension](https://github.com/lutherbu/extension-examples/tree/main/codemirror-extension): extension examples for JupyterLab 4+
- [extension-template](https://github.com/jupyterlab/extension-template): a copier template for extension on JupyterLab 4+
- ChatGPT: for TypeScript ... :sweat_smile:

Please follow licenses specified above (if any)
