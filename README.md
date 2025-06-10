# GNU Radio ASK Text Transmission

This project demonstrates a complete Amplitude Shift Keying (ASK) communication system implemented in GNU Radio. It simulates sending a short text message using ASK modulation, transmitting it as a WAV audio signal, and then demodulating it back into readable text.

## Project Overview

The system is split into two primary flows:

1. **Transmitter Flowgraph**
2. **Receiver Flowgraph**

Both are implemented using GNU Radio Companion (GRC) and linked via a WAV file.

---

## Transmitter Flow

The transmitter converts a text message into an ASK modulated signal.

### Steps:
1. **Vector Source**: Contains ASCII values representing the text message (e.g., "HELLO").
2. **Unpack K Bits**: Splits each byte into individual bits.
3. **Char To Float**: Converts bits into float values.
4. **Throttle**: Controls the bit rate.
5. **Float To Complex**: Converts float to complex for modulation.
6. **Signal Source**: Generates a sine wave carrier at 15 kHz.
7. **Multiply**: Performs ASK modulation by multiplying the carrier with the signal.
8. **Complex To Float**: Converts back to float format.
9. **WAV File Sink**: Saves the modulated audio as a `.wav` file.
10. **QT GUI Time Sink**: Visualizes the modulated waveform.

---

## Receiver Flow

The receiver demodulates the ASK signal from the WAV file and reconstructs the original text.

### Steps:
1. **WAV File Source**: Reads the modulated audio signal.
2. **Multiply**: Removes negative values by squaring the signal.
3. **Low Pass Filter**: Filters out the high-frequency carrier.
4. **Threshold**: Converts the filtered signal into digital bits (0 or 1).
5. **Float To Char**: Converts float values to char.
6. **Pack K Bits**: Groups bits into bytes.
7. **File Sink**: Saves the decoded text to a `.txt` file.
8. **QT GUI Time Sink**: Displays the demodulated waveform and bit stream.

---

> Note: The `.wav` and `.txt` files are generated during execution.

---

## How to Run

1. Open the `transmitter.grc` in GNU Radio Companion and run it.
   - This will generate a `data.wav` file.
2. Open the `receiver.grc` in GNU Radio Companion and run it.
   - This will decode the message and output to `data.txt`.

---

## Modulation Parameters

| Parameter     | Value        |
|---------------|--------------|
| Carrier Freq  | 15 kHz       |
| Sample Rate   | 30 kHz       |
| Bit Rate      | 4 kbps       |
| Modulation    | ASK (On-Off) |

---

## Example Message

The input text in the transmitter is:
HELLO

The same text should appear in the `data.txt` output file after successful demodulation.
