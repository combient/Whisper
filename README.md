# I simple colab notebook to use OpenAI's Whisper model

Forked from https://github.com/AndrewMayneProjects/Whisper
This is not production-ready code. It is a proof of concept.

### Whisper Google Drive Video Transcription Python Notebook

This connects to your Google Drive and will batch process video files uploaded to /WhisperVideo

It will generate a json file with the transcription divided up according to punctuation and
with timestamps for each sentence.

### How to use

1. Upload a video to your Google Drive in the `/WhisperVideo folder` ( you can also reuse
a video from the `/WhisperVideo/ProcessedVideo` directory by moving it back to 
the `/WhisperVideo` folder and deleting the files under `JsonFiles`, `TextFiles`and `AudioFiles`).

2. Open the notebook in Google Colab and run all the cells.

3. Check the `/WhisperVideo/JsonFiles` folder for the json file with the transcription.

### Example json output

````json
[
    {
        "end": 14.48,
        "start": 0.0,
        "text": " So it seems like I need to record more audio for Whisper to be able to learn my speech patterns and for Whisper to correctly punctuate what I'm saying."
    },
    {
        "end": 19.32,
        "start": 14.48,
        "text": "So in order to provide some more verbiage here I'm just gonna babble for a little bit."
    }
]
````
### Extract text from json

````shell
jq -r '.[] | "[start: \(.start), end: \(.end)] :  \(.text)"' output.json
````

to output

````
[start: 0, end: 14.48] :   So it seems like I need to record more audio for Whisper to be able to learn my speech patterns and for Whisper to correctly punctuate what I'm saying.
[start: 14.48, end: 19.32] :  So in order to provide some more verbiage here I'm just gonna babble for a little bit.
````