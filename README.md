# MATLAB-Audio-Labeler-Google-Cloud-Speech-to-Text-LongRunningRecognize-with-Python
My attempt at fixing the MATLAB Audio Labeler app's Speech-to-Text function's issues with regards to using Google's cloud-based speech-to-text service. This program leverages Python to automatically upload and run long_running_recognize on compatible audio files. No more error messages from Audio Labeler's built-in Speech-to-Text function that your audio recording is too long.

Originally intended to trancribe files for grading of speech accuracy.
Includes labels for speakers and accuracy (can be ignored if not wanted).

### This program may require an understanding of Python. It certainly wouldn't hurt.

## How It Works
1. MATLAB and its easy uigetfile function are used to allow the user to select their audio file.
2. The file is remixed to a mono .wav file if it's not already.
3. The file and necessary inforation are then passed to the Python script that uploads the file to a Google Cloud Storage bucket, performs the transcription, and passes back the results.
4. MATLAB then turns the results into a table of words with start and end times, and then further into a Labeled Signal Set (lss) linked to the audio file.
5. MATLAB then saves both the table and the lss before opening Audio Labeler and prompting the user to load the Labeled Signal Set either from the saved file or from the workspace.

## Setup
Before you use this program, there are a number of steps required to get everything up and working.
1. Install [Python](https://www.python.org/downloads/).
2. Run the MATLAB_Speech_Recog_SETUP.py file. It should be under /PythonFiles. The script should end with this message: "Looks like everything works as intended! You're ready to begin!". If so, you can skip the next step. If not, try the next step before going further.
3. Double check that you have successfully installed the google-cloud-speech and google-cloud-storage libraries by opening a terminal, typing "python" and hitting enter to start the Python shell, and then typing "from google.cloud import speech" and pressing enter and then "from google.cloud import storage" and pressing enter. If this all works without error, you're good to proceed. If not, then you may have to manually install the google-cloud-speech and google-cloud-storage libraries.
4. Set up your [Google Cloud Speech-to-Text API](https://cloud.google.com/speech-to-text/docs/quickstart-client-libraries).
5. Download your [Google Cloud authorization JSON file](https://cloud.google.com/speech-to-text/docs/libraries) and store it someplace safe. We recommend the /data folder in /PythonFiles.
6. Create a [Google Cloud Storage bucket](https://cloud.google.com/storage/docs/creating-buckets) to store your audio files.
7. Create a folder in your Google Cloud Storage bucket named __TranscriptionOutput__.
8. Change the paths for your download of the Python script folder. (Lines 49 and 50 in the GoogleSpeech2TextPipeline.m file.)
9. Change the path to your Google Cloud authorization JSON file. (Line 60 in the GoogleSpeech2TextPipeline.m file.)
10. Change the name of the bucket to the name of your Google Cloud Storage bucket. (Line 56 in the GoogleSpeech2TextPipeline.m file.) *Bucket names are unique identifiers, so make sure to use **just** the name of the bucket. **NOT** gs://your_bucket_name. **JUST** your_bucket_name.*

Once all of that is complete, you should be ready to fire up MATLAB and run GoogleSpeech2TextPipeline.m. If you've set up everything correctly, it should work!
