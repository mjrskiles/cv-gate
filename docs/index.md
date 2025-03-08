# Shapeware 1U

## A Sound Byte Labs Eurorack Module

Shapeware 1U is a compact analog utility module for Eurorack synthesizers. It provides a simple wave shaper and gate processor with both manual and CV control.

## Design

Please see the [KiCAD schematic files](https://github.com/mjrskiles/cv-gate) on GitHub.

## Features

- Bipolar mono CV/audio input processing
- +5V to -5V mono output
- Waveshaping capabilities
    - Convert any input wave into a square wave
    - Pulse width 'squeeze' with pot
    - Output voltage matches peak amplitude of input
- Manual gate button outputs +5V
- Visual feedback via bipolar LED
- Compact 1U, 6HP Eurorack format compatible with Intellijel Tile system.

## How It Works

Shapeware processes input CV signals through an analog window comparator with peak detection.

The interface consists of:

Input
- CV/audio input
- Manual gate button
- Waveshaper pot

Output
- Bipolar LED
- CV/audio output

The circuit is designed so that the output idles at 0V. If you press the gate button, the output with go to +5V. The gate button overrides the CV input. As long as the button is not pressed, the output follows the CV input. The basic idea is that the module will take any input on the CV input and convert it into a square wave with roughly the same loudness/amplitude as the original input.

The waveshaper pot allows you to 'squeeze' the pulse width of the output square wave. Internally, the circuit is a comparator with a peak detector. The waveshaper pot sets the positive and negative thresholds. The comparator compares the input voltage to the positive and negative thresholds. The output of the comparator is a 3-state wave. If the input is above the positive threshold, the output is 1. If the input is below the negative threshold, the output is -1. If the input is between the thresholds, the output is 0. The voltage on the output is matched to the peak amplitude of the input. The LED is driven by the output of the comparator circuit and switches between red and green based on the sign of the output.

The CV input is immediately buffered and distributed to the circuit components. The peak detector circuit works by passing the buffered input to positive and negative rectifiers. The rectifiers are configured to 'hold' the peak voltage of the input. The detected peak rolls off over time, allowing lower peaks to be detected. The outputs of the rectifiers are mixed together. The mixed output is then passed to both the bipolar LED and the analog switch. The waveshaper channel is open any time the button is not pressed and the CV input is outside of the 0V threshold. 

## Documentation

Please refer to the [schematic (PDF)](cv-gate.pdf).
