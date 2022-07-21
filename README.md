# Developing a Language Model for Nsyilxcn

## Background
I apply the approach from 'Forced Alignment for Understudies Languages Varieties' [1] to the language of Nsyilxcn using a new alignment tool (MFA) and what little available online data there is for the language. 

## 1) Data Preparation
The MFA requires the following for training and alignment:
- [audio files](https://montreal-forced-aligner.readthedocs.io/en/latest/user_guide/corpus_structure.html#corpus-structure)
- [transcription files](https://montreal-forced-aligner.readthedocs.io/en/latest/user_guide/corpus_structure.html#corpus-structure)
- [pronunciation dictionary](https://montreal-forced-aligner.readthedocs.io/en/latest/user_guide/dictionary.html#dictionary-format)

### 1.1) Audio Files
I recieved the audio corpus from Craig. I went through each file, trimmed the audio and saved it with a meaningful name. Theses files go in ```unprocessed/audio``` in the [Nsyilxcn-Corpus-Generation](https://github.com/jkranabetter/Nsyilxcn-Corpus-Generation) repository.

### 1.2) Transcription Files
I revieced the transcription files from Craig. I corralated the transcriptions to the audio and saved each audio files corresponding Nsyilcxn text in a ```.txt``` file with the *same name* as the audio file. Theses files go in ```unprocessed/text``` in the [Nsyilxcn-Corpus-Generation](https://github.com/jkranabetter/Nsyilxcn-Corpus-Generation) repository.

### 1.3) Processing the dataset
In the [Nsyilxcn-Corpus-Generation](https://github.com/jkranabetter/Nsyilxcn-Corpus-Generation) repository, process the dataset. Instructions in the readme file. Each speaker should have their own folder. The processed dataset will be in the ```sound corpus``` folder. 

### 1.4) Move the Dataset to this Repository
Next I moved the processed dataset from the [Nsyilxcn-Corpus-Generation](https://github.com/jkranabetter/Nsyilxcn-Corpus-Generation) repository into this repository under the ```SoundCorpus``` folder.

## 2) Pronunciation Dictionary
To generate the pronunciation dictionary we need three things:
- An Nsyilxcn dictionary
- A phonetic system 
- A map for Nsyilxcn to phones

### 2.1) An Nsyilxcn dictionary
I scraped the dictionary from this [Online Nsyilxcn Dictionary](https://www.meltr.org/CvDict/lexicon/index.htm?fbclid=IwAR3k63PS3PPnNiDT6xFYLGlGbqiL990Ra9c6w6jVpW-uWrpMuTxHJyrzvFY). 

### 2.2) A Phonetic System
I chose the [IPA system](https://www.ipachart.com/) because it looked to have the most coverage of Nsyilxcn sounds. If you change the phones set make sure to modify the MFA commands. For example the current commands are set to IPA as seen in: 
 ```mfa validate --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt```.

### 2.3) A Map for Nsyilxcn to Phones
 I did my best to interpret based on a pronunciation guide. This can be changed and regenerated. Just replace the ```nsyilxcn_mappings.txt``` file in this repo. More information on mappings in the [Nsyilxcn-Corpus-Generation](https://github.com/jkranabetter/Nsyilxcn-Corpus-Generation) repository. 

 ## 3) Load in your Unaligned Data
 Put your data to be aligned in the ```input``` folder. The output will be in the ```output``` folder. 

 ## 4) Run the repository
If you havent set up your environment get check the 'setting up your environment'  section below.
### 4.1) Activate your environment
Activate your environment before you use the MFA. The environment closes when you close VSCode.
```
conda activate mfa-dev
```
### 4.2) Validate your data
Check to make sure you have obeyed the holy laws of MFA formatting for the dataset. If you have issues here check the MFA reference and try the --clean command.
```
mfa validate --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt
```

### 4.3) Train the model
You have 3 options depending on what you want to output.\
Export just the trained acoustic model:
```
mfa train --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt ./mfa_data/new_acoustic_model.zip 
```
Export just the training alignments:
```
mfa train --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt  ./mfa_data/my_corpus_aligned 
```
Export both trained model and alignments:
```
mfa train --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt  ./mfa_data/new_acoustic_model.zip ./mfa_data/my_corpus_aligned  
```

### 4.4) Align using the Trained Model
Finally we can align on new data using our trained model:
```
mfa align ./input nsyilxcn_mappings.txt mfa_data/new_acoustic_model.zip ./output
```

## References
 - [1] https://scholarspace.manoa.hawaii.edu/server/api/core/bitstreams/5fd5e5c0-b211-460f-ad74-fb2e14e61709/content

# Montreal Forced Aligner

The Montreal Forced Aligner is a command line utility for performing forced alignment of speech datasets using Kaldi (http://kaldi-asr.org/).

Please see the documentation http://montreal-forced-aligner.readthedocs.io for installation and usage.

If you run into any issues, please check the [mailing list](https://groups.google.com/forum/#!forum/mfa-users) for fixes/workarounds or to post a [new issue](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner/issues).

## Installation

You can install MFA either entirely through [conda](https://docs.conda.io/en/latest/) or a mix of conda for Kaldi and Pynini dependencies and Python packaging for MFA itself

### Conda installation

MFA is hosted on [conda-forge](https://conda-forge.org/) and can be installed via:

```
conda install -c conda-forge montreal-forced-aligner
```

in your environment of choice.

### Setting up the environment

Running this repository for the first time you will need to create an environment using the command:
```
conda env create -n mfa-dev -f environment.yml  # Linux or mac
```

Next time, we only need to activate the enviroment using:
```
conda activate mfa-dev
```

You should be able to see appropriate output from the command `mfa version`


fe's forced alignment blog posts](https://memcauliffe.com/tag/forced-alignment.html)

## Quick links
* [Getting started docs](https://montreal-forced-aligner.readthedocs.io/en/latest/getting_started.html)
* [User Guide](https://montreal-forced-aligner.readthedocs.io/en/latest/user_guide/index.html)
* [API Reference](https://montreal-forced-aligner.readthedocs.io/en/latest/reference/index.html)
* [Release notes](https://montreal-forced-aligner.readthedocs.io/en/latest/changelog/index.html)
* [MFA Models](https://github.com/MontrealCorpusTools/mfa-models)
* [Eleanor Chodroff's MFA tutorial](https://www.eleanorchodroff.com/tutorial/montreal-forced-aligner-v2.html)
* [@mmcaulif