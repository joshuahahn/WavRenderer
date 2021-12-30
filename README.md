
# Wave File Rendering Tool

This project is a tool for rendering linear PCM audio data WAVE files. Supports functionality for various audio waves (sin, square, and saw) and audio modulation (pan, gain, ADSR envelope, and mixing). 

---

## Tone Rendering

The render_tone program creates a single continuous tone with user-specified parameters. The program is invoked using ```./render_tone waveform frequency amplitude numsamples wavfileout```:

**Parameters**

- *waveform*: Specifies the shape of the wave. 0 for sine, 1 for square, and 2 for saw wave. 
- *frequency*: Specifies the frequency of the tone (Hz). Taken in as a floating-point value.
- *amplitude*: Specifies the relative amplitude of the tone. Taken in as a floating point value from 0.0 (no sound) to 1.0 (maximum volume)
- *numsamples*: Specifies the number of stereo samples. The sampling frequency is fixed at 44.1 kHz (44,100 samples / second).
- *wavfileout*: Specifies the name of the rendered WAVE file. 