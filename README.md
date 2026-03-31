# Card Symbol Recognition using OpenCV

## Overview

This project focuses on identifying matching playing cards from a set of images using computer vision techniques.

The input consists of:

* One image containing **two cards**
* Six option images containing **individual cards**

The goal is to detect which two option cards match the ones in the main image.

---

## Motivation

This project started as an attempt to solve an image-matching problem under ideal conditions.
However, as the images became more complex (noise, distortions, background interference), simple approaches stopped working.

This repository documents the **full trial-and-error journey** of improving the solution step by step.

---

## What’s Inside

This notebook intentionally includes multiple approaches:

### 1. Template Matching

* Used `cv2.matchTemplate`
* Worked initially but failed with noisy images

### 2. Structural Similarity (SSIM)

* Compared overall image similarity
* Sensitive to distortions and alignment

### 3. ORB Feature Matching

* Detected keypoints and descriptors
* Improved robustness but inconsistent results

### 4. Histogram & Color Matching

* Compared color distributions
* Not reliable for symbol-level matching

### 5. Area-Based Methods

* Compared pixel areas after thresholding
* Failed due to scaling and noise variations

### 6. Patch-Based Matching

* Focused on top-left card regions
* Partial improvement but still fragile

---

## Final Approach: Contour-Based Matching ✅

The final working solution is based on **contour detection and shape analysis**:

### Steps:

1. Preprocess image:

   * Convert to grayscale
   * Apply Gaussian blur
   * Threshold to isolate symbols

2. Extract contours:

   * Filter out noise using area threshold

3. Compute features:

   * Contour area
   * Circularity (shape descriptor)

4. Build a "card signature":

   * Number of symbols
   * Mean area
   * Mean circularity

5. Compare cards:

   * Match option cards based on closest signature

---

## Why This Works

* Focuses on **shape instead of raw pixels**
* More robust to:

  * Noise
  * Background changes
  * Minor distortions

---

## Tech Stack

* Python
* OpenCV
* NumPy

---

## Note

This notebook is intentionally kept **unfiltered and experimental** to show the full development process, including failed approaches and iterations.

---

## Future Improvements

* Better contour filtering
* Machine learning-based classification
* Handling rotations and perspective distortions more robustly

---

## Author
Khan Juned 
https://github.com/junedkhan9310

Built as a hands-on exploration of practical computer vision problem solving.
