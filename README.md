# NAME: ASWIN.L
# REG NO: 212224230028
# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('me.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
faceImage.shape
glassPNG = cv2.imread('sung.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
glassPNG = cv2.resize(glassPNG,(150,70))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[180:250,150:300]=glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI= faceWithGlassesArithmetic[180:250,150:300]
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
maskedGlass = cv2.multiply(glassBGR,glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
faceWithGlassesArithmetic[180:250,150:300]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

## Output:

<img width="378" height="498" alt="Screenshot 2025-09-22 101427" src="https://github.com/user-attachments/assets/1af0354c-c3b8-4e32-a19a-568e637019e0" />
<img width="591" height="330" alt="Screenshot 2025-09-22 101443" src="https://github.com/user-attachments/assets/1bea6e65-6875-44a3-9d64-421a3fd55ac7" />
<img width="1161" height="308" alt="Screenshot 2025-09-22 101502" src="https://github.com/user-attachments/assets/f544590e-6954-4ec8-b2da-7b1ff433981a" />
<img width="382" height="472" alt="Screenshot 2025-09-22 101510" src="https://github.com/user-attachments/assets/3b2c2e81-8908-4620-aa76-8e8c2500ca19" />
<img width="1164" height="233" alt="Screenshot 2025-09-22 101521" src="https://github.com/user-attachments/assets/821b12b6-6121-403d-8e3a-3dda771139bc" />
<img width="1163" height="715" alt="Screenshot 2025-09-22 101546" src="https://github.com/user-attachments/assets/15dbc6dd-8497-42d5-86e9-a686aed2732c" />


Feel free to fork, contribute, or customize this project for your creative needs!
