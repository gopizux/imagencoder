# Secret Image Encoder

A client-side steganography tool that allows users to hide secret messages within images using the Least Significant Bit (LSB) technique. All processing occurs locally in the browser, ensuring complete privacy and security.

## Overview

Secret Image Encoder is a web-based application that implements digital steganography - the practice of concealing information within other non-secret data. This tool specifically uses image steganography to embed text messages into digital images without any visually detectable changes.

## Features

### Core Functionality
- **Message Encoding**: Hide text messages within PNG, JPEG, and other image formats
- **Message Decoding**: Extract hidden messages from encoded images
- **Client-Side Processing**: All operations performed locally in the browser
- **Zero Data Retention**: No server uploads or data storage
- **Visual Preservation**: Encoded images appear identical to originals

### Technical Features
- LSB (Least Significant Bit) steganography implementation
- Binary message encoding with null terminator for accurate extraction
- Support for various image formats
- Automatic capacity checking to prevent message overflow
- Real-time image preview and comparison

## How It Works

### The LSB Steganography Method

The application uses the Least Significant Bit technique, which works as follows:

1. **Pixel Structure**: Each pixel in an image contains RGB (Red, Green, Blue) color values, each ranging from 0-255 (8 bits)

2. **Bit Manipulation**: The algorithm modifies only the least significant bit of each color channel, causing minimal visual change

3. **Message Encoding Process**:
   - Convert the text message to binary format
   - Iterate through image pixels sequentially
   - Replace the LSB of each color channel with message bits
   - Add a null terminator to mark message end

4. **Message Decoding Process**:
   - Extract LSBs from each color channel
   - Reconstruct the binary message
   - Convert binary back to text
   - Stop at null terminator

### Capacity Calculation

The maximum message capacity depends on image dimensions:
```
Maximum characters = (Width × Height × 3) / 8
```
For example, a 1024×768 image can store approximately 294,912 characters.

## Installation

### Direct Usage
Simply open the HTML file in any modern web browser. No installation or server setup required.

```bash
# Clone the repository
git clone https://github.com/yourusername/secret-image-encoder.git

# Navigate to the project directory
cd secret-image-encoder

# Open in browser
open index.html
```

### Hosting
The application can be hosted on any static web server or platform:
- GitHub Pages
- Netlify
- Vercel
- AWS S3
- Any traditional web server

## Usage Guide

### Hiding a Message

1. Navigate to the "Hide Message" tab
2. Click "Choose Cover Image" and select your image
3. Enter your secret message in the text area
4. Click "Hide Message in Image"
5. Download the encoded image using the download button

### Revealing a Message

1. Navigate to the "Reveal Message" tab
2. Click "Upload Encoded Image" and select the encoded image
3. Click "Reveal Hidden Message"
4. The hidden message will be displayed in the text area

## Technical Specifications

### Dependencies
- Bootstrap 5.3.0 (UI Framework)
- Font Awesome 6.4.0 (Icons)
- Vanilla JavaScript (Core functionality)

### Browser Compatibility
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

### File Support
- **Input Formats**: PNG, JPEG, GIF, BMP, WebP
- **Output Format**: PNG (to preserve data integrity)

## Security Considerations

### Privacy Features
- **Local Processing**: All steganography operations occur client-side
- **No External Communication**: No API calls or server requests
- **No Cookies/Tracking**: No user data collection
- **No Dependencies on External Services**: Fully self-contained

### Limitations
- The encoded message is not encrypted - consider encrypting sensitive data before encoding
- Image compression or format conversion may destroy hidden data
- Social media platforms may compress images, potentially losing embedded messages
- Best results with PNG format due to lossless compression

## Implementation Details

### Core Algorithm Structure

```javascript
// Message to Binary Conversion
textToBinary(text) {
    return text.split('').map(char => 
        char.charCodeAt(0).toString(2).padStart(8, '0')
    ).join('');
}

// LSB Embedding
encode(imageData, message) {
    const binaryMessage = textToBinary(message + '\0');
    // Modify LSBs of RGB channels
    for each pixel:
        for each color channel (R, G, B):
            channel_value = (channel_value & 0xFE) | message_bit
}
```

### Performance Optimization
- Efficient bit manipulation using bitwise operators
- Minimal memory footprint with in-place modifications
- Streamlined canvas operations for image handling

## Use Cases

- **Secure Communication**: Exchange sensitive information discretely
- **Digital Watermarking**: Embed copyright or ownership information
- **Authentication**: Hide verification codes or signatures
- **Privacy Protection**: Share confidential data without obvious encryption
- **Educational Purpose**: Demonstrate steganography concepts

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

### Development Setup

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add YourFeature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Disclaimer

This tool is provided for educational and legitimate privacy purposes only. Users are responsible for complying with applicable laws and regulations regarding data privacy and encryption in their jurisdiction. The developers assume no liability for misuse of this tool.

## Contact

For questions, suggestions, or issues, please contact

## Acknowledgments

- LSB steganography algorithm implementation based on academic research in digital image processing
- UI design inspired by modern security and privacy tools
- Bootstrap team for the excellent CSS framework

---

**Note**: Always verify that your encoded images retain their hidden messages after downloading, especially if you plan to share them through platforms that may compress or modify images.
