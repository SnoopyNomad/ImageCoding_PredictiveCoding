# Predictive Coding for Image Compression

This project implements predictive coding algorithms for image compression, comparing lossless and lossy approaches. The implementation processes an X-ray image and evaluates the compression performance using Signal-to-Noise Ratio (SNR) metrics.

## Overview

Predictive coding is a technique used in image compression that predicts pixel values based on neighboring pixels and encodes only the prediction error (residual). This approach exploits spatial redundancy in images to achieve compression.

## Features

- **Lossless Predictive Coding**: Preserves all image information by encoding exact prediction errors
- **Lossy Predictive Coding**: Uses quantization to reduce data size while maintaining acceptable image quality
- **SNR Analysis**: Compares the performance of both methods using Signal-to-Noise Ratio calculations

## Algorithm Details

### Lossless Predictive Coding

- Uses a simple predictor: `predicted_value = (pixel_right + pixel_below) / 2`
- Encodes the exact prediction error: `error = actual_value - predicted_value`
- No information loss - perfect reconstruction possible

### Lossy Predictive Coding

- Uses an adaptive predictor that chooses between:
  - Horizontal prediction: `predicted_value = pixel_left`
  - Vertical prediction: `predicted_value = pixel_above`
- Selection is based on which direction has smaller gradient
- Quantizes the prediction error using a 6-level quantizer:
  - Error ranges: `[-∞, -40/255]`, `[-40/255, -10/255]`, `[-10/255, 0]`, `[0, 10/255]`, `[10/255, 40/255]`, `[40/255, +∞]`
  - Quantized values: `-64/255`, `-16/255`, `-4/255`, `4/255`, `16/255`, `64/255`

## Requirements

- Python 3.x
- NumPy
- Matplotlib

## Installation

```bash
pip install numpy matplotlib
```

## Usage

1. Ensure `x-ray.png` is in the same directory as the notebook
2. Open `PredictiveCoding.ipynb` in Jupyter Notebook or JupyterLab
3. Run all cells sequentially

## Output

The notebook generates several visualizations:

1. **Original Image**: Displays the input X-ray image and its histogram
2. **Lossless Results**: Shows the prediction image and error histogram
3. **Lossy Results**: Shows the quantized prediction image and error histogram
4. **SNR Comparison**: Prints Signal-to-Noise Ratio for both methods

### Expected Results

- **SNR Lossless**: ~79.59 dB (higher is better, lossless has perfect reconstruction)
- **SNR Lossy**: ~65.73 dB (lower due to quantization, but still acceptable quality)

## File Structure

```
ImageCoding_PredictiveCoding/
├── PredictiveCoding.ipynb    # Main notebook with implementation
├── x-ray.png                  # Input image
└── README.md                  # This file
```

## Notes

- The lossless method provides perfect reconstruction but requires storing all prediction errors
- The lossy method achieves better compression at the cost of some image quality
- SNR values may vary slightly depending on the input image characteristics

## References

Predictive coding is a fundamental technique in image compression, used in standards like JPEG-LS and as a component in more complex codecs.

