# SONIC PI WORKSHOP

## Introduction
- Algorave Video
- Sonic Pi (Instrument / Programming)
- Raspi, Interfaces, Ruby
- Minecraft, Research Data (Pure Data)
- Live Performance

## Sources
- [Sonic Pi Webpage]()
- [Sonic Pi Documentation]()
- [YouTube Tutorial](https://www.youtube.com/playlist?list=PLaitaNxyd8SHvTQjRGnMdKLsARXW7iYyp)
- [Mehackit Workshop](https://sonic-pi.mehackit.org/)

## Coding Environment
- Ruby ( Lines, Variables, Functions)
- Help
- Preferences
- Buffer

## Basics
- `puts "Hello World"`
- PLAY Pitch Number
  - MIDI Number
  - Name :D5
  - :r
- Parallel Execution -> SLEEP
- basic loop with `x.times do end`
- USE_BPM (Default 60)
- **EXERCISE:** Write basic Melody
- USE_SYNTH

## MOAR PARAMETERS
- amp :
  - 0, 1, >1
  - `play 50, amp: 0.1` 
- pan :
  - -1 to 1
- ADSR :
  - timing in beats
  - release, attack, sustain, decay
  - attack_level, decay_level

## SAMPLES
- `sample :ambi_lunar_land`
```
sample :ambi_lunar_land
sleep 1
play 48
sleep 0.5
play 36
sample :ambi_drone
sleep 1
play 36
```
- `sample :ambi_choir, rate: 0.5`
- rate
  - 0 - 1, >1, <0
- attack, release, sustain
- start, finish
- sample_duration
- chopping
```
live_loop :samplechopper do
  sample :loop_amen_full, num_slices:8, slice:rrand_i(0,7)
  sleep sample_duration(:loop_amen_full) / 8
end
```

## LOOPS
- x.times do
- loop do end
- Threads
  - Scopes
```
in_thread do
  loop do
    sample :drum_heavy_kick
    sleep 1
  end
end

loop do
  use_synth :fm
  play 40, release: 0.2
  sleep 0.5
end
```
- live_loop

```
live_loop :foo do
  sample :loop_garzul
  use_synth :prophet
  play :c1, release: 8, cutoff: rrand(70, 130)
  sleep 8
end
```

```
live_loop :hello do
  at [0, 1, 2, 3] do
    sample :drum_bass_soft
  end
  at [0.5,1,1.5,2,3.5] do
    sample :hat_bdu
  end
  sleep 4
end
```

- **EXERCISE:** write basic drum rythm

```
use_bpm 100

live_loop :drums do
  sample :drum_heavy_kick
  sleep 1
  sample :drum_snare_hard
  sleep 1
  sample :drum_heavy_kick
  sleep 1
  sample :drum_snare_hard
  sleep 1
end

live_loop :hihat do
  sample :drum_cymbal_closed
  sleep 0.25
  sample :drum_cymbal_pedal
  sleep 1
end

live_loop :bass do
  use_synth :fm
  play :c2, attack: 0, release: 0.25
  sleep 0.25
  play :c2, attack: 0, release: 0.3
  sleep 2
  play :e2
  sleep 0.75
  play :f2
  sleep 1
end

live_loop :melody do
  play_pattern_timed [:c4, :e4, :f4, :g4, :f4, :e4, :f4, :g4, :f4, :e4, :f4], [0.25, 0.25, 0.25, 1.5, 0.25, 0.25, 0.25, 0.25, 0.25, 0.25], attack: 0, release: 0.2
end
```


## RANDOM
- if one_in(x), BLOCK or SIMPLE
- Loop do play rrand(50,80) sleep 1 -> Float Values
- random amp, pan etc...
- rrand_i
- use_random_seed

## STRUCTURES
- List `play [c4,d4,e4][0]`
  - Tick
  - Choose
```
10.times do
  play [51,54,55,56].choose
  sleep 0.5
end
```
- Rings
- Chords `puts chord(:E3, :m7)`
  - Arpeggios `play_pattern_timed chord(:E3, :M7), 0.25`
- Scales `scale(:C3, :harmonic)`
```
use_synth :tb303
loop do
  play choose(scale(:E3, :minor)), release: 0.3, cutoff: rrand(60, 120)
  sleep 0.25
end
```

```
chords = [(chord :C, :minor7), (chord :Ab, :major7), (chord :Eb, :major7), (chord :Bb, "7")].ring
c = chords[0] # take the first chord of the ring and save it to a variable

live_loop :melody do
  use_synth :blade
  r = [0.25, 0.25, 0.5, 1].choose
  play c.choose, attack: 0, release: r
  sleep r
end

live_loop :keys do
  use_synth :blade
  play c
  sleep 1
end

live_loop :bass do
  use_synth :fm
  use_octave -2
  3.times do
    play c[0] # play the first note of the chord
    sleep 1
  end
  play c[2] # play the third note of the chord
  sleep 0.5
  play c[1] # # play the second note of the chord
  sleep 0.5
  c = chords.tick
end
```
- Functions
- Functions
```
define :chord_player do |root, repeats|
  repeats.times do
    play chord(root, :minor), release: 0.3
    sleep 0.5
  end
end
```

## EFFECTS
- with_fx :echo do
```
with_fx :echo, phase: 0.5, decay: 8 do
  play 50
  sleep 0.5
  sample :elec_plip
  sleep 0.5
  play 62
end
```
- see FX help
- Nesting FX

## PERFORMING
- Controlling Running Sound, run-local variable
```
s = play 60, release: 5
sleep 0.5
control s, note: 65
sleep 0.5
control s, note: 67
sleep 3
control s, note: 72
```
- FX
```
with_fx :reverb do |r|
  play 50
  sleep 0.5
  control r, mix: 0.7
  play 55
  sleep 1
  control r, mix: 0.9
  sleep 1
  play 62
end
```


