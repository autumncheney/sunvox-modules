# abstract

a variant of my chip perc single module, where instead of controlling a single drum sound, it controls a set of twelve sounds via a random seed. each sound is mapped to a key on the keyboard, with the sounds repeating every octave

designed to generate drum sounds reminiscent of old computer chips via amplitude and frequency modulation. it works by generating three waveforms with an asr envelope and frequency modulating the first by the second and amplitude modulating the first by the third

heavily inspired by nightradio's fractal bits app, especially with the effects (which are literally ripped from the fractal bits sunvox export)

note that the sounds are keytracked to the octave, so you can get variations of each sound when playing on dfferent octaves

great as percussion for music genres like idm and glitch

the noise curves were generated by pixilang, i'll see if i can find the original file

# controls

## group 1: seed control

- seed: controls the drumkit seed. note that while there are 256 distinct seeds, they are also interpolated, so you can get variations on the current seed +/-128 units from the current seed

## group 2: spatial controls

- stereo: the stereo width of the drum sounds + effects. 0 is mono, and 128 (4000) is no change

## group 3: effect controls

- reverb: the amount of reverb on the drums. note that this controls both the wet and the feedback of the reverb
- overdrive: the amount of waveshaping on the signal. based on a custom waveshaper curve
- lofi: the amount of sample rate reduction (digitzation) on the signal. note that this is exponential. 0 = no reduction

## group 4: sound2ctl sample rate settings

- envelope sample rate: the sample rate of the sound2ctl module in hertz. requested by nightradio. increasing this increases the granularity at the cost of processing power. according to nr, 150 hz is the sweet spot
