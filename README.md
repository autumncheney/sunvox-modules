# abstract
here are all the sunvox modules i've made. they are sorted based on sunvox's own module library. this commit also contains documentation and notes for each module

to get the modules, simply clone this repo, move the archive to sunvox's root directory, and tell your file manager to merge the directories

these require at least version 2.0 for the controller colors and extra controllers. idk what happens if you try to load these in sunvox 1.9.6c or lower

feel free to report bugs with the modules or documentation or even request new ones in the issue tracker :>

WARNING: the documentation is out of date (and has been for the past year). it will be updated in the future as part of a new project

# template
this repo also contains my default sunvox template for creating new songs. i will explain what it does and how to make use of it in this section

## overview

![template](https://user-images.githubusercontent.com/76746896/212500637-c6f83758-d29d-4aa2-9aeb-74270b50a089.png)

this template implements clip-to-zero (ctz), a mixing strategy for making loud and clean masters. essentially, it uses clipping (and limiting) to control the dynamics of sounds and busses and make them louder. additionally, in ctz, the core drums (usually kick and snare) are deliberately sent to -0.0 dbfs to make them as loud as possible, and all other sounds are sidechained (ducked) out of their way. you can learn more about it [here](https://docs.google.com/document/d/1Ogxa5-X_QdbtfLLQ_2mDEgPgHxNRLebQ7pps3rXewPM/edit) and [here](https://www.youtube.com/playlist?list=PL8r1b6466J-96DEGHcFLd52zSZ0ntMfPC)

this template also includes utilities for metering and drum kit creation. see the various parts for detailed information

## metering

![template-monitoring](https://user-images.githubusercontent.com/76746896/212500751-c6845ac7-b3ab-4bfa-a834-5fcbb60ef411.png)

this metering section includes a variety of meters and an a/b comparison utility for comparing between the master output and a reference, to be loaded into the "reference" sampler and played in the pattern (there is a "reference" pattern there by default, the starting position of the sample can be controlled using the "phase" controller in the "phase" multisynth

to a/b, simply set the multictl labelled "ctl a/b" to 32768 (8000) to enable the sampler output. the sampler's output will be sent to the meters and to the output module. all other values will allow the master (a) through

the meters include a lufs meter (by fuzion_mixer and logickin), a stereo scope (goniometer), peak meter, and rms meter. the peak and rms meters are compressors, so you can view the envelope of the material in the module's controller settings

## busses

![template-busses](https://user-images.githubusercontent.com/76746896/212500940-3be39f4d-e490-4efc-8bf5-652aabf2c30d.png)

the template includes some default busses and sub-busses, though of course these can be changed to your liking. they are, from left to right:

- framework drums
  - kick
  - snare
  - toms
- non-framework drums (tops)
  - hihats
  - cymbals (rides, short crashes, etc)
  - misc percussion
- basses
  - sub bass (basses that lack mid-frequency content)
  - mid bass (basses with heavy mid-frequency content)
- fx (sound effects)
  - sustained fx (effects with a longer or sustained volume envelope; risers, background noise, etc)
  - transient fx (effects with a shorter volume envelope; impacts, special percussion, vocals (non-melodic), etc)
- melodic (mid-to-high sounds with tonal content)
  - chords
  - melodies (arps, interminent melodic effects, etc)
  - leads
  - pads
  
the bass, fx, and melodic busses are sent to a "non-framework" bus

## ducking

![template-ducking](https://user-images.githubusercontent.com/76746896/212501115-a40d9e4c-a5cc-4acc-844a-32984bb72229.png)

the output of the non-framework bus is ducked using the three ducker modules (right red box), triggered by the framework triggers (left red box). it is intended that the framework sounds are triggered by multisynths, which should be routed to the framework triggers for automatic ducking. the framework triggers themselves can also be directly triggered in a pattern, for sidechain effects. the amount of the ducking can be controlled using the "velocity" controller of the trigger multisynths

to determine the optimal ducker settings, record the processed drum sound into a sampler, crop the sample to the most relevant part, and note the total length; the "hold" and "release" controllers of the ducker should add up to this time. the balance between them should be determined by inspection of the amplitude envelope of the sample; the hold time should last while the sound has a relatively flat envelope, while the release time should last while the sound fades out

## drumkits

![template-kit](https://user-images.githubusercontent.com/76746896/212501279-eb3b9202-25ae-4390-b2c9-eec32938c1af.png)

this template includes a setup for making drumkits. the "trigger" multisynth is the note input for the kit; starting at note c0, the sounds of the kit will be distributed across the keyboard according to the "out.port = note % num of outs" algorithm (see the sunvox manual for info)

for each kit, the drum sounds within each have a note input, the sound module (or modules), and a "mix" amplifier to mix the sound; the sounds are then sent to an "input" amplfiier to be commonly processed. the default sounds are kicker modules, and you will probably want to replace them with something else

to add drums to the kit, copy and paste one of the input-sound-mix tuplets and connect the "dist" multisynth to the input and the "mix" amplifer to the "input" amplifier. it is recommended to order the sounds left-to-right for clearer apparent note distribution

note that this kit setup is not just for drums, you can also have tonal sounds layered this way (with the "dist" module's distribution disabled) to allow them to share common processing :>

## adding new sounds

![template-new-sounds](https://user-images.githubusercontent.com/76746896/212501560-8eb69aa8-ff15-4ca4-88b0-61def1b0e177.png)

an example of adding new sounds to the template is provided above. the best practice is to have a multisynth trigger every sound, and the sound's output to be sent to a bus module (whether it is a bus lite, bus, or bus pro depends on the mixing need). optionally, a fader can be placed after the bus. this should then be sent into the bus input module








