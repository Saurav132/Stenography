# Image Steganography with OpenCV

This project implements a simple image steganography technique using OpenCV, allowing users to hide a secret message inside an image and retrieve it later using a passcode.

## Features
- Hide a text message inside an image
- Retrieve the hidden message using a passcode
- Uses OpenCV for image processing

## Requirements
Make sure you have the following installed:
- Python 3.x
- OpenCV (`cv2`)

You can install OpenCV using:
```bash
pip install opencv-python
```

## Usage
### 1. Encoding a Secret Message
Run the script and provide the required inputs:
```bash
python steganography.py
```
- Enter the secret message you want to hide.
- Provide a passcode for decryption.
- The modified image will be saved as `encryptedImage.jpg`.

### 2. Decoding the Hidden Message
- Re-run the script and enter the correct passcode to retrieve the hidden message.

## Code Overview
```python
import cv2
import os

img = cv2.imread("mypic.jpg")  # Replace with the correct image path
msg = input("Enter secret message:")
password = input("Enter a passcode:")

d = {}
c = {}
for i in range(255):
    d[chr(i)] = i
    c[i] = chr(i)

n, m, z = 0, 0, 0
for i in range(len(msg)):
    img[n, m, z] = d[msg[i]]
    n += 1
    m += 1
    z = (z + 1) % 3

cv2.imwrite("encryptedImage.jpg", img)
os.system("start encryptedImage.jpg")

# Decryption
message = ""
n, m, z = 0, 0, 0
pas = input("Enter passcode for Decryption")
if password == pas:
    for i in range(len(msg)):
        message += c[img[n, m, z]]
        n += 1
        m += 1
        z = (z + 1) % 3
    print("Decryption message:", message)
else:
    print("YOU ARE NOT AUTHORIZED")
```

## Notes
- The script currently modifies pixel values directly, which might make the image visibly different if the message is long.
- The encoding and decoding method is simple and does not use advanced encryption techniques.

## Contributing
Feel free to fork this repository and enhance the steganography technique. Pull requests are welcome!

## License
This project is open-source and available under the MIT License.

