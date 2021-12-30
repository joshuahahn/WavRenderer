
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

**Example Usage**

```
352800

W 0 1
E 0 1
P 0 -0.4

W 1 2
E 1 1
P 1 0.4

N 0 0 8820 63 0.8
N 0 0 8820 66 0.8
N 1 22050 30870 61 0.8
N 1 22050 30870 65 0.8
N 0 44100 52920 63 0.8
N 0 44100 52920 66 0.8
N 1 66150 74970 61 0.8
N 1 66150 74970 65 0.8
N 0 88200 97020 63 0.8
N 0 88200 97020 66 0.8
N 1 110250 119070 61 0.8
N 1 110250 119070 65 0.8
N 0 132300 141120 63 0.8
N 0 132300 141120 66 0.8
N 1 154350 163170 61 0.8
N 1 154350 163170 65 0.8

N 0 176400 194040 66 0.8
N 0 176400 194040 70 0.8
N 1 220500 238140 66 0.8
N 1 220500 238140 70 0.8
N 0 264600 282240 66 0.8
N 0 264600 282240 70 0.8
```

---

## Echo Rendering

The render_echo program modifies a WAVE file and adds echo based on specified parameters. Invoked using ```./render_echo wavfilein wavfileout delay amplitude```

**Parameters**

- *wavfilein*: Specifies the name of the input WAVE file.
- *wavfileout*: Specifies the name of the output WAVE file.
- *delay*: Specifies the delay time in sample numbers.
- *amplitude*: Specifies the volume of the echos as a floating point value from 0.0 (no echo) to 1.0 (max echo).

**Example Usage**

- Adding echo to a file named "example.wav" into a file named "echo.wav" with a delay of 22050 samples (or 0.5 seconds, calculated using 44100 * x seconds) and a echo factor of 0.5.
    - ```./render_echo example.wav echo.wav 22050 0.5```
- Adding echo to a file named "example2.wav" into a file named "echo2.wav" with a delay of 11025 samples (or 0.25 seconds, calculated using 44100 * x seconds) and a echo factor of 0.3.
    - ```./render_echo example2.wav echo2.wav 11025 0.3```

---

Project completed with Kevin Kim of Johns Hopkins University 