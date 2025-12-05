# Hush

Hush is a cross-platform noise-cancellation engine designed to give users control over the audio in the content they consume. 
It provides fast, modular tools for removing background music and filtering unwanted noise, powered by a high-performance C++ processing core and exposed through clean APIs, GHCR-hosted containers, and an intuitive Web UI. The system is built for efficiency and flexibility, making it easy for developers to integrate and for everyday users to clean up video or audio. Future updates will expand the engine with additional ML models, advanced DSP modules, and realtime processing to deliver an even more capable and customizable audio-filtering experience.

## Prerequisites

To get started with `Hush`, ensure that you have the following software installed on your system. These dependencies are necessary for running the backend server, compiling the C++ processor, and handling media files.

- **Python 3.9+**: Required for running the backend server.
- **FFmpeg**: For extracting, probing, and processing audio files.
- **CMake**: Needed to compile the C++ `MediaProcessor`.
- **nlohmann-json**: A JSON library required for parsing configuration files in the `MediaProcessor`.
- **libsndfile**: Required for sampled audio file operations in the `MediaProcessor`.
- **Docker and Docker Compose** (optional but recommended for a quick setup):

### Installation Commands

  **FFmpeg**:
  - **On Ubuntu/Debian**: 
    ```sh
    sudo apt update
    sudo apt install ffmpeg
    ```
  - **On macOS**:
    ```sh
    brew install ffmpeg
    ```

    After installing FFmpeg, ensure the correct path is set in the `config.json` file. By default, it is set to `/usr/bin/ffmpeg`. If you are using macOS and installed FFmpeg via Homebrew, update the path in `config.json` to:

    ```json
    "ffmpeg_path": "/opt/homebrew/bin/ffmpeg"
    ```

  **CMake**:
  - **On Ubuntu/Debian**: 
    ```sh
    sudo apt update
    sudo apt install cmake
    ```
  - **On macOS**:
    ```sh
    brew install cmake
    ```

  **nlohmann-json**:
  - **On Ubuntu/Debian**: 
    ```sh
    sudo apt update
    sudo apt install nlohmann-json3-dev
    ```
  - **On macOS**:
    ```sh
    brew install nlohmann-json
    ```

  **libsndfile**:
  - **On Ubuntu/Debian**: 
    ```sh
    sudo apt update
    sudo apt install libsndfile1-dev
    ```
  - **On macOS**:
    ```sh
    brew install libsndfile
    ```

  **Docker and Docker Compose**:
  - **On Ubuntu**:
    ```sh
    sudo apt install docker.io docker-compose
    ```
  - **On macOS**:
    ```sh
    brew install docker
    brew install docker-compose
    ```
## Getting Started
Follow these steps to set up `Hush` manually.

#### Step 1: Ensure Dependencies Are Installed

Ensure all dependencies mentioned in the [Prerequisites](#prerequisites) section are installed before proceeding.

#### Step 2: Install Python Dependencies

Install the Python dependencies with:
```sh
pip install -r requirements.txt
```
#### Step 3: Compile the Media Processor

1. Navigate to the `MediaProcessor` directory:
```sh
cd MediaProcessor
```

2. Make a build directory and navigate into it:

```sh
mkdir build
cd build
```
3. Run CMake and compile (release build by default)
```sh
cmake ..
make
```
#### Step 4: Start the Backend Server

After setting up the dependencies and compiling the C++ project, **navigate back to the project root** and start the backend server:
```sh
python3 app.py 
```

The server should be accessible at http://127.0.0.1:8080. Open this address in a web browser to get started.
