# -Exp-10--Record-IMPLEMENTATION-OF-OPENING-AND-CLOSING
## Name : SHRIHARI M
## Reg.no : 212225230265
## Exp-10- Record-IMPLEMENTATION OF OPENING AND CLOSING
## Aim :
To implement morphological opening and closing operations on a noisy image using a 5*5 structuring element in OpenCV, and to observe their effect on salt-and-pepper noise.

## Algorithm :
Step - 1 :
Create a grayscale image with the text “TAMIZHSELVAN B”.

Step - 2 :
Add white noise to the image.

Step - 3 :
Apply opening using a 5*5 kernel to remove white noise.

Step - 4 :
Add black noise and apply closing to remove black noise.

Step - 5 :
Apply morphological gradient to detect the edges and display all the results.

## Program :
```
import numpy as np
import cv2
import matplotlib.pyplot as plt
blank=np.zeros((600,600))
import numpy as np
import matplotlib.pyplot as plt

image = np.zeros((600, 600, 3), dtype=np.uint8)
plt.imshow(image)
plt.axis('on')
plt.show()

def load_image():
    blank_image = np.zeros((600, 800), dtype=np.uint8)
    font = cv2.FONT_HERSHEY_SIMPLEX
    cv2.putText(
        blank_image,
        text='SHRIHARI M',
        org=(30, 350),
        fontFace=font,
        fontScale=2.5,
        color=255,
        thickness=8,
        lineType=cv2.LINE_AA
    )
    return blank_image
def display_img(img):
    fig = plt.figure(figsize=(12, 8))
    ax = fig.add_subplot(111)
    ax.imshow(img, cmap='gray')
    plt.axis('off')
    plt.show()

img = load_image()
kernel = np.ones((5, 5), dtype=np.uint8)
white_noise = np.random.randint(
    low=0,
    high=2,
    size=(600, 800),
    dtype=np.uint8
)

white_noise = white_noise * 255
noise_img = white_noise + img
noise_img = np.clip(noise_img, 0, 255).astype(np.uint8)
display_img(noise_img)

opening = cv2.morphologyEx(noise_img, cv2.MORPH_OPEN, kernel)
display_img(opening)
black_noise = np.random.randint(
    low=0,
    high=2,
    size=(600, 800)
)
black_noise = black_noise * -255
black_noise_img = img.astype(np.int16) + black_noise
black_noise_img[black_noise_img == -255] = 0
black_noise_img = np.clip(black_noise_img, 0, 255).astype(np.uint8)
display_img(black_noise_img)

closing = cv2.morphologyEx(black_noise_img, cv2.MORPH_CLOSE, kernel)
display_img(closing)


display_img(img)

gradient = cv2.morphologyEx(img,cv2.MORPH_GRADIENT,kernel)
display_img(gradient)
```
## Output:
<img width="536" height="662" alt="image" src="https://github.com/user-attachments/assets/14d9195e-35f8-40b7-ab26-2494b0297f7c" />

<img width="546" height="792" alt="image" src="https://github.com/user-attachments/assets/806bdcc9-9c87-43d0-9884-fdde5d6f5bcf" />

<img width="587" height="805" alt="image" src="https://github.com/user-attachments/assets/815a4d23-3c85-4d07-a3b2-399573f3fea7" />

<img width="602" height="405" alt="image" src="https://github.com/user-attachments/assets/21759942-5150-4ed4-8060-a726f3405188" />

## Result :
The opening and closing operations were successfully implemented using OpenCV. Opening effectively reduces white (salt) noise, while closing reduces black (pepper) noise and fills small gaps in the text. The morphological gradient successfully highlights the edges of the text. Thus, the effects of morphological opening, closing, and gradient operations were successfully observed.
