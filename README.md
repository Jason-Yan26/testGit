# testGit
Just a test for git

author:yzh
date:2022.04.29


import cv2
from skimage import morphology
import numpy as np

image_path = "D:\闫志豪-个人资料\Exercise_Moire_Pattern\image\理想化已处理抛物线形摩尔纹.png"  # 图片路径
img = cv2.imread(image_path)
# cv2.imshow('原始图像', img)  # 显示图片,[图片窗口名字，图片]
# cv2.waitKey(0)  # 无限期显示窗口

# 将图片转为灰度图
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
# 将灰度图二值化：大津阈值法
retval, binary = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY_INV | cv2.THRESH_OTSU)
cv2.imshow('二值图像', binary)  # 显示图片,[图片窗口名字，图片]
cv2.waitKey(0)  # 无限期显示窗口

thinned = cv2.ximgproc.thinning(binary)
cv2.imshow('骨架图像', thinned)  # 显示图片,[图片窗口名字，图片]
cv2.waitKey(0)  # 无限期显示窗口
# #提取图像骨架
# skeleton0 = morphology.skeletonize(binary)


#计算图像梯度的算子：cv2.Sobel(),cv2.Schar(),cv2.Laplacian()

sobelx = cv2.Sobel(thinned, cv2.CV_32F, 1, 0, ksize=-1)
sobelx = cv2.convertScaleAbs(sobelx)  # 绝对值转换
sobelx = np.float32(sobelx)
cv2.imshow('sobelx', sobelx)  # 显示图片,[图片窗口名字，图片]
cv2.waitKey(0)  # 无限期显示窗口

sobely = cv2.Sobel(thinned, cv2.CV_32F, 0, 1, ksize=-1)
sobely = cv2.convertScaleAbs(sobely)  # 绝对值转换
sobely = np.float32(sobely)
cv2.imshow('sobely', sobely)  # 显示图片,[图片窗口名字，图片]
cv2.waitKey(0)  # 无限期显示窗口

# 计算梯度的大小和方向
mag, angle = cv2.cartToPolar(sobelx, sobely, angleInDegrees=True)
print("successful!")
