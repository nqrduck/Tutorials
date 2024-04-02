# 2. LimeNQR Tutorial 🦆
## Introduction
The LimeNQR spectrometer can be used with the NQRduck program. 

## Requirements
- All requirements from the [NQRduck Setup Tutorial](0_NQRduck_Setup.md)

- On Debian-based systems, the following packages are required to build the software:

    ```
    sudo apt-get install g++ cmake liblimesuite-dev libhdf5-dev
    ```

    On Arch Linux, the following packages are required to build the software:

    ```
    sudo pacman -S gcc cmake limesuite hdf5
    ```
- Last but not least, install the [nqrduck-spectrometer-limenqr][https://github.com/nqrduck/nqrduck-spectrometer-limenqr] module:

    ```
    pip install "nqrduck-spectrometer-limenqr @ git+https://github.com/nqrduck/nqrduck-spectrometer-limenqr"
    ```

## Steps (Linux)
### Loopback Measurement
1. Check that you installed the nqrduck-spectrometer-limenqr module. You can click on the "Spectrometer" button in the menu bar and select "LimeNQR". Another way to check if the module is installed is to open "Help" -> "About Modules".

2. Connect the USB cable of the LimeNQR spectrometer to your computer. 

3. Load the FID pulse sequence int the Pulse Programmer. You can use the same sequence as in the NQRduck Simulator Tutorial.

4. Adjust the RX event to occur at the same time as the ADC Readout. We will perform a "Loopback" measurement, where we observe the output signal of of the LImeNQR spectrometer.

5. Connect the TX and RX ports of the LimeNQR spectrometer with a SMA cable and a 20dB attenuator.

6. Go to the measurement module, enter a measurement frequency and a number of averages  (100) and  click start  measurement. You should be able to see the output signal of the LimeNQR spectrometer.

7. You can now change the pulse shape of the TX pulse and observe the signal change in the measurement module after running the measurement again.

### NQR Measurement
1. Load the NQR pulse sequence in the Pulse Programmer. You can use the same sequence as in the NQRduck Simulator Tutorial. Make sure not to use the Loopback measurement.

2. Connect the LimeNQR spectrometer to your spectroscopy setup. 

