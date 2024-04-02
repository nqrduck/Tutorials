# 0. NQRduck Setup Tutorial 🦆
## Introduction
This Tutorial gives a short overview of how to setup the NQRduck program. The NQRduck program is a collection of different modules that can be installed separately. The core program is the main entry point and provides a user interface to access the different modules. 

## Requirements

- Python 3.10+
- pip
- virtualenv
- About 600MB of free storage space


## Steps (Linux)
1. Install the specified requirements.
2. Create a virtual environment and activate it:
    ```bash
    python -m venv venv
    . venv/bin/activate
    ```
3. You can now install the NQRduck core program with a few base modules by running:
    
    ```bash
    pip install "nqrduck[base] @ git+https://github.com/nqrduck/nqrduck"
    ```
4. Run the program with `nqrduck`. This should open up a window with the NQRduck program.

5. You can switch between different modules with the toolbar. The installed modules should be "Measurement" and "Spectrometer". You can also check all available modules by opening "Help" -> "About Modules".

6. If you don't like how the program looks, you can change the appearance in "Settings" -> "Preferences". Settings are saved and restored on the next start. Updating of the plot font size requires a restart of the program.

