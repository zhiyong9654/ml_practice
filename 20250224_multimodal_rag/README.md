# Course
https://learn.deeplearning.ai/courses/building-multimodal-search-and-rag/lesson/ddx5y/overview-of-multimodality

# Learning points
## Overview of multimodality
1. The video focuses on non-native multimodal models.
    1. Use separate models for each modality. I.e. nomic for text, ViT for image etc. But they must have the same embedding dimension.
    1. Contrastive training is done to push similar embeddings together. I.e. embedding of picture of lion, and text "lion" will be pushed closer together, while text "fish" is pushed further away.
