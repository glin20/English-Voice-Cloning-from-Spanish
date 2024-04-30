# English-Voice-Cloning-from-Spanish
Code Submission for Group 8 (Jacob Karvelis, Geoffrey Lin, Ryan Moore, and Steven Wells). Will be deleted after being scored.

Implementation using a clone of Corentin Jemine's Real-Time Voice Cloning with a Spanish dataset instead of English.

Included is the original code from Coretin Jemine's repository along with a trained model from a Spanish dataset from LibriSpeech. Also included is the Montreal Forced Aligner program written by Steven.

Link to original repository: https://github.com/CorentinJ/Real-Time-Voice-Cloning

### 1. Requirements (on CS Servers (no GPU))
1. Create and activate a Conda environment (preferably in Python v3.7.0)
2. Install ffmpeg (conda install ffmpeg)
3. Install PyTorch (conda install pytorch torchvision torchaudio cpuonly -c pytorch)
4. Install from requirements.txt (pip install -r requirements.txt)
5. Install portaudio (conda install portaudio)

### 2. Downloading Models
1. Navigate to saved_models
2. Run curl -L "https://drive.usercontent.google.com/download?id=1TkWlsRfKxzKqQDWE-UJPuYzmto2BeqBO&confirm=xxx" -o spanish_1.zip
3. Unzip spanish_1.zip using unzip spanish_1.zip -d spanish_1
4. Run curl -L "https://drive.usercontent.google.com/download?id=1U_lllUfjUqgdA9l4ZJs_MPI5Y38UJgZ_&confirm=xxx" -o default.zip
5. Unzip using unzip default.zip

### 3. Running
1. Launch using python demo_toolbox.py
2. Select the Spanish-1 under Encoder, Synthesizer, and Vocoder
3. Enter text you want to be said in generation
4. Record or choose a audio file under embeddings
5. Synthesize and vocode
   	* Since it's running on CS Servers you'll likely have to use an application such as MobaXterm in order to access the file and play the audio through it.

### Extra (Running the Aligner)
1. First run the split_transcripts.py file specifically with line 34 uncommented and line 35 commented out. Pass it the --t transcript file which should be the one file containing every transcript for the whole dataset, and give it the -o argument to specify the output directory, which should be the directory where the dataset is kept. This will split the transcript file into individual transcript files for each book. These files are what the script that preprocesses librispeech data for the MFA expects.
2. Next run the reorganize_librispeech_pre_align.py script. This script will reorganize the librispeech dataset into the format that the MFA expects. You have to manually set the directories that it takes from and outputs to, and the output directory should be a directory visible to the MFA aligner (this is important if you are using a docker container).
3. Now you are ready to run the MFA aligner, and my recommendation for this step is to install version 2.2.17 in a docker container. Set up the docker container so that it can see the directory where the reorganized librispeech dataset is stored. Upon starting the MFA aligner, first run the mfa validate command which will validate that the dataset is compatible with the aligner. Next, run mfa model download acoustic mfa_spanish to download the Spanish acoustic model and mfa model download dictionary mfa_spanish to download the spanish dictionary. Finally, run the mfa align DATASET_DIRECTORY mfa_spanish mfa_spanish OUTPUT_DIRECTORY command to align the dataset. This will generate .TextGrid files for each audio file in the dataset.
	If you can't use docker you can also use conda following this: https://montreal-forced-aligner.readthedocs.io/en/latest/installation.html
4. Now that the dataset has been aligned, run the reorganize_alignments_post_align.py script which will reorganize the sound files and textgrids into a directory structure that our repo expects. You have to manually set the directories that it takes from and outputs to for this script as well.
5. Finally, run the process_textgrids.py script which converts the textgrids into a format that the MFA expects. Just set the input directory to the directory that the previous script created, and this script will take the textgrids and from them create .alignment.txt files for each book in the dataset.
6. Now you can use this dataset with our repository.

### Extra (Training the models)
Read the original steps by CorenteinJ: https://github.com/CorentinJ/Real-Time-Voice-Cloning/wiki/Training
