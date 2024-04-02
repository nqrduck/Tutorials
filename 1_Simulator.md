# 1. NQRduck Simulator Tutorial 🦆
## Introduction
This Tutorial gives a short overview of how to use the NQRduck Simulator. The NQRduck Simulator is a module of the NQRduck program that allows you to simulate NQR signals and spectra.

## Requirements
* All requirements from the [NQRduck Setup Tutorial](0_NQRduck_Setup.md)

## Steps (Linux)
1. Switch to the Spectrometer module in the NQRduck program.

2. You can now see two different sections in the Spectrometer module:
    - The left side are the spectrometer settings. These are values that don't  change during a Pulse Sequence.
    - The right side is the Pulse Programmer. Here you can create sequences of pulses that are executed during the simulation.

3. Create a simple Free Induction Decay (FID) sequence in the pulse programmer on the right side:
    - A sequence is made up of different events that are executed subsequently. Different events are rows in the pulse programmer table. 
    - For every event you can specify a certain length and a name. 
    - Every event now has Pulse Parameters associated with it. For the Simulator, these are the TX and the RX Pulse Parameters.

<img src="Figures/1_pulseprogrammer.png" width=50%>

    The picture shows an exemplary FID sequence.
    - a.) The different events.
        - Pulse is our TX Pulse that excites the sample.
        - Blank is a waiting time between the TX Pulse and the RX Readout in order to await coil ringing.
        - RX is the ADC Readout that measures the signal.
        - TR is the repetition time between the different averages. 
    - b.) The Pulse Parameters for the selected event.
    - c.) The Pulse Parameters for the TX Pulse.
    - d.) The Pulse Parameters for the ADC Readout.
    - e.) The duration of the different events

4. You can now adjust the settings  of the Simulator on the right side. Different settings are for example the number of simulation points or the noise level.






<!-- TODO:
Screenshot of the pulse programmer with a simple FID sequence
-->