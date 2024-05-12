**QR Code Generator with Vue.js**

This Vue.js application generates customizable QR codes using the `@chenfengyuan/vue-qrcode` library. Users can generate both SVG and Canvas-based QR codes with various customization options.

### Setup

To run this application locally, follow these steps:

1. Clone the repository:

   ```bash
   git clone <repository-url>
   ```

2. Navigate to the project directory:

   ```bash
   cd <project-directory>
   ```

3. Install dependencies:

   ```bash
   npm install
   ```

4. Start the development server:

   ```bash
   npm run dev
   ```

### Features

- **SVG QR Code Generation**: Generates SVG-based QR codes with customizable options such as error correction level, width, and color.

- **Canvas QR Code Generation**: Generates Canvas-based QR codes with similar customization options as SVG.

- **SVG Download**: Users can download the SVG version of the generated QR code by clicking on the SVG QR code image.

- **PNG Download**: Users can download the PNG version of the generated QR code by clicking on the Canvas QR code.

### Usage

1. **SVG QR Code Generation**:
    - Locate the "QR CODE Example" section on the main page.
    - Under "SVG", an example QR code generated using SVG is displayed.
    - Customize the QR code parameters such as `errorCorrectionLevel`, `width`, and `color` to generate QR codes according to your preferences.

2. **Canvas QR Code Generation**:
    - Below the SVG example, you'll find another example QR code generated using Canvas.
    - Customize the Canvas QR code parameters similar to SVG QR codes.

### Credits

- This application utilizes the `@chenfengyuan/vue-qrcode` library for QR code generation.
- SVG download functionality adapted from [soldair/node-qrcode](https://github.com/soldair/node-qrcode).

<!-- https://github.com/fengyuanchen/vue-qrcode/blob/HEAD/src/README.md -->
<!-- https://github.com/soldair/node-qrcode#qr-code-options -->
