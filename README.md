import cv2
import numpy as np
from tkinter.filedialog import *

pic = askopenfilename()
img = cv2.imread(pic)

grey = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
grey= cv2.medianBlur(grey,7)
edges = cv2.adaptiveThreshold(grey,255,cv2.ADAPTIVE_THRESH_MEAN_C,cv2.THRESH_BINARY,9,9)

#CARTOONIZE
color = cv2.bilateralFilter(img,9,250,250)
cartoon= cv2.bitwise_and(color,color,mask=edges)

cv2.imshow("Original",img)
cv2.imshow("Cartoonized",cartoon)

cv2.imwrite("Cartoon.jpg",cartoon)
cv2.waitKey(0)
cv2.destroyAllWindow()



