# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** [Your Name Here]  
- **Register Number:** [Your Register Number Here]
# Ex. No. 01 – Digital Image Processing Using OpenCV

## 1. Read the image using OpenCV imread() as a grayscale image.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread('fox.jpg', cv2.IMREAD_GRAYSCALE)
```

## 2. Print the image width, height and channel.

```python
height, width = img.shape
channel = 1

print("Width:", width)
print("Height:", height)
print("Channel:", channel)
```

## 3. Display the image using Matplotlib imshow().

```python
plt.imshow(img, cmap='gray')
plt.title('Grayscale Image')
plt.axis('off')
plt.show()
```

## 4. Save the image as a PNG file using OpenCV imwrite().

```python
cv2.imwrite('fox_gray.png', img)
```

## 5. Read the saved image as a color image using cv2.cvtColor().

```python
gray_img = cv2.imread('fox_gray.png', cv2.IMREAD_GRAYSCALE)
color_img = cv2.cvtColor(gray_img, cv2.COLOR_GRAY2BGR)
```

## 6. Display the color image and print its width, height and channel.

```python
height, width, channel = color_img.shape

print("Width:", width)
print("Height:", height)
print("Channel:", channel)

color_rgb = cv2.cvtColor(color_img, cv2.COLOR_BGR2RGB)

plt.imshow(color_rgb)
plt.title('Color Image')
plt.axis('off')
plt.show()
```

## 7. Crop the image to extract a specific object from the image.

```python
img = cv2.imread('fox.jpg')

cropped_img = img[100:400, 100:400]

cropped_rgb = cv2.cvtColor(cropped_img, cv2.COLOR_BGR2RGB)

plt.imshow(cropped_rgb)
plt.title('Cropped Image')
plt.axis('off')
plt.show()
```

*Note: Adjust the crop coordinates to capture the fox properly in your image.*

## 8. Resize the image up by a factor of 2x.

```python
resized_img = cv2.resize(
    cropped_img, None, fx=2, fy=2,
    interpolation=cv2.INTER_LINEAR
)

resized_rgb = cv2.cvtColor(resized_img, cv2.COLOR_BGR2RGB)

plt.imshow(resized_rgb)
plt.title('Resized Image 2x')
plt.axis('off')
plt.show()
```

## 9. Flip the cropped/resized image horizontally.

```python
flipped_img = cv2.flip(resized_img, 1)

flipped_rgb = cv2.cvtColor(flipped_img, cv2.COLOR_BGR2RGB)

plt.imshow(flipped_rgb)
plt.title('Horizontally Flipped Image')
plt.axis('off')
plt.show()
```

## 10. Read the image using OpenCV.

```python
img = cv2.imread('fox.jpg')

img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.imshow(img_rgb)
plt.title('Original Image')
plt.axis('off')
plt.show()
```

## 11. Add the given text to the bottom of the image, centered on the image.

```python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN

height, width, channel = img.shape

font_scale = 3
thickness = 3

text_size = cv2.getTextSize(text, font_face, font_scale, thickness)[0]

x = (width - text_size[0]) // 2
y = height - 30

cv2.putText(img, text, (x, y), font_face, font_scale,
            (255, 255, 255), thickness)

```

## 12. Draw a magenta rectangle around the image.

```python
height, width, channel = img.shape

rect_color = (255, 0, 255)

cv2.rectangle(img, (50, 50), (width-50, height-50),
              rect_color, 5)
```

## 13. Display the final annotated image.

```python
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 7))
plt.imshow(img_rgb)
plt.title('Final Annotated Image')
plt.axis('off')
plt.show()
```

## 14. Read the image.

```python
img = cv2.imread('fox.jpg')

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')
plt.show()
```

## 15. Adjust the brightness of the image by creating a matrix of ones with float64 data type.

```python
matrix_ones = np.ones(img.shape, dtype=np.float64)
matrix = matrix_ones * 50
```

## 16. Create brighter and darker images.

```python
img_brighter = cv2.add(img, matrix, dtype=cv2.CV_8U)
img_darker = cv2.subtract(img, matrix, dtype=cv2.CV_8U)
```

## 17. Display the images (Original Image, Darker Image, Brighter Image).

```python
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
darker_rgb = cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB)
brighter_rgb = cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(img_rgb)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(darker_rgb)
plt.title('Darker Image')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(brighter_rgb)
plt.title('Brighter Image')
plt.axis('off')

plt.show()
```

## 18. Modify the image contrast using factors 1.1 and 1.2.

```python
matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2

img_higher1 = cv2.convertScaleAbs(img, alpha=1.1, beta=0)
img_higher2 = cv2.convertScaleAbs(img, alpha=1.2, beta=0)

img_lower = cv2.convertScaleAbs(img, alpha=0.8, beta=0)
```

## 19. Display the images (Original, Lower Contrast, Higher Contrast).

```python
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
lower_rgb = cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB)
higher_rgb = cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(img_rgb)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(lower_rgb)
plt.title('Lower Contrast')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(higher_rgb)
plt.title('Higher Contrast')
plt.axis('off')

plt.show()
```

## 20. Split the image into B, G, R components and display the channels.

```python
img = cv2.imread('fox.jpg')

B, G, R = cv2.split(img)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(B, cmap='gray')
plt.title('Blue Channel')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(G, cmap='gray')
plt.title('Green Channel')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(R, cmap='gray')
plt.title('Red Channel')
plt.axis('off')

plt.show()
```

## 21. Merge the R, G, B channels and display along with the original image.

```python
img = cv2.imread('fox.jpg')

B, G, R = cv2.split(img)

merged_img = cv2.merge([B, G, R])

img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
merged_rgb = cv2.cvtColor(merged_img, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img_rgb)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(merged_rgb)
plt.title('Merged RGB Image')
plt.axis('off')

plt.show()
```

## 22. Split the image into H, S, V components and display the channels.

```python
img = cv2.imread('fox.jpg')

hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

H, S, V = cv2.split(hsv)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(H, cmap='gray')
plt.title('Hue Channel')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(S, cmap='gray')
plt.title('Saturation Channel')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(V, cmap='gray')
plt.title('Value Channel')
plt.axis('off')

plt.show()
```

## 23. Merge the H, S, V channels and display along with the original image.

```python
img = cv2.imread('fox.jpg')

hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

H, S, V = cv2.split(hsv)

merged_hsv = cv2.merge([H, S, V])

merged_img = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
merged_rgb = cv2.cvtColor(merged_img, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img_rgb)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(merged_rgb)
plt.title('Merged HSV Image')
plt.axis('off')

plt.show()
```

---



## Output:
## ORIGINAL

<img width="258" height="307" alt="Screenshot 2026-11-19 140354" src="https://github.com/user-attachments/assets/9e1f69f3-e506-4f50-add3-15f76c720856" />


## LINE

<img width="297" height="297" alt="Screenshot 2026-11-19 140402" src="https://github.com/user-attachments/assets/17721737-814b-400d-8bce-f3868430e4cc" />


## CIRCLE
<img width="255" height="302" alt="Screenshot 2026-11-19 140418" src="https://github.com/user-attachments/assets/e40d69ec-2639-4a0d-a9f8-2d4e9e45d194" />

## RECTANGLE

<img width="237" height="296" alt="Screenshot 2026-11-19 140430" src="https://github.com/user-attachments/assets/18ea8a6c-bff9-4459-a194-bc9ac0191837" />

## HSV

<img width="231" height="315" alt="Screenshot 2026-11-19 140451" src="https://github.com/user-attachments/assets/bd3ddbe8-a8e2-42e5-922b-71923f502850" />

## GRAYSCALE

<img width="232" height="297" alt="Screenshot 2026-11-19 140506" src="https://github.com/user-attachments/assets/909eb251-9139-4bd9-8f8f-5281f5338fa4" />

## YCRCB

<img width="235" height="303" alt="Screenshot 2026-11-19 140516" src="https://github.com/user-attachments/assets/12b5be50-3c3c-4fcb-bd24-6458d25da2d1" />

## RESIZE IMAGE

<img width="445" height="545" alt="Screenshot 2026-11-19 140545" src="https://github.com/user-attachments/assets/45b979bb-9b57-4670-a520-cc46e911efc4" />

## CROPPED

<img width="377" height="492" alt="Screenshot 2026-11-19 140603" src="https://github.com/user-attachments/assets/f4d17356-16b4-46d2-a897-48744817c767" />

## HORIZONTAL FLIP 

<img width="422" height="535" alt="Screenshot 2026-11-19 140627" src="https://github.com/user-attachments/assets/f289709c-8d16-4f2f-a190-a77af33bbed3" />

## VERTICAL FLIP


<img width="415" height="495" alt="Screenshot 2026-11-19 140636" src="https://github.com/user-attachments/assets/a0cc48ac-875a-410d-bfd0-a3c5af859727" />










## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

