# Setting Up Julia and Interactive Notebooks on Ubuntu

This guide provides step-by-step instructions to install Julia, configure the environment, set up IJulia for interactive notebooks, install Jupyter Notebook, and prepare VS Code for Julia development on Ubuntu.

## Prerequisites

Before you begin, ensure the following are installed:

- `wget` and `tar` (typically preinstalled on Ubuntu) for downloading and extracting Julia.
- `python3` and `python3-venv` for creating a virtual environment.
- VS Code (optional, if you plan to use it for Julia development).

To install `python3-venv`, run:

```bash
sudo apt update
sudo apt install python3-venv
```

## 1. Installing Julia on Ubuntu

Download and extract Julia version 1.11.1:

```bash
wget https://julialang-s3.julialang.org/bin/linux/x64/1.11/julia-1.11.1-linux-x86_64.tar.gz
tar zxvf julia-1.11.1-linux-x86_64.tar.gz
```

This extracts Julia into a directory named `julia-1.11.1`. No traditional installation is required; you’ll run Julia from this directory.

**Note**: Visit the [Julia downloads page](https://julialang.org/downloads/) to check for the latest version and update the URL if necessary.

## 2. Adding Julia to the PATH

To use Julia from any terminal, add its `bin` directory to your `PATH`:

1. Navigate to the Julia `bin` directory and get its full path. For example, if extracted in your home directory:

```bash
cd ~/julia-1.11.1/bin
pwd
```

Copy the output (e.g., `/home/user/julia-1.11.1/bin`).

2. Open your `~/.bashrc` file in a text editor:

```bash
nano ~/.bashrc
```

3. Add the following line at the end, replacing `/path/to/julia-1.11.1/bin` with the path from step 1:

```bash
export PATH="$PATH:/path/to/julia-1.11.1/bin"
```

4. Save the file (Ctrl+O, Enter, Ctrl+X in nano) and apply the changes:

```bash
source ~/.bashrc
```

**Verification**: Test Julia by running:

```bash
julia --version
```

You should see the version number (e.g., `julia version 1.11.1`).

## 3. Installing IJulia for Interactive Notebooks

Install the IJulia package to enable Julia in Jupyter notebooks:

1. Open a terminal and start the Julia REPL:

```bash
julia
```

2. In the Julia REPL, run:

```julia
import Pkg
Pkg.add("IJulia")
```

This installs IJulia, integrating Julia with Jupyter.

## 4. Setting Up Jupyter Notebook

Set up Jupyter Notebook in a virtual environment for a clean installation:

1. Create a virtual environment (you can choose any location, e.g., your home directory):

```bash
python3 -m venv ~/myenv
```

2. Activate the virtual environment:

```bash
source ~/myenv/bin/activate
```

3. Install Jupyter:

```bash
pip install jupyter
```

4. Launch Jupyter Notebook:

```bash
jupyter notebook
```

Your browser will open the Jupyter interface, and the Julia kernel should be available if IJulia was installed correctly.

**Verification**: List available kernels:

```bash
jupyter kernelspec list
```

Look for a Julia entry (e.g., `julia-1.11`).

**Note**: To exit the virtual environment later, run `deactivate`.

## 5. Setting Up VS Code for Julia

Configure VS Code for Julia development:

1. Open VS Code.
2. Access the Extensions view (Ctrl+Shift+X or click the Extensions icon).
3. Search for "Julia".
4. Click "Install" on the official Julia extension.

This adds features like syntax highlighting and debugging for Julia in VS Code.

## Using Julia

- **Scripts**: Save Julia scripts with the `.jl` extension (e.g., `myscript.jl`).
- **Notebooks**: Create Jupyter notebooks with the `.ipynb` extension. Select the Julia kernel in Jupyter to run Julia code.

## Final Notes

You’re now ready to use Julia for scripting and interactive notebooks! For more details, consult the [Julia documentation](https://docs.julialang.org/) or [Jupyter documentation](https://jupyter.org/documentation).