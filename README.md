# MAAE: Mask-Guided Attention-Based Semantic Guidance for Text-to-Image Diffusion Models

## Description
This work is built upon Attend-and-Excite:[Attention-Based Semantic Guidance for Text-to-Image Diffusion Models (SIGGRAPH 2023)](https://yuval-alaluf.github.io/Attend-and-Excite/).

Research question: How can we enable soft conditions on multiple objects layout in stable diffusion?

• Built a new algorithm upon Attend and Excite (Attention-Based Semantic Guidance for Diffusion Models)

• Deployed a new loss function, directly regulating attention maps by input masks at the inference stage

• The new architecture can generate images guided by multi-object prompts and follow the mask layout


## Method
We provide addtional binary mask input for selected key tokens of the prompt. The instinct is to regulize the attention map of each token as close to the mask as possible.
Here is how we construct our new loss function:

1.We want to maximize the values inside the mask (we call the matrix keeping only these values Inner), 
and also minimize the values outside of the mask (we call the matrix keeping only these values Outer).

<img width="1000" alt="Screen Shot 2023-12-03 at 5 46 10 PM" src="https://github.com/KolvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/4478aded-07e5-48bc-b513-7e6427640737">
lvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/e8de7d61-eb21-468a-827c-7dc0af8be26f">

To compute this, for each attention map, we compute the Diff matrix = Inner-Outer, and try to minimize value: mean (Diff) in our loss function 

2.Also, we want to make sure the attention map also regulated by the edge of the masks. 
To do this, we compute the edge matrix of each attention map:

<img width="700" alt="Screen Shot 2023-12-03 at 5 51 58 PM" src="https://github.com/KolvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/15744d07-6b61-40a7-b3f4-aa4536e1c28d">

In our loss function, we also try to maximize the edge matrix, by minimizing value: -sum (edge matrix).

Putting together, our loss function would be:

<img width="800" alt="Screen Shot 2023-12-03 at 6 05 54 PM" src="https://github.com/KolvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/eab80a0b-2a0e-4df6-8642-b43e78d07cf6">

notice that in real implementation, the edge part of the loss function can be eliminated, given the situation whether edge regularization is important in specific tasks.
α is a hyperparameter that is usually 100.

## Full architecture overview


MAAE overview: 

<img width="500" alt="Screen Shot 2023-12-03 at 5 28 22 PM" src="https://github.com/KolvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/a1bc78cf-a849-418d-b7d5-d3fec34b3a48">


In comparison, original AAE overview from paper:

<img width="500" alt="Screen Shot 2023-12-03 at 5 27 07 PM" src="https://github.com/KolvacS-W/Mask-Guided-Attention-Semantic-Guidance-for-Text-to-Image-Diffusion-Models/assets/55591358/0bdb2490-fe1c-4842-90d6-67f8a92332ad">


