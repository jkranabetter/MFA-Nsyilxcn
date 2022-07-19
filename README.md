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

## Commands for this implimentation
First, validate your data.
```
mfa validate --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt
```
Then we can train the acoustic model and export it + training alignments.
```
mfa train --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt ./mfa_data/new_acoustic_model.zip  # Export just the trained acoustic model
mfa train --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt  ./mfa_data/my_corpus_aligned --clean # Export just the training alignments
mfa train --phone_set IPA ./SoundCorpus nsyilxcn_mappings.txt  ./mfa_data/new_acoustic_model.zip ./mfa_data/my_corpus_aligned  # Export both trained model and alignments
```

## Align

Finally we can align on new data using our trained model:
```
mfa align ./input nsyilxcn_mappings.txt mfa_data/new_acoustic_model.zip ./output
```

## Quick links
* [Getting started docs](https://montreal-forced-aligner.readthedocs.io/en/latest/getting_started.html)
* [User Guide](https://montreal-forced-aligner.readthedocs.io/en/latest/user_guide/index.html)
* [API Reference](https://montreal-forced-aligner.readthedocs.io/en/latest/reference/index.html)
* [Release notes](https://montreal-forced-aligner.readthedocs.io/en/latest/changelog/index.html)
* [MFA Models](https://github.com/MontrealCorpusTools/mfa-models)
* [Eleanor Chodroff's MFA tutorial](https://www.eleanorchodroff.com/tutorial/montreal-forced-aligner-v2.html)
* [@mmcaulif