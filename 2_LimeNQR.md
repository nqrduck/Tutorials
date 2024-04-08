# 2. LimeNQR Tutorial 🦆
## Introduction
The LimeNQR spectrometer can be used with the NQRduck program for magnetic resonance experiments.

This tutorial will show you how to use the LimeNQR spectrometer with the NQRduck program. We will perform a loopback measurement, a TX check, and a NQR measurement on a sample. 

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
- Last but not least, install the [nqrduck-spectrometer-limenqr](https://github.com/nqrduck/nqrduck-spectrometer-limenqr) module:

    ```
    pip install "nqrduck-spectrometer-limenqr @ git+https://github.com/nqrduck/nqrduck-spectrometer-limenqr"
    ```

### ⚠️ Safety Tips ⚠️
- Don't leave the low noise amplifier (LNA) unconnected on the in- and output. This could damage the LNA.

- Don't output a pulse without a load connected to the TX port. This could damage the RFPA.

- Don't pulse at any other where the probe coil is not tuned and matched. This could damage the setup.

- Don't forget the TR event in your pulse sequence. This could damage the setup.

- Make sure the Pre Amplifier is cooled. It will burn out otherwise.

## Steps (Linux)
### Loopback Measurement
This is a simple test to check if the LimeNQR spectrometer is working correctly. We measure the output signal of the LimeNQR spectrometer with the receive path of the LimeNQR spectrometer.

| <img src="Figures/2_loopback_schematic.png" width=40%> |
|:--:| 
| Figure: Schematic for the loopback measurement.|

1. Check that you installed the nqrduck-spectrometer-limenqr module. You can click on the `Spectrometer` button in the menu bar and select `LimeNQR`. Another way to check if the module is installed is to open `Help" -> About Modules`.

2. Connect the USB cable of the LimeNQR spectrometer to your computer. 

3. Load the FID pulse sequence into the `Pulse Programmer`. You can use the same sequence as in the [NQRduck Simulator Tutorial](1_Simulator.md).

4. Adjust the RX event to occur at the same time as the TX Pulse. We will perform a "Loopback" measurement, where we observe the output signal of of the LImeNQR spectrometer.

5. Connect the TX and RX ports of the LimeNQR spectrometer with a SMA cable and a 20dB attenuator.

| <img src="Figures/2_Loopback.png" width=100%> |
|:--:| 
| Figure: Picture of the Spectrometer setup for the loopback measurement. The silver part is the attenuator. The RX and TX path are connected.|

6. Go to the measurement module, enter a `Target Frequency` and a number of `Averages` (100) and  click `Start Measurement`. You should be able to see the output signal of the LimeNQR spectrometer.

7. You can now change the pulse shape of the TX pulse and observe the signal change in the measurement module after running the measurement again.

8. You can also observe the signal in frequency space by clicking on the `FFT` button in the measurement module.

### TX Check
Here we will perform a test if the Radio Frequency Power Amplifier (RFPA) is working correctly. We will measure the output signal of the RFPA by pulsing into a 50 Ohm dummy load and observing the signal with an oscilloscope. 

| <img src="Figures/2_dummy_load.jpg" width=40%> |
|:--:|
| Figure: Picture of the dummy load.|

1. Load the FID pulse sequence in the `Pulse Programmer`. You can use the same sequence as in the [NQRduck Simulator Tutorial](1_Simulator.md). Make sure to add an TR event to the sequence. The last event in your pulse sequence will always be interpreted as the TR time. If you don't add a TR event, the duty cycle of the TX pulse might be too high and you could damage things. 

2. We use a pre-amplifier to amplify the signal of the LimeNQR spectrometer. Connect the TX port of the LimeNQR spectrometer to the Pre Amplifier. Connect the Pre Amplifier to the 12V Power Supply. Make sure the Pre Amplifier is cooled because it will burn out otherwise. The RX port of the LimeNQR spectrometer can stay unconnected. 

3. Connect the gate of the LimeNQR to the oscilloscope on Channel 1. Trigger on a rising flank on Channel 1. Use a timescale that makes sense for your pulse sequence.

4. Observe the pulse on Channel 2 of the oscilloscope, by connecting it to the Directional Coupler (FWD). Use AC coupling. 

5. Go to the spectrometer `Settings` and set the `TX gain` to `10`.

6. Set the `Target Frequency` to 83.56 MHz and the number of `Averages` to 100. Click `Start Measurement`. You should see the pulse on the oscilloscope. The blue trace is the Gate Signal and the yellow trace is the TX pulse.

### NQR Measurement
We will now perform a NQR measurement on a sample. We will use the BiPh3 sample for this tutorial.

| <img src="Figures/2_BiPh3.jpg" width=25%> |
|:--:|
| Figure: Picture of the BiPh3 sample. |

1. Load the NQR pulse sequence in the `Pulse Programmer` by clicking the `Load pulse sequence`. You can use the same sequence as in the NQRduck Simulator Tutorial. Make sure not to use the Loopback measurement where the RX event occurs at the same time as the TX pulse.

2. Put the sample into the probe coil and tune and match it at 83.56 MHz using a Network Analyzer. You can find detailed instructions at [Tuning and Matching](###Tuning-and-Matching).

3. Connections ⚡: 

The experiment now has to be set up as follows:

| <img src="Figures/2_measurement_schematic.png" width=100%> |
|:--:|
| Figure: Schematic of the NQR measurement setup. The power connections are not depicted. |

- [ ] Connect the 12V Power Supply to the LimeNQR spectrometer and the USB cable to your computer.
- [ ] Connect the Gate of the LimeNQR spectrometer to the Gate of the Power Amplifier.
- [ ] Connect the TX port of the LimeNQR spectrometer to the Pre Amplifier.
- [ ] Connect the Pre Amplifier to the 12V Power Supply. Maker sure the Pre Amplifier is cooled because it will burn out otherwise.
- [ ] Connect the RX port of the LimeNQR spectrometer to Low Noise Amplifier (LNA).
- [ ] Connect the LNA to the 5V Power Supply.

| <img src="Figures/2_fullmeas_pic.jpg" width=100%> |
|:--:|
| Figure: Picture of the NQR measurement setup. |

4. Go to the measurement module, enter a `Target Frequency` of 83.56 MHz and a number of `Averages` (1000) and  click `Start Measurement`. You should be able to see the NQR signal of the BiPh3 sample. Don't pulse at any other frequency than 83.56 MHz, because you could damage the setup.

5. You should see a peak from your signal at the Intermediate Frequency (IF) that was set in the `Spectrometer` tab. The default value is 5MHz. 

-  What else do you see in the spectrum? Can you identify the different peaks?

6. To make sure that the signal is coming from the sample, you can remove the sample from the probe coil and see if the signal disappears.
⚠️CAREFUL!⚠️ You need to tune and match the probe coil again after removing the sample.

7. You can now also try a Spin Echo if the FID worked. If you have very long sequences, make sure to increase the `Acquisition Time` in the `Spectrometer` settings.










.




