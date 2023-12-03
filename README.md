# MAAE: Mask-Guided Attention-Based Semantic Guidance for Text-to-Image Diffusion Models

## Description
This work is built upon Attend-and-Excite: Attention-Based Semantic Guidance for Text-to-Image Diffusion Models (SIGGRAPH 2023).

Research question: How can we enable soft conditions on multiple objects layout in stable diffusion?

• Built a new algorithm upon Attend and Excite (Attention-Based Semantic Guidance for Diffusion Models)

• Deployed a new loss function, directly regulating attention maps by input masks at the inference stage

• The new architecture can generate images guided by multi-object prompts and follow the mask layout


## Method


## Detail Implementation

original AAE overview from paper:

<img width="500" alt="Screen Shot 2023-12-03 at 5 27 07 PM" src="https://github.com/KolvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/0bdb2490-fe1c-4842-90d6-67f8a92332ad">


MAAE overview: 

<img width="500" alt="Screen Shot 2023-12-03 at 5 28 22 PM" src="https://github.com/KolvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/a1bc78cf-a849-418d-b7d5-d3fec34b3a48">

