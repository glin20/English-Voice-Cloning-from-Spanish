# English-Voice-Cloning-from-Spanish
Code Submission for Group 8 (Jacob Karvelis, Geoffrey Lin, Ryan Moore, and Steven Wells). Will be deleted after being scored.

Implementation using a clone of Corentin Jemine's Real-Time Voice Cloning with a Spanish dataset instead of English.

Included is the original code from Coretin Jemine's repository along with a trained model from a Spanish dataset from LibriSpeech. Also included is the Montreal Forced Aligner program written by Steven.

### 1. Requirements (on CS Servers (no GPU))
1. Create and activate a Conda environment (preferably in Python v3.7.0)
2. Install ffmpeg (conda install ffmpeg)
3. Install PyTorch (conda install pytorch torchvision torchaudio cpuonly -c pytorch)
4. Install from requirements.txt (pip install -r requirements.txt)
5. Install portaudio (conda install portaudio)

### 2. Running
1. Launch using python demo_toolbox.py
2. Select the Spanish-1 under Encoder, Synthesizer, and Vocoder
3. Enter text you want to be said in generation
4. Record or choose a audio file under embeddings
5. Synthesize and vocode
