
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

**Example Usage**

- Rendering a 140.31 Hz sine wave at 0.5 volume:
    - ```./render_tone 0 140.31 0.5 44100 140sine_half.wav```
- Rendering a 140.31 Hz sawtooth wave at 1.0 volume:
    - ```./render_tone 2 140.31 1.0 44100 140saw_full.wav```
- Rendering a 120.00 Hz square wav at 0.01 volume:
    - ```./render_tone 1 120.00 0.01 44100 120square_quiet.wav```

---
## Song Rendering

The render_song program creates a song from a text file that specifies details about the song. The program is invoked using ```./render_song songinput waveoutput```

**Parametes**

- *songinput*: Specifies the details of the song to be produced.
    - The first line in the songinput text file specifies the number of samples. 
        - Since we have decided to use a fixed sampling frequency of 44.1 kHz, the length of the song is number of samples / 44100.
    - The lines that follow are a series of *directives*, formatted as follows:
    - **N instrument start end note gain**: Renders tone based on parameters.
        - *instrument*: Specifies the instrument of the note.
        - *start*: Specifies the first sample number. 
        - *end*: Specifies the last sample number.
        - *note*: Specifies the MIDI note number.
        - *gain*: Specifies the gain factor, ranging from 0.0 to 1.0.
    - **W instrument waveform**: Sets instrument waveform
        - *instrument*: Specifies instrument to be modified.
        - *waveform*: Specifies the wave form to be set on the instrument number.
    - **P instrument angle**: Sets instrument pan
        - *instrument* Specifies instrument to be modified.
        - *angle*: Specifies pan angle (in radians).
    - **E instrument enable**: Sets ADSR status
        - *instrument*: Specifies instrument to be modified.
        - *enable*: Specifies ADSR status (0 for off, 1 for on).
    - **G instrument gain**: Sets gain factor
        - *instrument*: Specifies instrument to be modified.
        - *gain*: Specifies gain factor (0.0 for none, 1.0 for maximum).