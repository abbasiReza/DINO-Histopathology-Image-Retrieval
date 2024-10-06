# DINO Histopathology Image Retrieval
<div align="center">
  <img width="100%" alt="DINO illustration" src="dino.gif">
</div>


This project implements an image retrieval system for histopathology images using the DINO self-supervised learning model. The goal is to retrieve similar histopathology images given a query image.

## Model

DINO is a vision transformer model trained in a self-supervised manner to learn useful visual representations from unlabeled images.

DINO uses a teacher-student training framework. The teacher and student models are instantiated from the same backbone CNN (such as ResNet). The teacher has access to more information to provide better target representations for the student to match. 

Specifically, the teacher model uses a momentum encoder along with otherwise identical architecture as the student. The momentum encoder accumulates information over time leading to improved representations.

This teacher-student framework allows DINO to learn more robust visual features from unlabeled data in a self-supervised manner.

In this project, a DINO model pre-trained on ImageNet is used as the image encoder. Images are passed through the model to generate DINO visual feature vectors. These features capture semantic information that can be used to effectively index and retrieve similar histopathology images. 

During training, the DINO model is fine-tuned on the histopathology datasets to adapt to this domain. The trained model is then used to encode the dataset images into the search index. At retrieval time, DINO features are extracted from query images and used to find the most similar database images.

## Datasets

The model is trained and evaluated on the following histopathology image datasets:

- [BracS](https://www.bracs.icar.cnr.it/) - Breast Cancer Histopathology Image Dataset
- [CRC](https://warwick.ac.uk/fac/cross\_fac/tia/data/extended\_crc\_grading/) - Colorectal Cancer Histopathology Images  
- [BATCH](https://iciar2018-challenge.grand-challenge.org/Dataset/) - BreAst Cancer Histology Challenge Dataset

## Usage 

The image retrieval system provides an interface to upload a query histology image. It then indexes through the dataset encodings to find the most similar images based on the DINO features. The top k retrieved images are returned, ranked by similarity.

The project provides code to train the DINO encoder as well as utilities to index and search the image datasets.

