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

## Contribution
| **Contribution**                          | **Description**                                                                                                                                                                                                                                                                                                                  |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Planet Imagery Download Script**        | I restructured the code to enhance readability and efficiency by eliminating redundancy and simplifying key functions. This included consolidating similar code blocks and optimizing logic to minimize repetition, thus improving overall organization. I also added some libraries like `datetime` to streamline and summarize code. Additionally, I added detailed comments for user guidance, and mentioned helper notebooks to further elucidate the code's functionality. [Code Link]() |
| **Apply NDWI Sliding Window**             | Implemented a sliding window approach to segment images, replacing the single global threshold method. This technique involves applying multiple overlapping windows (10 to 30 per pixel) across the image, providing a finer resolution of water and land classification. [Code Link]()                                                                                          |
| **Skip Invalid Sliding Windows**          | Some sliding windows, most of which are outside the NDWI image, are skipped to solve this problem. [Code Link]()                                                                                                                                                                                                                              |
| **Majority Sliding Window Classification** | Utilized a majority-based classification system where each pixel’s classification as water or land is determined by the majority of sliding windows overlapping that pixel. This method improves classification accuracy by reducing the impact of isolated threshold anomalies. [Code Link]()                                                           |
| **Gaussian Smoothing (Optional)**         | Incorporated Gaussian filtering before NDWI calculation to smooth the image and reduce noise. This step is optional, allowing users to choose whether to apply it based on the quality of the input data. Gaussian smoothing enhances the reliability of water body detection by mitigating noise effects. [Code Link]()                                     |
| **Concatenation of Sliding Window and Mean Threshold Images** | Combined the results from the sliding window classification with a mean threshold image. The sliding window technique classifies only the pixels within each window, leaving other parts of the image unclassified. To address this, unclassified regions are filled by merging the sliding window output with a mean threshold-based classification, ensuring that all image areas are covered and improving overall segmentation accuracy. [Code Link]() |


