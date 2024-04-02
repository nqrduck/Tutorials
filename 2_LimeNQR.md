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
- Last but not least, install the [nqrduck-spectrometer-limenqr](https://github.com/nqrduck/nqrduck-spectrometer-limenqr) module:

    ```
    pip install "nqrduck-spectrometer-limenqr @ git+https://github.com/nqrduck/nqrduck-spectrometer-limenqr"
    ```

## Steps (Linux)
### Loopback Measurement
This is a simple test to check if the LimeNQR spectrometer is working correctly. We measure the output signal of the LimeNQR spectrometer with the receive path of the LimeNQR spectrometer.

1. Check that you installed the nqrduck-spectrometer-limenqr module. You can click on the `Spectrometer` button in the menu bar and select `LimeNQR`. Another way to check if the module is installed is to open `Help" -> About Modules`.

2. Connect the USB cable of the LimeNQR spectrometer to your computer. 

3. Load the FID pulse sequence int the `Pulse Programmer`. You can use the same sequence as in the [NQRduck Simulator Tutorial](1_Simulator.md).

4. Adjust the RX event to occur at the same time as the ADC Readout. We will perform a "Loopback" measurement, where we observe the output signal of of the LImeNQR spectrometer.

5. Connect the TX and RX ports of the LimeNQR spectrometer with a SMA cable and a 20dB attenuator.

| <img src="Figures/2_Loopback.png" width=100%> |
|:--:| 
| Figure: Spectrometer setup for the loopback measurement. |

6. Go to the measurement module, enter a `Target Frequency` and a number of `Averages` (100) and  click `Sart Measurement`. You should be able to see the output signal of the LimeNQR spectrometer.

7. You can now change the pulse shape of the TX pulse and observe the signal change in the measurement module after running the measurement again.

### TX Check
Here we will perform a test if the Radio Frequency Power Amplifier (RFPA) is working correctly. We will measure the output signal of the RFPA by pulsing into a 50 Ohm dummy load and observing the signal with an oscilloscope. 

1. Load the FID pulse sequence in the `Pulse Programmer`. You can use the same sequence as in the [NQRduck Simulator Tutorial](1_Simulator.md). Make sure to add an TR event to the sequence. The last event in your pulse sequence will always be interpreted as the TR time. If you don't add a TR event, the duty cycle of the TX pulse might be too high and you could damage things. 

2. We use a pre-amplifier to amplify the signal of the LimeNQR spectrometer. Connect the TX port of the LimeNQR spectrometer to the Pre Amplifier. Connect the Pre Amplifier to the 12V Power Supply. Make sure the Pre Amplifier is cooled because it will burn out otherwise.

### NQR Measurement
We will now perform a NQR measurement on a sample. We will use the BiPh3 sample for this tutorial.

1. Load the NQR pulse sequence in the `Pulse Programmer` by clicking the `Load pulse sequence`. You can use the same sequence as in the NQRduck Simulator Tutorial. Make sure not to use the Loopback measurement where the RX event occurs at the same time as the TX pulse.

2. Put the sample into the probe coil and tune and match it at 83.56 MHz using a Network Analyzer. You can find detailed instructions at [Tuning and Matching](###Tuning-and-Matching).

3. Connections: 

- [ ] Connect the 12V Power Supply to the LimeNQR spectrometer and the USB cable to your computer.
- [ ] Connect the Gate of the LimeNQR spectrometer to the Gate of the Power Amplifier.
- [ ] Connect the TX port of the LimeNQR spectrometer to the Pre Amplifier.
- [ ] Connect the Pre Amplifier to the 12V Power Supply. Maker sure the Pre Amplifier is cooled because it will burn out otherwise.
- [ ] Connect the RX port of the LimeNQR spectrometer to Low Noise Amplifier (LNA).
- [ ] Connect the LNA to the 5V Power Supply.

4. Go to the measurement module, enter a `Target Frequency` of 83.56 MHz and a number of `Averages` (1000) and  click `Start Measurement`. You should be able to see the NQR signal of the BiPh3 sample. Don't pulse at any other frequency than 83.56 MHz, because you could damage the setup.

5. You can now also try a Spin Echo if the FID worked. If you have very long sequences, make sure to increase the `Acquisition Time` in the `Spectrometer` settings.

### Safety Tips
- Don't leave the low noise amplifier (LNA) unconnected on the in- and output. This could damage the LNA.

- Don't output a pulse without a load connected to the TX port. This could damage the RFPA.

- Don't pulse at any other where the probe coil is not tuned and matched. This could damage the setup.

- Don't forget the TR event in your pulse sequence. This could damage the setup.

- Make sure the Pre Amplifier is cooled. It will burn out otherwise.

### Tuning and Matching
_Tuning and Matching_ describes the process of adjusting the probe coil to the Larmor frequency of the sample.

#### Theory

At high frequencies the impedance of the coil has to be matched to the characteristic impedance of the cables and spectrometer of 50 $\Omega$. If we don't match the impedance, the signal will be reflected at the coil and we will lose signal strength.

| <img src="Figures/2_tuning_matching_circuit.png" width=100%> |
|:--:| 
|Figure: Example of a parallel resonator topology. The coaxial cable and output of the spectrometer are matched to a purely resistive impedance $Z_0$ of $50\Omega$. The Matching Network matches the impedance of the coil to $50\Omega$ to minimize reflections.|

The reflection coefficient $\Gamma$ describes what portion of the forwarded signal is reflected. It can be calculated from the impedance of the probe coil $Z_{coil}$ and the characteristic impedance of the cable $Z_0$.

$
    \Gamma = \frac{Z_{coil} - Z_0}{Z_{coil} + Z_0}
$

As can be seen, the reflection of the forward running signal is minimal when $Z_{coil}$ is equal to $Z_{0}$.

The reflection coefficient can can also be expressed in terms of the Return Loss $RL$ in dB:

$
    RL = -20 \cdot \log_{10}(|\Gamma|)
$

We therefore want to achieve a high Return Loss to minimize reflections.

#### Tuning and Matching in Practice

For Tuning and Matching the coil has two adjustable capacitors. One for tuning and one for matching of the probe coil:

| <img src="Figures/2_probe_coil.png" width=100%> |
|:--:|
| Figure: Picture of the probe coil with the steppers. The stepper/capacitor for tuning and matching are labelled.|

While the probe coil has stepper motors for automatic Tuning and Matching of the probe coil, we will use our hands to adjust the capacitors. Don't worry, the stepper motors can be moved by hand without damaging them.

The principle of tuning and matching is shown in the following figure:

| <img src="Figures/2_principle_tm.png" width=50%> |
|:--:|
| Figure:Depiction of a reflection measurement of our probe coil. On the x-axis you can see the frequency and on the y-axis the $RL$. In a simplified viewpoint, $C_t$ can be used to adjust the resonance frequency (Tuning) of the probe coil, and $C_m$ for the amount of reflection (Matching) occurring at resonance frequency. While tuning and matching influence each other in real applications, this representation can be helpful in understanding the functions of the capacitors for tuning and matching. |

We use a Vector Network Analyzer (VNA) to measure the $S_{11}$ value of our probe coil. The $S_{11}$ value is directly related to the Return Loss $RL$: In a simplified view only the sign is inverted.

Connect the SMA port of the probe coil to Port 1 of the VNA and start a $S_{11}$ measurement:

| <img src="Figures/2_VNA.jpg" width=75%> |
|:--:|
| Figure: Picture of the VNA performing a $S_{11}$ measurement. Port 1 of the VNA is directly connected to our probe coil. The VNA has a button `SPAN` that can be used to adjust the frequency range of the measurement. To scale the RL measurement you can click the `SCALE` button and select `Autoscale`.|

Now create a marker by clicking the `MKR` button and move it to 83.56 MHz, which is the Larmor Frequency of our BiPh3 sample. You can now adjust the capacitors of the probe coil to achieve a minimum $S_{11}$ value at 83.56 MHz (about -30dB). By narrowing the frequency range of the VNA you can increase the resolution of the measurement.

Make sure you perform the Tuning and matching with your sample in the probe coil. The sample influences the resonance frequency of the probe coil.


