# 2D Image Convolution on FPGA PYNQ-Z2

This repository implements and compares 2D image convolution on different hardware platforms:

- **FPGA acceleration on PYNQ-Z2** using a custom overlay
- **ARM CPU execution on the PYNQ-Z2 board**
- **Laptop/PC CPU execution**
- **Laptop/PC CPU execution with OpenCV**

The goal of the project is to demonstrate how image convolution can be accelerated on FPGA hardware and to compare the performance against CPU-based implementations.

## Repository Contents

```text
.
├── input/                              # Input images used for convolution tests
├── (tested in laptop)-cpu.ipynb         # CPU implementation tested on laptop/PC
├── (tested in laptop)-cpu-opencv.ipynb  # OpenCV-based CPU implementation tested on laptop/PC
├── testeed in PYNQ-cpu.ipynb            # CPU implementation tested on PYNQ-Z2 ARM processor
├── testeed in PYNQ-FPGA.ipynb           # FPGA implementation tested on PYNQ-Z2
├── conv2d_pynq_overlay.bit              # FPGA bitstream overlay file
├── conv2d_pynq_overlay.hwh              # Hardware handoff file for the overlay
├── LICENSE
└── README.md
```

> **Note:** Some notebook filenames in the repository use the word `testeed`. Keep the filenames unchanged unless you also update the corresponding references in your workflow.

## Hardware and Software Requirements

### For FPGA Execution

- PYNQ-Z2 development board
- PYNQ image installed on the board
- Jupyter Notebook environment on PYNQ
- Python 3
- Required Python packages available in the PYNQ environment, such as:
  - `numpy`
  - `matplotlib`
  - `PIL` / `Pillow`
  - `pynq`

### For Laptop/PC CPU Execution

- Python 3
- Jupyter Notebook or JupyterLab
- Recommended Python packages:
  - `numpy`
  - `matplotlib`
  - `Pillow`
  - `opencv-python` for the OpenCV notebook

Install common dependencies with:

```bash
pip install numpy matplotlib pillow opencv-python jupyter
```

## Important PYNQ-Z2 Overlay Requirement

To run the FPGA implementation on the PYNQ-Z2 board, the two overlay files must be located in the **same directory as the main FPGA notebook/code file**:

```text
conv2d_pynq_overlay.bit
conv2d_pynq_overlay.hwh
```

For example, if you run:

```text
testeed in PYNQ-FPGA.ipynb
```

then both overlay files must be placed beside that notebook:

```text
.
├── testeed in PYNQ-FPGA.ipynb
├── conv2d_pynq_overlay.bit
└── conv2d_pynq_overlay.hwh
```

The `.bit` file configures the FPGA fabric, while the `.hwh` file provides the hardware metadata required by PYNQ to correctly communicate with the overlay.

## How to Run on PYNQ-Z2 FPGA

1. Clone or download this repository.

2. Copy the project folder to the PYNQ-Z2 board. For example, you can upload the files through the PYNQ Jupyter web interface.

3. Make sure the following files are in the same folder:

   ```text
   testeed in PYNQ-FPGA.ipynb
   conv2d_pynq_overlay.bit
   conv2d_pynq_overlay.hwh
   input/
   ```

4. Open the PYNQ Jupyter Notebook interface in your browser.

5. Open:

   ```text
   testeed in PYNQ-FPGA.ipynb
   ```

6. Run the notebook cells in order.

7. The notebook loads the FPGA overlay and performs 2D image convolution using the hardware accelerator.

## How to Run CPU Versions

### Laptop/PC CPU

Open and run:

```text
(tested in laptop)-cpu.ipynb
```

This notebook runs the convolution algorithm on a laptop or desktop CPU.

### Laptop/PC CPU with OpenCV

Open and run:

```text
(tested in laptop)-cpu-opencv.ipynb
```

This notebook uses OpenCV for convolution/image filtering and can be used as a reference implementation.

### PYNQ-Z2 ARM CPU

Open and run:

```text
testeed in PYNQ-cpu.ipynb
```

This notebook runs the convolution algorithm on the ARM processor of the PYNQ-Z2 board, without using FPGA acceleration.

## Project Workflow

The project compares 2D convolution across three execution environments:

1. **PC/Laptop CPU**  
   A baseline software implementation running on a standard computer.

2. **PYNQ-Z2 ARM CPU**  
   A software implementation running on the embedded ARM processor of the PYNQ-Z2.

3. **PYNQ-Z2 FPGA Overlay**  
   A hardware-accelerated implementation using a custom FPGA overlay.

This allows direct comparison between general-purpose CPU processing and FPGA-based acceleration for image convolution.

## Input Images

Input images are stored in the `input/` directory. Make sure this folder is available in the same relative path expected by the notebooks before running the code.

## Expected Output

The notebooks perform convolution on input images and display or save the processed results. Depending on the notebook, the output may include:

- Original input image
- Convolved/filtered output image
- Execution time
- Performance comparison between CPU and FPGA implementations

## Notes

- The FPGA notebook requires the overlay files to be present beside the main code/notebook file.
- The provided overlay is intended for the PYNQ-Z2 board.
- If the overlay files are missing or placed in another directory, PYNQ will not be able to load the FPGA design correctly.
- The hardware design may need to be regenerated if you use a different FPGA board or a different PYNQ image version.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
