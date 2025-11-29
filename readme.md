# Hush

A high-performance audio noise cancellation engine written entirely in C++. It uses a hybrid approach, combining traditional Digital Signal Processing (DSP) techniques with a trained PyTorch Machine Learning model to intelligently remove background noise from audio files.

The system is designed for efficiency and real-time processing capabilities, making it a suitable core for applications requiring low-latency audio enhancement.

## Core Features

*   **Hybrid Processing:** Leverages a `denoiser_model.pt` (a TorchScript model exported from Python) to guide a DSP-based spectral subtraction algorithm.
*   **Intelligent Adaptation:** Analyzes audio in real-time to determine characteristics like Signal-to-Noise Ratio (SNR) and noise type, adapting its processing strategy accordingly.
*   **Frame-Based, Real-Time Capable:** Processes audio in small chunks with very low latency (~1-2 ms per frame), suitable for live audio streams.
*   **High Performance:** Built in C++ and linked against the LibTorch library for maximum computational efficiency.
*   **Modular Design:** Separates concerns into distinct modules for audio I/O, VAD, DSP, and ML processing.

## Dependencies

To build and run this project, you will need:
*   A C++17 compliant compiler (e.g., Clang, GCC)
*   CMake (version 3.15 or later)
*   **LibTorch:** The C++ distribution of PyTorch. [Download here](https://pytorch.org/get-started/locally/).
*   **libsndfile:** A library for reading and writing audio files.
    *   On macOS: `brew install libsndfile`
    *   On Debian/Ubuntu: `sudo apt-get install libsndfile1-dev`

## Build Instructions

1.  **Download and setup LibTorch**:
    Download LibTorch from the official PyTorch website. After extracting the archive:
    
    ```bash
    xattr -r -d com.apple.quarantine "/path/to/libtorch"
    ```

2.  **Configure `CMakeLists.txt`**:
    Open the `CMakeLists.txt` file and set the `CMAKE_PREFIX_PATH` variable to the absolute path of your unzipped LibTorch installation directory.
    ```cmake
    set(CMAKE_PREFIX_PATH "/path/to/your/libtorch")
    ```

3.  **Create a build directory**:
    ```bash
    mkdir build
    cd build
    ```

4.  **Generate the build system**:
    ```bash
    cmake ..
    ```

5.  **Compile the project**:
    ```bash
    make
    ```
    An executable named `HushMe` will be created inside the `build` directory.

## Usage

Run the executable from the **project root directory**, providing an input file and an output file as arguments.

```bash
# General Usage
./build/HushMe <path/to/input.wav> <path/to/output.wav>

# Example
./build/HushMe test_audio/noisy_white.wav enhanced_audio.wav
```


```shell
(base) ➜  build cd ..                                                                                   
./build/HushMe test_audio/noisy_white.wav final_enhanced_output.wav
Enhanced Noise Cancellation System
==================================================
Input file: test_audio/noisy_white.wav
Output file: final_enhanced_output.wav
Processing mode: balanced
ML model: denoiser_model.pt
==================================================
Loaded audio file: test_audio/noisy_white.wav (144000 samples, 48000 Hz)
ML model loaded successfully from: traced_denoiser_model.pt
Enhanced Noise Processor Initialized with Intelligence.
Processor initialized with 'balanced' mode.

Processing 280 frames with intelligent hybrid system...

Frame 0 analysis:
  SNR: 10.0 dB
  Noise type: broadband
  Strategy: balanced
  DSP weight: 0.30
  ML weight: 0.70
  Processing time: 22.88 ms

Frame 1 analysis:
  SNR: 0.6 dB
  Noise type: broadband
  Strategy: aggressive
  DSP weight: 0.50
  ML weight: 0.50
  Processing time: 0.53 ms

Frame 2 analysis:
  SNR: 1.1 dB
  Noise type: broadband
  Strategy: aggressive
  DSP weight: 0.50
  ML weight: 0.50
  Processing time: 0.50 ms
  - Processed frame 200/280 (71%) 

Processing completed in 848 ms.
Average processing time per frame: 3.03 ms

============================================================
INTELLIGENT PROCESSING ANALYSIS
============================================================
Performance Metrics:
  Average processing time: 1.23 ms per frame
  Average estimated SNR: 1.36 dB
  Average noise reduction: 25.87 dB
  Total frames processed: 280

Intelligent Fusion Analysis:
  Average DSP weight: 0.46
  Average ML weight: 0.54

Strategy Distribution:
  aggressive: 279 frames (99.64%)
  balanced: 1 frames (0.36%)

Noise Type Distribution:
  broadband: 267 frames (95.36%)
  mixed: 13 frames (4.64%)
============================================================

Enhanced audio saved to: final_enhanced_output.wav
Detailed metrics saved to: final_enhanced_output_metrics.json

Performance Assessment:
Real-time capable (< 10ms per frame)
Adaptive strategy selection active
Multiple noise types detected

Processing complete!
Files generated:
  - Enhanced audio: final_enhanced_output.wav
  - Processing metrics: final_enhanced_output_metrics.json

```

The system will process the input audio and save the enhanced version to the specified output path.

---
I ported the core intelligence from the Python prototype to a high-performance, real-time capable C++ application.


