## Overview
**CONVLORA AND ADABN BASED DOMAIN ADAPTATION VIA SELF-TRAINING**

  
The code repository for paper "ConvLoRA and AdaBN based DOMAIN ADAPTATION via SELF-TRAINING" accepted at [IEEE ISBI 2024](https://biomedicalimaging.org/2024/) in PyTorch.

## ConvLoRA

We propose Convolutional Low-Rank Adaptation (ConvLoRA), as an adaptation of Low-Rank Domain Adaptation (LoRA) in LLMs. ConvLoRA is specifically
designed for application in Convolutional Neural Networks (CNNs), presenting a novel approach to address domain adaptation challenges in the context of image data. Instead of creating dedicated fine-tuned models for multiple target domains, each with the same number of parameters as the base model, we inject several ConvLoRA adapters into the base model pre-trained on the source domain, and only adapt the ConvLoRA parameters, while keeping all other parameters. This method allows faster updates by adapting only a small set of domain specific parameters. 

<p align="center"><img width="60%" src="/imgs/uda_arch.png" /></p>

## Results

<p align="center"><img width="80%" src="/imgs/results.png" /></p>

## Dataset
## [CC359 ](https://www.ccdataset.com/home)
Calgary-Campinas (CC359) dataset is a multi-vendor (GE, Philips, Siemens), multi-field strength (1 5, 3) magnetic resonance (MR) T1-weighted volumetric brain imaging dataset. It has six different domains and contains 359 3D brain MR image volumes, primarily focused on the task of skull stripping. 


## Arguments

Following arguments are required to run the code. The details are in <main.py>

Task Related Arguments

```dataset:``` Option for the dataset, default to CC359

```site:``` Site in CC359 dataset

```step:``` Specifies stage of adaptation pipeline (base_model, refine, adapt)

```seed:``` Seed value for reproducibility

```test:``` Flag to activate inference


## Training scripts 
Training base model

```
python main.py --config ./config/baseline.json --data "cc359" --site 2 --step "base_model" --seed 1234 --wandb_mode "online" --suffix <"user defined">  

```

Training ESH model

```
python main.py --config ./config/feature_seg.json --data "cc359" --site 2 --step "feature_segmentor"  --seed 1234  --wandb_mode "online"  --suffix <"user defined"> 
```

Adaptation


```
python main.py --config ./config/refinment.json --data "cc359" --site 3  --step "adapt"  --seed 1234  --wandb_mode "online"  --suffix <"user defined">

```


## Inference

```
python main.py --config ./config/test_baseline.json --data "cc359" --site 3  --step "test" --seed 1234 ---wandb_mode "online" --suffix <"user defined"> --test test --adapt "lora" 


```


## Contact
Feel free to raise an issue or contact me at sidra.aleem2@mail.dcu.ie for queries and discussions.
