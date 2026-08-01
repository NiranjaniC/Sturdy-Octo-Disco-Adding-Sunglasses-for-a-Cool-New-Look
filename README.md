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
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
# Load the Face Image
faceImage = cv2.imread('face.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
faceImage.shape
#resized_faceImage.shape
faceImage.shape
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('glass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(370,140))
print("image Dimension ={}".format(glassPNG.shape))
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()
# Replace the eye region with the sunglass image
faceWithGlassesNaive[385:525,240:610]=glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)
# Make a copy
faceWithGlassesArithmetic = faceImage.copy()
# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[385:525,225:595]
# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)
# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[385:525,225:595]=eyeRoiFinal
# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

## Output

<img width="944" height="752" alt="image" src="https://github.com/user-attachments/assets/7454e9ec-9e79-433e-beb4-771938b547c4" />
<img width="914" height="759" alt="image" src="https://github.com/user-attachments/assets/6975975f-7880-4a0c-9444-d4c1ef8cd442" />
<img width="932" height="437" alt="image" src="https://github.com/user-attachments/assets/1952584d-8abf-487b-a632-ad7126875974" />
<img width="950" height="608" alt="image" src="https://github.com/user-attachments/assets/1638078e-2be7-470d-bc46-fa12b9a73f4b" />
<img width="931" height="653" alt="image" src="https://github.com/user-attachments/assets/a1bf788e-35c3-4a4f-a785-1c94bf43d229" />
<img width="931" height="757" alt="image" src="https://github.com/user-attachments/assets/c4ed5126-6336-4991-8789-6c29d2139a04" />

## Result

The passport-size image was successfully processed using OpenCV by overlaying a pair of sunglasses onto the eye region. Image masking and alpha blending techniques were used to ensure the sunglasses blended naturally with the original image. The final output demonstrates the successful implementation of image overlay and basic image manipulation using OpenCV.






