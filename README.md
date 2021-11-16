# CloudHSM-model

This repository contains the Tamarin prover model that we used to specify and check the Cloud HSM secure configuration described in the paper:

R. Focardi and F. L. Luccio. *A Formally Verified Configuration for Hardware Security Modules in the Cloud*. [ACM CCS 2021](https://www.sigsac.org/ccs/CCS2021/), November 2021. [[Conference proceedings and presentation](https://dl.acm.org/doi/10.1145/3460120.3484785)][[Author's version on arxiv](https://arxiv.org/abs/2109.13631)].

## Model

Currently, we make available two versions of the model:

- The [original Tamarin prover model](https://github.com/secgroup/CloudHSM-model/blob/main/HSM_model_CCS_cameraready.spthy) from the CCS paper;
- An [updated Tamarin prover model](https://github.com/secgroup/CloudHSM-model/blob/main/HSM_model_CCS_updated.spthy) with the following improvements with respect to the original model:

	- We now use `K(...)` instead of `KU(...)` to model attacker knowledge in the three secrecy lemmas as `KU` is, in fact, Tamarin-internal. Lemmas are still proved automatically but the check is a bit slower (see below). Many thanks to Cas Cremers for spotting this.

## Prerequisites

To check the model you need to install the [Tamarin prover](https://tamarin-prover.github.io/).

## Usage

The reported execution times were obtained on a 2018 MacBook pro.

The full model can be checked with Tamarin in about `1m50s` (`1m30s` for the original model) as follows:

```bash
$ tamarin-prover --prove HSM_model_CCS_updated.spthy
```

The full model includes one helper lemma used to make the proof converge (named `Unwrap`) and a number of sanity lemmas. 

Checking just the secrecy lemmas takes about `1m` (`22s` for the original model):

```bash
$ tamarin-prover --prove=Secrecy* HSM_model_CCS_updated.spthy
```

Checking just the `Unwrap` helper lemma takes about `1m04s`:

```bash
$ tamarin-prover --prove=Unwrap HSM_model_CCS_updated.spthy
```

