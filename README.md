# EX. NO. 01

# IMAGE HANDLING AND PIXEL TRANSFORMATIONS USING OPENCV

## AIM

To write a Python program using OpenCV to read and display images, adjust image brightness, modify image contrast, perform bitwise operations, and split and merge image colour channels.

## SOFTWARE REQUIRED

1. Anaconda – Python
2. Jupyter Notebook
3. OpenCV (cv2)
4. NumPy
5. Matplotlib

## ALGORITHM

**Step 1:** Import the required libraries, including OpenCV, NumPy and Matplotlib.

**Step 2:** Read the Eagle image in grayscale and display it using Matplotlib.

**Step 3:** Print the image width, height and channel information.

**Step 4:** Save the grayscale image as a PNG file and read it as a colour image.

**Step 5:** Crop the Eagle object, resize it by a factor of 2 and flip it horizontally.

**Step 6:** Read the Apollo-11 launch image and add text and a magenta rectangle.

**Step 7:** Read the Boy image and adjust its brightness using matrix addition and subtraction.

**Step 8:** Modify image contrast using scaling factors of 1.1 and 1.2.

**Step 9:** Split the image into Blue, Green and Red components and display them.

**Step 10:** Merge the R, G and B components and display the result.

**Step 11:** Convert the image into HSV colour space and split it into Hue, Saturation and Value components.

**Step 12:** Merge the HSV components and display the result.

**Step 13:** Perform bitwise operations and display the final output.

---

# PROGRAM

## 1. Import Required Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

## 2. Read the Eagle Image in Grayscale

```python
img = cv2.imread('Eagle_in_Flight.jpg', 0)
```

## 3. Print Image Width, Height and Channel

```python
height, width = img.shape

print("Width:", width)
print("Height:", height)
print("Channel: 1")
```

## 4. Display the Grayscale Image

```python
plt.imshow(img, cmap='gray')
plt.title("Eagle Grayscale Image")
plt.axis('off')
plt.show()
```

## 5. Save the Image as PNG

```python
cv2.imwrite('Eagle.png', img)
```

## 6. Read the Saved Image as a Colour Image

```python
gray_img = cv2.imread('Eagle.png', 0)
color_img = cv2.cvtColor(gray_img, cv2.COLOR_GRAY2BGR)
```

## 7. Display the Colour Image and Print Dimensions

```python
height, width, channel = color_img.shape

print("Width:", width)
print("Height:", height)
print("Channel:", channel)

plt.imshow(cv2.cvtColor(color_img, cv2.COLOR_BGR2RGB))
plt.title("Colour Image")
plt.axis('off')
plt.show()
```

## 8. Crop the Eagle Image

```python
cropped_img = img[50:400, 100:500]

plt.imshow(cropped_img, cmap='gray')
plt.title("Cropped Eagle Image")
plt.axis('off')
plt.show()
```

**Note:** Adjust the crop coordinates according to the Eagle's position in your image.

## 9. Resize the Image by a Factor of 2

```python
resized_img = cv2.resize(cropped_img, None, fx=2, fy=2)

plt.imshow(resized_img, cmap='gray')
plt.title("Resized Image")
plt.axis('off')
plt.show()
```

## 10. Flip the Image Horizontally

```python
flipped_img = cv2.flip(resized_img, 1)

plt.imshow(flipped_img, cmap='gray')
plt.title("Flipped Image")
plt.axis('off')
plt.show()
```

## 11. Read the Apollo-11 Launch Image

```python
apollo = cv2.imread('Apollo-11-launch.jpg')
apollo = cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB)
```

## 12. Add Text to the Image

```python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'

font_face = cv2.FONT_HERSHEY_PLAIN
font_scale = 2
color = (255, 255, 255)

cv2.putText(
    apollo,
    text,
    (50, apollo.shape[0]-30),
    font_face,
    font_scale,
    color,
    2
)
```

## 13. Draw a Magenta Rectangle

```python
rect_color = (255, 0, 255)

cv2.rectangle(
    apollo,
    (100, 50),
    (500, 600),
    rect_color,
    3
)
```

**Note:** Adjust rectangle coordinates to cover the rocket and launch tower in your image.

## 14. Display the Final Annotated Image

```python
plt.imshow(apollo)
plt.title("Apollo 11 Launch")
plt.axis('off')
plt.show()
```

## 15. Read the Boy Image

```python
img = cv2.imread('Boy.jpg')

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')
plt.show()
```

## 16. Create a Matrix of Ones for Brightness Adjustment

```python
matrix_ones = np.ones(img.shape, dtype=np.float64) * 50
```

## 17. Adjust Image Brightness

Create brighter and darker images using matrix addition and subtraction.

```python
img_float = img.astype(np.float64)

img_brighter = cv2.add(img_float, matrix_ones)
img_darker = cv2.subtract(img_float, matrix_ones)

img_brighter = np.clip(img_brighter, 0, 255).astype(np.uint8)
img_darker = np.clip(img_darker, 0, 255).astype(np.uint8)
```

## 18. Display Original, Darker and Brighter Images

```python
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title("Darker Image")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter Image")
plt.axis('off')

plt.show()
```

## 19. Modify Image Contrast

Create higher contrast images using scaling factors of 1.1 and 1.2.

```python
matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2

img_float = img.astype(np.float64)

img_higher1 = cv2.multiply(img_float, matrix1)
img_higher2 = cv2.multiply(img_float, matrix2)

img_higher1 = np.clip(img_higher1, 0, 255).astype(np.uint8)
img_higher2 = np.clip(img_higher2, 0, 255).astype(np.uint8)
```

## 20. Display Lower and Higher Contrast Images

```python
img_lower = cv2.multiply(
    img_float,
    np.ones(img.shape, dtype=np.float64) * 0.8
)

img_lower = np.clip(img_lower, 0, 255).astype(np.uint8)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB))
plt.title("Lower Contrast")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB))
plt.title("Higher Contrast")
plt.axis('off')

plt.show()
```

## 21. Split the Image into B, G and R Channels

```python
B, G, R = cv2.split(img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(B, cmap='gray')
plt.title("Blue Channel")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(G, cmap='gray')
plt.title("Green Channel")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(R, cmap='gray')
plt.title("Red Channel")
plt.axis('off')

plt.show()
```

## 22. Merge the B, G and R Channels

```python
merged_img = cv2.merge([B, G, R])

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged_img, cv2.COLOR_BGR2RGB))
plt.title("Merged RGB Image")
plt.axis('off')

plt.show()
```

## 23. Convert the Image into HSV Colour Space and Split Channels

```python
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

H, S, V = cv2.split(hsv_img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(H, cmap='gray')
plt.title("Hue Channel")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(S, cmap='gray')
plt.title("Saturation Channel")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(V, cmap='gray')
plt.title("Value Channel")
plt.axis('off')

plt.show()
```

## 24. Merge the H, S and V Channels

```python
merged_hsv = cv2.merge([H, S, V])

final_img = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(final_img, cv2.COLOR_BGR2RGB))
plt.title("Merged HSV Image")
plt.axis('off')

plt.show()
```

## 25. Perform Bitwise Operations

```python
mask = np.zeros(img.shape[:2], dtype=np.uint8)

cv2.rectangle(mask, (50, 50), (300, 300), 255, -1)

bitwise_img = cv2.bitwise_and(img, img, mask=mask)

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(bitwise_img, cv2.COLOR_BGR2RGB))
plt.title("Bitwise AND Image")
plt.axis('off')

plt.show()
```

---

# OUTPUT

The following outputs are obtained:

1. Read and display an image.
   <img width="653" height="528" alt="image" src="https://github.com/user-attachments/assets/cccd5dc6-2f12-4649-a06e-79a46e330e01" />
2. Adjust image brightness (darker and brighter images).
   <img width="1313" height="310" alt="image" src="https://github.com/user-attachments/assets/b0433dcc-ec99-434c-a579-21562633e964" />

4. Modify image contrast (lower and higher contrast).
   <img width="1256" height="300" alt="image" src="https://github.com/user-attachments/assets/897258d6-227d-4aee-afa0-1ecb3223f0c3" />

6. Generate an image using bitwise operations.
   <img width="1087" height="375" alt="image" src="https://github.com/user-attachments/assets/6b28a26e-a704-40cc-85fd-69971c407944" />


---

# RESULT

Thus, the images were successfully read and displayed using OpenCV. Image brightness and contrast adjustments, cropping, resizing, flipping, colour channel splitting and merging, and bitwise operations were performed successfully using Python.

---


**Title: Image Handling and Pixel Transformations Using OpenCV**

**Status: Completed**
