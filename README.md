# Step-by-Step Implementation for Generating the Class Saliency Map and Defining Pseudo-Background and Anomalous Vectors

## 1. Generate the Class Saliency Map

To begin, we will apply morphological operations on the hyperspectral image (HSI) data to isolate anomalies and background regions.

### Morphological Operations
- **Morphological Closing**: This operation helps to remove small dark areas in the image.
- **Morphological Opening**: This operation helps to remove small bright areas in the image.

We will use a square structuring element for these operations.

## 2. Differential Map Calculation

Next, we compute the differential map \( X \) using the following formula:

\[
X = |U - V_o(U)| + |U - V_c(U)|
\]

Where:
- \( U \) is the original hyperspectral data.
- \( V_o(U) \) is the morphologically opened version of \( U \).
- \( V_c(U) \) is the morphologically closed version of \( U \).

This differential map highlights both dark and bright small regions, effectively creating a saliency map.

## 3. Define Pseudo-Background and Anomalous Vectors Using Coarse Search

Based on the differential map, we will determine regions for background and anomalies:

- **Pseudo-Background Vectors**: Regions identified in the HSI that appear large, connected, and relatively uniform.
- **Anomalous Vectors**: Smaller, isolated regions with significant contrast compared to the background.

### Vector Labeling
We will label each vector in the hyperspectral image accordingly:
- The training dataset \( D_{Trn} \) will contain vectors identified as background (label = 0).
- The testing dataset \( D_{Tst} \) will contain all vectors, combining background and anomalous samples (label = 1 for anomalies).

## 4. Data Preprocessing for Training and Testing

### Normalization
We will normalize the vectors to bring their values within a range of [0, 1].

### Separation of Vectors
Separate the vectors into:
- **Training Vectors**: Only background vectors.
- **Testing Vectors**: Both background and anomalous vectors based on the labels derived from the saliency map.

