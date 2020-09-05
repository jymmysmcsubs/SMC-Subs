# SMC-Subs

## Scripts

### Vapoursynth BD x264 Opus Raw Encoderer Bash Script
Some parts of this script are genericised, but it is mostly based on how I currently like to structure my fansub project folders and filenames. This script has a spot to define variables specific to your encoding project: i.e. x264 arguments, your group tag, the name of the show you want to encode and what you want to go in brackets after the episode number, e.g. "[SMC-Raws] PriPara - 001 (BD 720p Opus)". It also uses [this script](https://gist.github.com/Myaamori/dfb0030fd4ee44364ca3b0c2c9c9b4aa) to create keyframes and gives you an area to write the path to it.

It assumes the filename for the Vapoursynth script you provide as this script's argument has the episode number with the right number of leading 0s before the file extension, "e.g. PriPara001.vpy" (PriPara has >99 episodes, otherwise it would just be PriPara01.vpy).

It also assumes the file the audio should come from is in quotation marks in the first line that has ``src`` in it, e.g. ``src = core.lsmas.LWLibavSource("/path/to/file.m2ts")`` and currently it doesn't evaluate any delay or duration from the Vapoursynth script, but rather gets the duration from the video once encoded and assumes there are no blank or otherwise unused frames at the start of the source video (this is an obvious area to be improved).

You are also expected to put the episode title in a commented out line of the Vapoursynth script as so: ``#Episode_Title:Example Translated Episode Title``. This is because I like having the title in the MKV file be in the format this script gives it, e.g.: "PriPara 1: I Became an Idol?!". Leading zeros are removed from the episode number for the MKV title field.

Currently ffmpeg converts the audio to 16bit wav due to this issue with the Opus encoder: https://gitlab.xiph.org/xiph/opus-tools/-/issues/2315

Dependencies are Vapoursynth (and thus Python), x264 and Opus (obviously), as well as ffmpeg, mkvtoolnix and cksfv. Also the [keyframes script](https://gist.github.com/Myaamori/dfb0030fd4ee44364ca3b0c2c9c9b4aa) I mentioned. Also, it's a Bash script and uses shell utilities like grep and awk.
