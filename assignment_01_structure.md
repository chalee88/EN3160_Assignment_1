# EN3160 Assignment 01

## Student Details

- Name:
- Index Number:
- GitHub Profile:

## Introduction

- Brief overview of intensity transformations and neighborhood filtering.
- Summary of the images, methods, and comparisons used in this assignment.

---

## Question 01 - Piecewise Linear Intensity Transformation

### Objective

- Implement the intensity transformation shown in Fig. 1a.
- Apply it to the image shown in Fig. 1b.

### Method

- Define `intensity_transform(im, breakpoints)`.
- Use the given breakpoint example:
  - `(0, 0)`
  - `(50, 50)`
  - `(100, 150)`
  - `(150, 255)`
  - `(255, 255)`
- Experiment with different breakpoints.

### Results

- Plot of the intensity transformation.
- Original image.
- Transformed image.
- Side-by-side comparison.

### Discussion

- Explain how the selected breakpoints affect contrast and brightness.
- Comment on the visually pleasing output.

---

## Question 02 - Brain Proton Density Image Enhancement

### Objective

- Apply intensity transformations to the brain proton density image in Fig. 2.
- Accentuate white matter and gray matter separately.

### White Matter Enhancement

- Chosen transformation.
- Transformation plot.
- Resulting image.
- Interpretation.

### Gray Matter Enhancement

- Chosen transformation.
- Transformation plot.
- Resulting image.
- Interpretation.

### Discussion

- Compare how the transformations emphasize different tissue regions.

---

## Question 03 - Gamma Correction in L*a*b* Color Space

### Objective

- Apply gamma correction to the `L` plane of the image in Fig. 3.

### Method

- Convert image from RGB/BGR to `L*a*b*` color space.
- Extract the `L` plane.
- Apply gamma correction.
- Recombine the corrected `L` plane with `a` and `b` planes.
- Convert back to RGB/BGR.

### Gamma Value

- Selected gamma value:

### Results

- Original image.
- Gamma-corrected image.
- Histogram of original image.
- Histogram of corrected image.

### Discussion

- Explain the visual effect of the selected gamma value.
- Compare histogram changes before and after correction.

---

## Question 04 - Vibrance Enhancement Using Saturation Transformation

### Objective

- Increase image vibrance by transforming the saturation plane of the image in Fig. 4.

### Method

- Convert image to HSV color space.
- Split into hue, saturation, and value planes.
- Apply the transformation:

```text
f(x) = min(x + a * 128 * exp(-((x - 128)^2) / (2 * sigma^2)), 255)
```

- Use `sigma = 70`.
- Adjust `a` in `[0, 1]`.
- Recombine hue, transformed saturation, and value planes.

### Parameter Selection

- Selected `a` value:

### Results

- Hue plane.
- Saturation plane.
- Value plane.
- Intensity transformation plot.
- Original image.
- Vibrance-enhanced image.

### Discussion

- Explain how changing `a` affects vibrance.
- Comment on whether the result looks natural or over-saturated.

---

## Question 05 - Histogram Equalization From Scratch

### Objective

- Write a custom function for histogram equalization.
- Apply it to the image shown in Fig. 5.

### Method

- Compute the image histogram.
- Compute the cumulative distribution function.
- Normalize the mapping.
- Apply the equalization mapping to the image.

### Results

- Original image.
- Equalized image.
- Histogram before equalization.
- Histogram after equalization.

### Discussion

- Explain how histogram equalization changes image contrast.
- Compare the before and after histograms.

---

## Question 06 - Foreground-Only Histogram Equalization

### Objective

- Histogram-equalize only the foreground of the image in Fig. 6.

### Method

#### HSV Plane Separation

- Convert image to HSV.
- Display hue, saturation, and value planes in grayscale.

#### Foreground Mask Extraction

- Select the best plane for thresholding.
- Apply thresholding to extract the foreground mask.

#### Foreground Histogram Equalization

- Extract foreground using `cv.bitwise_and`.
- Compute the foreground histogram.
- Compute cumulative sum using `np.cumsum`.
- Apply histogram equalization formulas from the lecture slides.

#### Background Recombination

- Extract the background.
- Add the equalized foreground and background.

### Results

- Hue plane.
- Saturation plane.
- Value plane.
- Foreground mask.
- Original image.
- Result with histogram-equalized foreground.

### Discussion

- Explain why the selected HSV plane was suitable for thresholding.
- Discuss how foreground-only equalization differs from full-image equalization.

---

## Question 07 - Sobel Filtering

### Objective

- Compute image gradients using Sobel filtering on the image in Fig. 7.

### Part A - Sobel Filtering Using `filter2D`

- Define Sobel kernels.
- Apply `cv.filter2D`.
- Display gradient results.

### Part B - Custom Sobel Filtering

- Implement convolution manually.
- Apply Sobel kernels.
- Display gradient results.

### Part C - Separable Sobel Filtering

- Use the separable property:

```text
[[1, 0, -1],
 [2, 0, -2],
 [1, 0, -1]]
=
[[1],
 [2],
 [1]]
*
[1, 0, -1]
```

- Apply filtering in two stages.
- Display gradient results.

### Results

- Original image.
- Sobel result using `filter2D`.
- Sobel result using custom implementation.
- Sobel result using separable filtering.

### Discussion

- Compare the three implementations.
- Discuss similarities, differences, and computational efficiency.

---

## Question 08 - Image Zooming

### Objective

- Write a function to zoom images by a scale factor `s` in `(0, 10]`.
- Support nearest-neighbor and bilinear interpolation.

### Method

#### Zoom Function

- Function inputs:
  - image
  - scale factor `s`
  - interpolation method
- Function outputs:
  - zoomed image

#### Nearest-Neighbor Interpolation

- Explain pixel coordinate mapping.
- Apply to test images.

#### Bilinear Interpolation

- Explain weighted averaging of neighboring pixels.
- Apply to test images.

### Evaluation

- Scale up the given small images by a factor of 4.
- Compare with the original large images.
- Compute normalized sum of squared difference.

### Results

- Original large images.
- Given small images.
- Nearest-neighbor zoomed images.
- Bilinear zoomed images.
- Normalized SSD values.

### Discussion

- Compare visual quality and SSD values.
- Explain why bilinear interpolation usually appears smoother.

---

## Question 09 - Foreground Segmentation and Background Blur

### Objective

- Use grabCut to segment the flower image in Fig. 8.
- Blur the background while keeping the flower foreground sharp.

### Part A - GrabCut Segmentation

- Initialize grabCut.
- Generate segmentation mask.
- Extract foreground image.
- Extract background image.

### Part B - Background Blur Enhancement

- Apply strong blur to the background.
- Combine sharp foreground with blurred background.
- Display original and enhanced images side-by-side.

### Part C - Edge Darkness Explanation

- Explain why the background just beyond the edge of the flower appears dark.

### Results

- Final segmentation mask.
- Foreground image.
- Background image.
- Original image.
- Enhanced image with blurred background.

### Discussion

- Comment on segmentation quality.
- Discuss boundary artifacts and edge effects.

---

## Question 10 - Bilateral Filtering

### Objective

- Smooth the Lake Minaret image in Fig. 9 while preserving sharp edges.

### Part A - OpenCV Bilateral Filter

- Apply `cv.bilateralFilter`.
- Select spatial standard deviation `sigma_s`.
- Select range standard deviation `sigma_r`.
- Compare with Gaussian blur using a similar kernel.

### Part B - Custom Bilateral Filter

- Implement bilateral filtering manually.
- Compare the custom result with OpenCV's `bilateralFilter`.
- Use a quantitative measure for comparison.

### Parameters

- Selected `sigma_s`:
- Selected `sigma_r`:
- Gaussian kernel size:
- Quantitative metric:

### Results

- Original image.
- Gaussian blurred image.
- OpenCV bilateral filtered image.
- Custom bilateral filtered image.
- Quantitative comparison values.

### Discussion

- Explain how bilateral filtering preserves edges.
- Compare OpenCV and custom implementation results.
- Discuss runtime and quality differences.

---

## Conclusion

- Summarize key observations across all questions.
- Mention the most effective enhancement and filtering techniques.
- Reflect on limitations and possible improvements.

## References

- Assignment PDF.
- Lecture slides.
- OpenCV documentation.
- NumPy documentation.
- Any external image or algorithm references used.

## Submission Checklist

- PDF exported directly from Jupyter Notebook.
- File named `your_index_a01.pdf`.
- Maximum 10 pages.
- Index number and name included.
- GitHub profile link included.
- Key code snippets included.
- Representative results included.
- Comparisons and discussions included.
- Commits made regularly.
