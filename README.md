![GSoC logo](https://developers.google.com/open-source/gsoc/resources/downloads/GSoC-logo-horizontal.svg)

# GSoC - Final Report

## Project
### **Title:** Automated Coastline Extraction for Erosion Modeling  
### **Mentor:** Frank Witmer

## Basic Info
| **Info**              | **Details**                                  |
|-----------------------|----------------------------------------------|
| **Name**              | Rawan Mohammed Elframawy                     |
| **Email**             | [rawann.elframawy@gmail.com](mailto:rawann.elframawy@gmail.com) |
| **GitLab Username**   | [rawann31](https://gitlab.com/rawann31)     |
| **LinkedIn**          | [rawann31](https://www.linkedin.com/in/rawann31) |
| **University**        | Nile University                              |
| **Organization**      | Alaska                                       |

## Background
My name is Rawan, and I recently graduated with a degree in Computer Science, specializing in Artificial Intelligence. I have a solid foundation in Deep Learning and Remote Sensing data, which I am eager to apply to real-world challenges. My passion lies in bridging the gap between research and practical coding, and I am excited to contribute to open-source projects through Google Summer of Code. This is my first experience with GSoC, and I am enthusiastic about the opportunity to collaborate with the global developer community and enhance my skills in a meaningful way.

## Project Overview
![Project Overview](./images/project_overview.png)

The primary goal of my Google Summer of Code project is to enhance the accuracy of coastline extraction, particularly for erosion modeling in Deering, Alaska, using high-resolution Planet imagery with a 3-meter resolution. The project focuses on creating reliable ground truth data and labels that will be used to train the [DeepWaterMap algorithm](https://github.com/isikdogan/deepwatermap), a deep convolutional neural network designed to segment surface water on multispectral imagery. Originally trained on 30-meter resolution Landsat data, DeepWaterMap will be adapted to work with higher-resolution data in this project.

One of the key challenges in coastline extraction is the application of the Normalized Difference Water Index (NDWI), a widely used remote sensing index for identifying water bodies. However, using a single threshold across an entire image often results in suboptimal accuracy. To address this, I implemented a sliding window approach combined with Otsu thresholding, which dynamically adjusts thresholds over localized regions of the image. This method has shown promising improvements in accuracy.

The newly generated labeled data, derived from this approach, will be used to retrain the [DeepWaterMap algorithm](https://github.com/isikdogan/deepwatermap), replacing the original Global Surface Water data. This project aims to produce a more accurate and reliable tool for coastline detection, which is crucial for monitoring and mitigating coastal erosion in vulnerable areas like Alaska.



## Contribution (What I did)

| **Contribution**                          | **Description**                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Planet Imagery Download Script**        | I restructured the code to enhance readability and efficiency. This included consolidating similar code blocks, optimizing logic to minimize repetition, and adding libraries like `datetime` to streamline and summarize code. Detailed comments and helper notebooks were also included for better user guidance. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/DeeringAutoDownloadCode.py) |
| **Apply NDWI Sliding Window**             | Implemented a sliding window approach to segment images, replacing the single global threshold method. This technique involves using multiple overlapping windows (10 to 30 per pixel) to achieve finer water and land classification. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/ndwi_labels.py)                                                                                       |
| **Skip Invalid Sliding Windows**          | Skipped some sliding windows, particularly those outside the NDWI image, to resolve issues related to invalid windows as this extremely affect th mean threshold for the image. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/ndwi_labels.py)                                                                                                                                                                                                                                    |
| **Majority Sliding Window Classification** | Developed a majority-based classification system where each pixel’s classification is determined by the majority of overlapping sliding windows. This approach enhances classification accuracy by reducing the impact of isolated threshold anomalies. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/ndwi_labels.py)                                                                                                    |
| **Gaussian Smoothing (Optional)**         | Incorporated optional Gaussian filtering before NDWI calculation to smooth the image and reduce noise. This step improves water body detection by mitigating noise effects, allowing users to apply it based on input data quality. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/ndwi_labels.py)                                                                                                              |
| **Concatenation of Sliding Window and Mean Threshold Images** | Merged results from sliding window classification with a mean threshold image. This approach addresses unclassified regions by combining sliding window outputs with mean threshold-based classification, ensuring comprehensive segmentation and improved accuracy. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/ndwi_labels.py)                                                          |
| **Rewrite the RMSE Code**                                                                      | In the second version that I made, the RMSE calculation was streamlined by centralizing it in the `calc_transects_rmse` function, improving readability. The code now utilizes list comprehensions and `itertuples()` for more efficient distance calculations and consolidates CRS reprojecting and shapefile loading. Additionally, region-based RMSE calculations are handled directly in the main script, reducing redundancy and enhancing clarity. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/rmse.py) |
| **Upgrade Global Surface Water Mapping from V3 to V4 and a Function to Download It to Disk** | I upgraded the version of GSW from version 3 to version 4. I used the `geemap` library to download images to disk. [View Code](https://github.com/fwitmer/CoastlineExtraction/blob/dev/gsw_monthly_labels.py)    |

## Downloding Script Flow:
<p align="center">
  <img src="./images/download_flow.jpg" alt="Downloading Script Flow" width="700"/>
</p>


## Processing Steps

| **1. Read the Planet Image** | **2. Calculate NDWI** |
|------------------------------|-----------------------|
| ![RGB Image](./images/image_rgb.png) | ![NDWI Image](./images/image_ndwi.png) |

| **3. Make Buffer Around Each Point** | **4. Skip Buffers Most of It Outside the Image** |
|--------------------------------------|-----------------------------------------------|
| ![Buffers Image](./images/image_buffers.png) | ![Skipped Buffers Image](./images/image_skipped_buffers.png) |

| **5. Calculate the Threshold Using Otsu** | **6. Repeat This Step for All Sliding Windows** |
|------------------------------|-----------------------|
| ![RGB Image](./images/image_labelled_image.png) | ![NDWI Image](./images/image_all_sliding_windows_labelled.png) |

| **7. Label Unsegmented Pixels from NDWI with one threshold** |
|---------------------------------|
<p align="center">
  <img src="./images/image_all_sliding_windows_labelled.png" alt="NDWI Sliding Window" width="330" style="display:inline-block; margin-right:0px;" />
  <img src="./images/image_ndwi_one_threshold.png" alt="NDWI One Threshold" width="330" style="display:inline-block; margin-right:0px;" />
  <img src="./images/ndwi_concatenated.png" alt="NDWI Concatenated" width="330" style="display:inline-block;" />
</p>


## Current State

The sliding window technique has significantly enhanced the accuracy of our image segmentation approach. This method provides a more accurate and robust way to segment images, outperforming both the Global Surface Water Mapping (GSW) approach and the single-threshold method. 

- **Root Mean Square Error (RMSE) for GSW**: 72.16
- **RMSE for Single-Threshold Method**: 19.744
- **RMSE for NDWI Sliding Window Technique**: 12.9

The NDWI sliding window technique has demonstrated superior performance, achieving the lowest RMSE and thereby providing the most accurate segmentation results.
| **RGB before** | **Segmented Image After** |
|------------------------------|-----------------------|
| ![RGB Image](./images/image_rgb.png) | ![Segmented Image After](./images/ndwi_concatenated.png) |


## Commits

| **Commit Name**                                                       | **Commit Link**                                          |
|-----------------------------------------------------------------------|----------------------------------------------------------|
| Replace `get_start`, `get_end`, `day_check` functions with `validate_and_compare_dates` function | [PR #16](https://github.com/fwitmer/CoastlineExtraction/pull/16) |
| Change Functions: `rem_winter`, `RE_format`, `PS_format`              | [PR #17](https://github.com/fwitmer/CoastlineExtraction/pull/17) |
| Update `date_sort` function                                           | [PR #18](https://github.com/fwitmer/CoastlineExtraction/pull/18) |
| Update to `merge_ids` function                                         | [PR #19](https://github.com/fwitmer/CoastlineExtraction/pull/19) |
| Adding additional imports, URLs, functions, enhance Documentation     | [PR #23](https://github.com/fwitmer/CoastlineExtraction/pull/23) |
| Update `ndwi_labels.py`, change the value of `clip` and `nodata` parameters | [PR #25](https://github.com/fwitmer/CoastlineExtraction/pull/25) |
| Update `ndwi_labels.py`, add comments and blurring function (Optional) | [PR #26](https://github.com/fwitmer/CoastlineExtraction/pull/26) |
| Standardized capitalization for named constants                       | [PR #28](https://github.com/fwitmer/CoastlineExtraction/pull/28) |
| Update `rmse.py`                                                      | [PR #29](https://github.com/fwitmer/CoastlineExtraction/pull/29) |
| Update GSW image collection & RMSE code                               | [PR #30](https://github.com/fwitmer/CoastlineExtraction/pull/30) |


## Future Work

Future work involves publishing our results in a research paper to share the advancements made in coastline extraction using the sliding window technique. Additionally, we plan to train the DeepWaterMap algorithm with the newly generated labels to assess its effectiveness. This step will help validate the improvements and further enhance the algorithm's performance.

## New Skills Learned

During GSoC 2024, I picked up some valuable new skills:

- **Open Source Contribution**: I learned to navigate open source projects, manage version control with GitHub.
- **GIS Tools and Techniques**: I gained hands-on experience with QGIS, enhancing my ability to analyze and visualize geographic data.


## Acknowledgments

I would like to extend my sincere gratitude to Professor Frank Witmer for his invaluable guidance, flexibility, and support throughout this project. His time and responsiveness have been greatly appreciated.

