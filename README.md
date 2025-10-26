# DJ System using OSC Controller and Pure Data

## Team Members
- Sebastian Castro
- Rafael Hermida

## Project Description

This project is a complete DJ system that uses **OSC Controller** (Open Sound Control) mobile app to control a music creation environment built in **Pure Data**. The system allows real-time music performance and creation through an intuitive mobile interface.

## Demo Video
[Link to YouTube video - max 5 minutes]

## Features

### Sound Generators
1. **Drum Machine** (3 instruments)
   - Kick Drum (button1)
   - Hi-Hat (button3)
   - Snare Drum (button2)

2. **Piano/Keyboard** (24 notes)
   - 2 octaves (C4 to B5)
   - Controlled by gridButtons 1-24
   - Each button plays a different musical note

3. **Synthesizers** (3 different synths)
   - Synth 1: Oscillator controlled by slider2 and toggle1
   - Synth 2: Bass synth with low-pass filter (slider3 + toggle2)
   - Synth 3: Phasor synth (slider4 + toggle3)

### Performance Tools

#### Drum Sequencer
- Uses gridToggles 1-24 (8 steps × 3 instruments)
- Automatic playback with adjustable tempo
- Program rhythmic patterns by activating/deactivating toggles
- **Layout:**
  - gridToggles 1-8: Kick drum pattern
  - gridToggles 9-16: Snare drum pattern
  - gridToggles 17-24: Hi-hat pattern

#### 2D Effects Controller (slider2D)
- **X-axis (slider2Dx)**: Low-pass filter frequency (200Hz - 10200Hz)
- **Y-axis (slider2Dy)**: Delay effect amount (0 - 0.8)
- Affects all audio sources in real-time

#### Master Volume
- **slider1**: Controls the overall output volume

## Technical Implementation

### Architecture
The system is divided into modular subpatches:
- `pd drums`: Contains kick, hat, and snare drum synthesizers
- `pd synth1, pd synth2, pd synth3`: Three different synthesizers
- `pd piano`: 24-note keyboard implementation
- `pd sequencer`: 8-step drum sequencer
- `pd effects`: 2D effects processor with filter and delay
- `pd master`: Main audio mixer and output

### OSC Communication
- The mobile app sends OSC messages via UDP on port 2000
- Pure Data receives and routes these messages to different parameters
- All widgets from the OSC Controller app are used:
  - Regular buttons (button1-3)
  - Grid buttons (gridButton1-24)
  - Grid toggles (gridToggle1-24)
  - Sliders (slider1-4)
  - 2D slider (slider2Dx, slider2Dy)

### Audio Processing
- Each drum sound is synthesized from scratch using oscillators, noise generators, and envelopes
- Piano uses MIDI note numbers converted to frequencies
- Effects chain includes delay and filtering
- All sounds are mixed in the master with individual volume control

## Design Decisions

### Why This Approach?

1. **Modular Design**: Each component (drums, piano, synths, effects) is in its own subpatch. This makes the code:
   - Easier to understand and maintain
   - Reusable for future projects
   - Simple to debug when issues arise

2. **Complete Synthesis**: All sounds are generated from basic building blocks (oscillators, noise, envelopes) rather than using samples. This:
   - Keeps the project lightweight (no external files needed)
   - Demonstrates fundamental synthesis techniques
   - Allows unlimited parameter tweaking

3. **Grid Layout for Sequencer**: Using the 24 grid toggles as a 3×8 matrix (3 instruments, 8 steps) provides:
   - Visual representation of the rhythm pattern
   - Easy pattern editing in real-time
   - Intuitive workflow similar to professional drum machines

4. **2D Slider for Effects**: Mapping the 2D slider to filter and delay allows:
   - Expressive performance control
   - Smooth transitions between effect settings
   - Efficient use of limited interface space

5. **Automatic Sequencer Start**: The sequencer starts automatically with `loadbang` because:
   - It creates an immediate musical result
   - Users can focus on programming patterns rather than starting/stopping playback
   - Better for live performance scenarios

## How to Use

1. **Setup:**
   - Install Pure Data on your computer
   - Install OSC Controller app on your mobile device
   - Connect both devices to the same WiFi network
   - Open the `.pd` file in Pure Data
   - Configure OSC Controller to send to your computer's IP on port 2000

2. **Making Music:**
   - Use slider1 to adjust master volume
   - Press buttons 1-3 to play drum sounds manually
   - Activate grid toggles 1-24 to program a drum sequence
   - Press grid buttons 1-24 to play piano notes
   - Move sliders 2-4 and activate toggles 1-3 to control synthesizers
   - Use the 2D slider to add filter and delay effects

3. **Performance Tips:**
   - Start by programming a simple drum pattern
   - Add melodic elements with the piano
   - Use synthesizers for bass and lead sounds
   - Apply effects gradually for dynamic changes

## Requirements

- Pure Data (Pd vanilla)
- OSC Controller app (iOS/Android)
- WiFi network for OSC communication


*Note: This system was designed to provide a complete, performable electronic music environment using only Pure Data's built-in objects and OSC control.*
