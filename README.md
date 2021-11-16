# CloudHSM-model

This repository contains the Tamarin prover model that we used to specify and check the Cloud HSM secure configuration described in the paper 

*A Formally Verified Configuration for Hardware Security Modules in the Cloud*
by R. Focardi and F. L. Luccio
[ACM CCS 2021](https://www.sigsac.org/ccs/CCS2021/), November 2021.

- Conference proceedings version on [ACM Digital Library](https://dl.acm.org/doi/10.1145/3460120.3484785)
- Author's version on [arxiv](https://arxiv.org/abs/2109.13631).

## Model

Currently, we make available two versions of the model:

- Original [Tamarin prover model](https://github.com/secgroup/CloudHSM-model/blob/main/HSM_model_CCS_cameraready.spthy) from the CCS paper;
- Updated [Tamarin prover model](https://github.com/secgroup/CloudHSM-model/blob/main/HSM_model_CCS_updated.spthy) with the following improvements with respect to the original model:
	- We now use `K(...)` instead of `KU(...)` to model attacker knowledge in the three secrecy lemmas. `KU` is in fact Tamarin-internal. Lemmas are still proved automatically but the check is a bit slower (see below). Thanks to Cas Cremers for suggesting this fix.

## Prerequisites

To check the model you need to install the [Tamarin prover](https://tamarin-prover.github.io/)

## Usage

The reported execution times are on a MacBook pro 2018.

The full model can be checked with Tamarin as follows and it takes about `1m50s` (`1m30s` for the original model):

```bash
$ tamarin-prover --prove HSM_model_CCS_updated.spthy
```

Secrecy lemmas can be checked in about `1m` (`22s` for the original model):

```bash
$ tamarin-prover --prove=Secrecy* HSM_model_CCS_updated.spthy

```

The `Unwrap` helper lemma can be checked in about `1m04s`:

```bash
$ tamarin-prover --prove=Unwrap HSM_model_CCS_updated.spthy

```

