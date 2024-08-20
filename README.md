![GSoC logo](https://developers.google.com/open-source/gsoc/resources/downloads/GSoC-logo-horizontal.svg)

# GSoC - Final Report

## Project
### **Title:** Automated Coastline Extraction for Erosion Modeling in Alaska  
### **Mentor:** Frank Witmer


## Basic Info
| Info             | Details                                  |
|------------------|------------------------------------------|
| **Name**         | Rawan Mohammed Elframawy                 |
| **Email**        | [rawann.elframawy@gmail.com](mailto:rawann.elframawy@gmail.com) |
| **GitLab Username** | [rawann31](https://gitlab.com/rawann31) |
| **LinkedIn**     | [rawann31](https://www.linkedin.com/in/rawann31) |
| **University**   | Nile University                          |
| **Organization** | Alaska                                   |


## Background
My name is Rawan, and I recently graduated with a degree in Computer Science, specializing in Artificial Intelligence. I have a solid foundation in Deep Learning and Remote Sensing data, which I am eager to apply to real-world challenges. My passion lies in bridging the gap between research and practical coding, and I am excited to contribute to open-source projects through Google Summer of Code. This is my first experience with GSoC, and I am enthusiastic about the opportunity to collaborate with the global developer community and enhance my skills in a meaningful way.


## Project Overview
![Project Overview](./images/project_overview.png)

The primary goal of my Google Summer of Code project is to enhance the accuracy of coastline extraction, particularly for erosion modeling in Deering, Alaska, using high-resolution Planet imagery with a 3-meter resolution. The project focuses on creating reliable ground truth data and labels that will be used to train the DeepWaterMap algorithm, a deep convolutional neural network designed to segment surface water on multispectral imagery. Originally trained on 30-meter resolution Landsat data, DeepWaterMap will be adapted to work with higher-resolution data in this project.

One of the key challenges in coastline extraction is the application of the Normalized Difference Water Index (NDWI), a widely used remote sensing index for identifying water bodies. However, using a single threshold across an entire image often results in suboptimal accuracy. To address this, I implemented a sliding window approach combined with Otsu thresholding, which dynamically adjusts thresholds over localized regions of the image. This method has shown promising improvements in accuracy.

The newly generated labeled data, derived from this approach, will be used to retrain the DeepWaterMap algorithm, replacing the original Global Surface Water data. This project aims to produce a more accurate and reliable tool for coastline detection, which is crucial for monitoring and mitigating coastal erosion in vulnerable areas like Alaska.

