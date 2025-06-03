# 🔐 Image Steganography Tool

A command-line steganography application that hides secret messages within images using the LSB (Least Significant Bit) technique. Developed as part of the Programming in C and C++ Languages (PJC) course at PJATK, Winter 2022/2023.

![c++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![cmake](https://img.shields.io/badge/CMake-064F8C?style=for-the-badge&logo=cmake&logoColor=white)
![steganography](https://img.shields.io/badge/Steganography-FF6B6B?style=for-the-badge&logo=shield&logoColor=white)

## 📋 Overview

This tool allows you to hide and extract secret messages within image files without visibly altering the image. It supports BMP and PPM image formats and uses a robust LSB steganography algorithm that modifies the two least significant bits of each color channel.

### 🌟 Key Features

- **Message Encryption** - Hide text messages within images
- **Message Decryption** - Extract hidden messages from images
- **Multi-format Support** - Works with BMP (24-bit) and PPM (ASCII) formats
- **Capacity Check** - Verify if your message fits in the image
- **Image Information** - Display detailed image metadata
- **ASCII Art UI** - Beautiful command-line interface with ASCII art
- **Error Handling** - Comprehensive error messages and validation

## 🎨 Supported Image Formats

|Format|Description|Extension|
|---|---|---|
|BMP|24-bit Bitmap images|`.bmp`|
|PPM|ASCII-encoded Portable PixMap|`.ppm`|

## 🏗️ Architecture

The project follows the MVC (Model-View-Controller) pattern:

### Core Components

- **Models**
    - `Image` - Abstract base class for image handling
    - `Bmp` - BMP format implementation
    - `Ppm` - PPM format implementation
    - `Message` - Steganography algorithm implementation
    - `Pixels` - Pixel manipulation utilities
- **Controllers**
    - `BaseController` - Main application controller
    - `FlagController` - Command-line flag parsing
    - `ArgumentController` - Command execution logic
- **View**
    - `CommandLineInterface` - User interface with ASCII art

## 🚀 Getting Started

### Prerequisites

- C++14 or higher
- CMake 3.23 or higher
- Command line interface

### Building the Project

1. Clone the repository:

bash

```bash
git clone https://github.com/yourusername/image-steganography-cpp.git
cd image-steganography-cpp
```

2. Create build directory and compile:

bash

```bash
mkdir build
cd build
cmake ..
make
```

Or use CMake directly:

bash

```bash
cmake -B build
cmake --build build
```

### Installation

After building, the executable will be in the `build` directory:

bash

```bash
./build/steganography
```

## 📝 Usage

### Command Syntax

bash

```bash
steganography [options] <path-to-image>
steganography [options] <path-to-image> "message-to-encrypt"
```

### Available Commands

|Flag|Long Form|Description|Example|
|---|---|---|---|
|`-h`|`--help`|Display help information|`steganography -h`|
|`-i`|`--info`|Show image information|`steganography -i image.bmp`|
|`-e`|`--encrypt`|Hide message in image|`steganography -e image.bmp "Secret message"`|
|`-d`|`--decrypt`|Extract message from image|`steganography -d image.bmp`|
|`-c`|`--check`|Check encryption capacity|`steganography -c image.bmp "Test message"`|

### Usage Examples

#### 1. Hide a Message

bash

```bash
steganography -e beach.bmp "This is my secret message!"
```

#### 2. Extract a Hidden Message

bash

```bash
steganography -d beach.bmp
```

#### 3. Check Image Information

bash

```bash
steganography -i beach.bmp
```

Output:

```
.------..------..------..------.
|I.--. ||N.--. ||F.--. ||O.--. |
| (\/) || :(): || :(): || :/\: |
| :\/: || ()() || ()() || :\/: |
| '--'I|| '--'N|| '--'F|| '--'O|
`------'`------'`------'`------'
File path: beach.bmp
File format: .bmp - 24 bit per pixel.
Image resolution: 1920 x 1080
Image size: 6220800 bytes
Last modification time: Tue Dec 20 15:30:00 2022
```

#### 4. Check Message Capacity

bash

```bash
steganography -c image.ppm "Can this message fit?"
```

## 🔧 How It Works

### LSB Steganography Algorithm

The tool uses the Least Significant Bit (LSB) technique to hide messages:

1. **Message Encoding**:
    - Prepends a "size" flag (4 bytes) and message length (4 bytes)
    - Converts the message to binary
    - Modifies the 2 least significant bits of each color channel (RGB)
    - Distributes bits across pixels to minimize visual impact
2. **Message Decoding**:
    - Reads the flag to verify an encoded message exists
    - Extracts the message length
    - Reconstructs the message from the modified bits

### Bit Distribution

Each pixel can store 6 bits of data (2 bits per color channel):

- Red channel: bits 0-1
- Blue channel: bits 2-3
- Green channel: bits 4-5

## 🛡️ Security Considerations

- Messages are not encrypted - only hidden
- No password protection
- Can be detected by steganalysis tools
- Original image is modified (though imperceptibly)

For sensitive data, consider encrypting your message before hiding it.

## 📊 Technical Details

### Maximum Message Capacity

The maximum message length (in bytes) is calculated as:

```
max_length = ((width × height × 3) - 64) ÷ 8
```

Where 64 bits are reserved for the header (flag + size).

### Performance

- Fast encoding/decoding (O(n) where n = number of pixels)
- Minimal memory footprint
- Supports large images (tested up to 4K resolution)

## 🧪 Testing

The tool includes comprehensive error handling for:

- Invalid file paths
- Unsupported formats
- Messages too large for the image
- Corrupted image files
- Missing encoded messages

## 📚 Academic Context

This project was developed as part of the Programming in C and C++ Languages (PJC) course at the Polish-Japanese Academy of Information Technology (PJATK) during the winter semester of 2022/2023.

### Learning Objectives

- Advanced C++ programming techniques
- File I/O and binary manipulation
- Image format parsing
- Command-line interface design
- Software architecture patterns (MVC)

## 🤝 Contributing

This is an academic project. Feel free to use it as a reference for learning, but please write your own implementation if you're working on a similar assignment.

## ⚠️ Disclaimer

This tool is for educational purposes only. Users are responsible for complying with applicable laws regarding privacy and data hiding in their jurisdiction.

## 📄 License

This project is part of academic coursework. Please refer to your institution's academic integrity policies before using this code.

## 👤 Author

**Krzysztof Przybysz**  
Student ID: s24825  
Course: Programming in C and C++ Languages (PJC)  
Semester: Winter 2022/2023

---

_Note: This is an educational implementation of steganography. For production use, consider established cryptographic libraries with proper security measures._