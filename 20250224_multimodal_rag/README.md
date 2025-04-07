# Course
https://learn.deeplearning.ai/courses/building-multimodal-search-and-rag/lesson/ddx5y/overview-of-multimodality

# Learning points
## Overview of multimodality
1. The video focuses on non-native multimodal models.
    1. Use separate models for each modality. I.e. nomic for text, ViT for image etc. But they must have the same embedding dimension.
    1. Contrastive training is done to push similar embeddings together. I.e. embedding of picture of lion, and text "lion" will be pushed closer together, while text "fish" is pushed further away.
    1. The video showing the change of embeddings is quite useful. To consider setting up a similar checkpoint when training our own embeddings for stakeholders to understand.
    1. [edit after working with openclip] I think contrastive learning is not useful particuarly if there's a native multimodal embedding model available. The embeddings from contrastive learning are inferior.

## Multimodal search
1. The video focuses on how to do multimodal search.
    1. Not learning too much here. Just take time to practice using openclip for multimodal embeddings. 
    1. Did my own implementation end to end using openclip for embeddings, and chroma for vectordb.

## LMM
1. Focuses on using LMMs.
    1. Will take the chance to try out Qwen2.5-VL.
        1. I ran into some conceptual issues, that I did some research to figure out:
            1. Models that are multimodal but can only take 1 modality at a time are considered _Sequential Multimodal models_
            1. Models that are mutlimodal and can take mixture of modalities at once are considered _Joint Multimodal models/Fusion models_ (Qwen-VL, GPT-4V(ision), and BLIP-2.)
    1. Nothing much learnt here. Mostly learnt about visual finetuning, but definitely not indepth.
