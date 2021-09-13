# CloudHSM-model
Cloud HSM secure configuration: To appear at ACM CCS, November 2021

This repository contains the [Tamarin prover](https://tamarin-prover.github.io/) models that we used to specify and check a Cloud HSM secure configuration described in the paper *A Formally Verified Configuration for Hardware Security Modules in the Cloud*, by R. Focardi and F. L. Luccio, accepted for publicatin at [ACM CCS 2021](https://www.sigsac.org/ccs/CCS2021/) in November 2021.

## Prerequisites

To check the model you need to install the [Tamarin prover](https://tamarin-prover.github.io/)

## Usage

The full model can be checked with Tamarin as follows (about 1m50s on a MacBook pro 2018):

```bash
$ tamarin-prover --prove HSM_model_CCS_cameraready.spthy
```

To only check the secrecy lemma (about 22s on a MacBook pro 2018):

```bash
$ tamarin-prover --prove=Secrecy* HSM_model_CCS_cameraready.spthy

```


