+++
title = "Hydra Workshop"
date = "2025-07-22T01:01:50+01:00"
author = "Sylvain Laurent"
authorTwitter = "magicking_" #do not include @
cover = ""
tags = ["hydra", "livecoding"]
keywords = ["livecoding", ""]
description = "Hydra Livecoding Workshop"
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

# Hydra Visual Coding Workshop

**Duration:** 2 hours + 1 hour bonus  
**Format:** 5 lessons (30min each) with 10min teaching + 15-20min workshop

---

## Lesson 1: Hydra 101 (10min + 20min)

### Teaching (10min)
- **Objective:** Get familiar with Hydra interface and basic workflow
- Navigate to [https://hydra.ojack.xyz](https://hydra.ojack.xyz)
- **Interface tour (2min):**
  - Play/Stop button
  - Clear button
  - Examples dropdown
  - Settings gear
- **Documentation overview:** Quick look at built-in help
- **Basic workflow demonstration:**
  ```javascript
  osc(40, 0.1, 1.2).out()
  ```
- Show simple texture → output chain

### Workshop 1 (20min)
**Goal:** Get your first visual output working
- Navigate to [https://hydra.ojack.xyz](https://hydra.ojack.xyz)
- Try these basic generators:
  - `osc().out()`
  - `noise().out()`
  - `solid(1,0,0).out()`
- Experiment with changing numbers
- Bookmark useful resources page (see cheatsheet)

---

## Lesson 2: Experimenting with Hydra (10min + 20min)

### Teaching (10min)
- **Core principle:** "You always get a result, no matter what numbers you use"
- **Math.PI exploration:**
  - `osc(40, 0.1, Math.PI).out()`
  - Show how Math.PI affects colors and scaling
- **Number ranges:** Demonstrate different parameter ranges
- **Happy accidents:** Show how random experimentation leads to discoveries

### Workshop 2 (20min)
**Goal:** Understand parameter experimentation
- Navigate to [https://hydra.ojack.xyz/functions](https://hydra.ojack.xyz/functions)
- Use this as reference while experimenting
- Try:
  - Different frequency values: `osc(10).out()` vs `osc(100).out()`
  - Color experiments with Math.PI
  - Scaling with various numbers

---

## Lesson 3: Mastering the Chain "." (10min + 20min)

### Teaching (10min)
- **The power of chaining:** Everything connects with "."
- **Write slowly and deliberately**
- **Basic chain structure:** `source().transform().output()`
- **Example progression:**
  ```javascript
  osc()           // just a source
  osc().rotate()  // add transformation
  osc().rotate(0.1).out() // complete chain
  ```
- Keep function reference page open

### Workshop 3 (20min)
**Goal:** Practice chaining functions confidently
- Navigate to blank canvas [https://hydra.ojack.xyz](https://hydra.ojack.xyz)
- Build chains step by step:
  - Start simple: `noise().out()`
  - Add transforms: `noise().color(1,0,0).out()`
  - Try combinations: `osc().rotate().scale().out()`
- Keep it simple, focus on the flow

---

## Lesson 4: Hyper-Hydra Modules (10min + 20min)

### Teaching (10min)
- **Introduction to external modules**
- **ShaderPark (glsl) integration demo:**
  - Navigate to: [ShaderPark Example](https://hydra.ojack.xyz/?code=Y29uc3QlMjAlN0IlMjBzY3VscHRUb0h5ZHJhUmVuZGVyZXIlMjAlN0QlMjAlM0QlMjBhd2FpdCUyMGltcG9ydCglMjJodHRwcyUzQSUyRiUyRnVucGtnLmNvbSUyRnNoYWRlci1wYXJrLWNvcmUlMkZkaXN0JTJGc2hhZGVyLXBhcmstY29yZS5lc20uanMlMjIp)
  - Show 3D sculptural possibilities
- **Extensibility of Hydra**

### Workshop 4 (20min)
**Goal:** Explore advanced modules and understand performance
- Reference: [Hyper-Hydra GitHub](https://github.com/geikha/hyper-hydra)
- Try the ShaderPark example
- Experiment with:
  - Image loading functions
  - Canvas size modifications
  - CPU-intensive operations
- Notice performance differences

---

## Lesson 5: Hydra-MIDI Integration (10min + 20min)

### Teaching (10min)
- **Real-time control with MIDI**
- **Music visualization possibilities**
- **Demo setup:**
  ```javascript
  await loadScript("https://6120.eu/public/midi.js")
  await midi.start({ channel: '*', input: '*' })
  midi.show()
  ```
- Show how MIDI values can control visual parameters

### Workshop 5 (20min)
**Goal:** Connect MIDI to visuals
- Navigate to: [MIDI Example](https://hydra.ojack.xyz/?code=YXdhaXQlMjBsb2FkU2NyaXB0KCUyMmh0dHBzJTNBJTJGJTJGNjEyMC5ldSUyRnB1YmxpYyUyRm1pZGkuanMlMjIp)
- Set up MIDI connection (virtual MIDI if no hardware)
- Try: `solid(note('*'), 0, 1).out()`
- Link different MIDI controls to visual parameters
- Create responsive audio-visual performances

---

# BONUS CONTENT (1 hour)

## Lesson 6: Collaborative Coding with Flok (10min + 20min)

### Teaching (10min)
- **Collaborative live coding concept**
- **Flok platform introduction**
- **Sharing sessions and real-time collaboration**
- **Community aspect of live coding**

### Workshop 6 (20min)
**Goal:** Experience collaborative visual coding
- Set up shared Flok session
- Practice collaborative etiquette
- Create group visual performances
- Share and iterate on each other's code

---

## Key Resources to Keep Handy:
- [Hydra Functions Reference](https://hydra.ojack.xyz/functions)
- [Hyper-Hydra Extensions](https://github.com/geikha/hyper-hydra)
- [Main Hydra Site](https://hydra.ojack.xyz)

## Workshop Philosophy:
- **Experimentation over perfection**
- **Happy accidents are learning opportunities**
- **Community and sharing enhances creativity**
- **Start simple, build complexity gradually**

# Hydra Functions Cheat Sheet

## Sources

### osc()
**Description:** Generates an oscillating wave pattern.
**Example:**
```javascript
osc(10, 0.1, 1).out()
```

### noise()
**Description:** Creates a noise texture.
**Example:**
```javascript
noise(3, 0.5).out()
```

### voronoi()
**Description:** Generates a Voronoi pattern.
**Example:**
```javascript
voronoi(5, 0.3, 0.8).out()
```

### shape()
**Description:** Renders a geometric shape.
**Example:**
```javascript
shape(4, 0.5, 0.1).out()
```

### gradient()
**Description:** Creates a gradient pattern.
**Example:**
```javascript
gradient(1).out()
```

### solid()
**Description:** Generates a solid color.
**Example:**
```javascript
solid(1, 0, 0).out()
```

## Modulation

### modulate()
**Description:** Modulates the source using another texture.
**Example:**
```javascript
osc(10, 0.1, 1).modulate(noise(3)).out()
```

### modulateScale()
**Description:** Modulates the scale of the source.
**Example:**
```javascript
osc(10, 0.1, 1).modulateScale(noise(3)).out()
```

### modulateRotate()
**Description:** Modulates the rotation of the source.
**Example:**
```javascript
osc(10, 0.1, 1).modulateRotate(noise(3)).out()
```

### modulatePixelate()
**Description:** Modulates the pixelation of the source.
**Example:**
```javascript
osc(10, 0.1, 1).modulatePixelate(noise(3)).out()
```

### modulateRepeat()
**Description:** Modulates the repetition of the source.
**Example:**
```javascript
osc(10, 0.1, 1).modulateRepeat(noise(3)).out()
```

### modulateScrollX()
**Description:** Modulates horizontal scrolling.
**Example:**
```javascript
osc(10, 0.1, 1).modulateScrollX(noise(3)).out()
```

### modulateScrollY()
**Description:** Modulates vertical scrolling.
**Example:**
```javascript
osc(10, 0.1, 1).modulateScrollY(noise(3)).out()
```

### modulateHue()
**Description:** Modulates the hue of the source.
**Example:**
```javascript
osc(10, 0.1, 1).modulateHue(noise(3)).out()
```

## Color

### color()
**Description:** Applies color to the source.
**Example:**
```javascript
osc(10, 0.1, 1).color(1, 0, 0).out()
```

### colorama()
**Description:** Applies a colorama effect.
**Example:**
```javascript
osc(10, 0.1, 1).colorama(0.5).out()
```

### saturate()
**Description:** Adjusts the saturation.
**Example:**
```javascript
osc(10, 0.1, 1).saturate(1.5).out()
```

### contrast()
**Description:** Adjusts the contrast.
**Example:**
```javascript
osc(10, 0.1, 1).contrast(1.5).out()
```

### brightness()
**Description:** Adjusts the brightness.
**Example:**
```javascript
osc(10, 0.1, 1).brightness(0.5).out()
```

### invert()
**Description:** Inverts the colors.
**Example:**
```javascript
osc(10, 0.1, 1).invert().out()
```

### luma()
**Description:** Applies a luma key.
**Example:**
```javascript
osc(10, 0.1, 1).luma(0.5).out()
```

### posterize()
**Description:** Applies a posterization effect.
**Example:**
```javascript
osc(10, 0.1, 1).posterize(3, 0.5).out()
```

## Geometry

### rotate()
**Description:** Rotates the source.
**Example:**
```javascript
osc(10, 0.1, 1).rotate(0.5).out()
```

### scale()
**Description:** Scales the source.
**Example:**
```javascript
osc(10, 0.1, 1).scale(1.5).out()
```

### pixelate()
**Description:** Applies a pixelation effect.
**Example:**
```javascript
osc(10, 0.1, 1).pixelate(10, 10).out()
```

### repeat()
**Description:** Repeats the source.
**Example:**
```javascript
osc(10, 0.1, 1).repeat(3, 3).out()
```

### repeatX()
**Description:** Repeats the source horizontally.
**Example:**
```javascript
osc(10, 0.1, 1).repeatX(3).out()
```

### repeatY()
**Description:** Repeats the source vertically.
**Example:**
```javascript
osc(10, 0.1, 1).repeatY(3).out()
```

### scroll()
**Description:** Scrolls the source.
**Example:**
```javascript
osc(10, 0.1, 1).scroll(0.1, 0.1).out()
```

### scrollX()
**Description:** Scrolls the source horizontally.
**Example:**
```javascript
osc(10, 0.1, 1).scrollX(0.1).out()
```

### scrollY()
**Description:** Scrolls the source vertically.
**Example:**
```javascript
osc(10, 0.1, 1).scrollY(0.1).out()
```

### kaleid()
**Description:** Applies a kaleidoscope effect.
**Example:**
```javascript
osc(10, 0.1, 1).kaleid(4).out()
```

## Blending

### add()
**Description:** Adds two sources.
**Example:**
```javascript
osc(10, 0.1, 1).add(noise(3)).out()
```

### sub()
**Description:** Subtracts one source from another.
**Example:**
```javascript
osc(10, 0.1, 1).sub(noise(3)).out()
```

### layer()
**Description:** Overlays one source on another.
**Example:**
```javascript
osc(10, 0.1, 1).layer(noise(3)).out()
```

### blend()
**Description:** Blends two sources.
**Example:**
```javascript
osc(10, 0.1, 1).blend(noise(3)).out()
```

### mult()
**Description:** Multiplies two sources.
**Example:**
```javascript
osc(10, 0.1, 1).mult(noise(3)).out()
```

### diff()
**Description:** Calculates the difference between two sources.
**Example:**
```javascript
osc(10, 0.1, 1).diff(noise(3)).out()
```

### mask()
**Description:** Applies a mask to the source.
**Example:**
```javascript
osc(10, 0.1, 1).mask(shape(4, 0.5, 0.1)).out()
```

## Utilities

### out()
**Description:** Outputs the current buffer.
**Example:**
```javascript
osc(10, 0.1, 1).out()
```

### render()
**Description:** Renders the specified buffer.
**Example:**
```javascript
render(o1)
```

### initCam()
**Description:** Initializes the webcam.
**Example:**
```javascript
s0.initCam()
src(s0).out()
```

### initVideo()
**Description:** Initializes a video source.
**Example:**
```javascript
s0.initVideo("path/to/video.mp4")
src(s0).out()
```

### initImage()
**Description:** Initializes an image source.
**Example:**
```javascript
s0.initImage("path/to/image.jpg")
src(s0).out()
```

### src()
**Description:** Sets the source for the pipeline.
**Example:**
```javascript
src(o0).out()
```

### time
**Description:** Global variable representing elapsed time.
**Example:**
```javascript
osc(10, 0.1, 1).rotate(() => time).out()
```

### speed
**Description:** Global variable controlling playback speed.
**Example:**
```javascript
speed = 0.5
```

### mouse
**Description:** Global variable representing mouse position.
**Example:**
```javascript
osc(10, 0.1, 1).rotate(() => mouse.x * 0.01).out()
```

### a.fft
**Description:** Array representing audio frequency data.
**Example:**
```javascript
osc(10, 0.1, 1).modulate(noise(() => a.fft[0] * 10)).out()
```

### a.setSmooth()
**Description:** Sets the smoothing for audio analysis.
**Example:**
```javascript
a.setSmooth(0.8)
```

### a.setBins()
**Description:** Sets the number of frequency bins for audio analysis.
**Example:**
```javascript
a.setBins(4)
```

### a.setCutoff()
**Description:** Sets the cutoff frequency for audio analysis.
**Example:**
```javascript
a.setCutoff(2)
```

### a.setScale()
**Description:** Sets the scale for audio analysis.
**Example:**
```javascript
a.setScale(2)
```
