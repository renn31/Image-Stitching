# Image-Stitching

## Menginstall Packages yang Diperlukan

Untuk  melakukan images stitching perlu menginstall beberapa packages.
1.	Menginstall imutils
untuk menginstal imutils gunakan perinah berikut:
```bash
pip3 install imutils
```
2. Menginstal opencv-python
Untuk menginstall opencv-python gunakan perintah berikut:
```bash
pip3 install opencv-python
```
3. Menginstall mahplotlib
Untuk menginstall mathplotlib gunakan perintah berikut:
```bash
pip3 install matplotlib
```
## Eksekusi Image Stitching
1. Masuk ke dalam direktori yang berisi kodingan image stitching dan terdapat sebuah direktori yang berisi image yang akan digabungkan.
Gunakan perintah cd untuk masuk ke dalam direktori.
```bash
cd <direkori>
```
Gunakan perintah ls untuk melihat isi direktori.
```bash
ls -l
```
![image](https://github.com/renn31/Image-Stitching/assets/128461789/de1087dd-cafe-4883-9e49-66d3c8117495)

image_stitching_simple.py merupakan program python image stitching yang akan dieksekusi.

Direktori /images berisi images yang akan digabungkan. 
Berikut adalah potongan-potongan gambar yang akan digabungkan:

![image](https://github.com/renn31/Image-Stitching/assets/128461789/fc02a018-98c9-4013-878a-2b259e685533)

2.	Program yang akan digunakan adalah  image_stitching_simple.py yang berisi kodingan sebagai berikut:
```bash
# USAGE
# python image_stitching_simple.py --images images/scottsdale --output output.png

# import the necessary packages
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2

# construct the argument parser and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", type=str, required=True,
	help="path to input directory of images to stitch")
ap.add_argument("-o", "--output", type=str, required=True,
	help="path to the output image")
args = vars(ap.parse_args())

# grab the paths to the input images and initialize our images list
print("[INFO] loading images...")
imagePaths = sorted(list(paths.list_images(args["images"])))
images = []

# loop over the image paths, load each one, and add them to our
# images to stich list
for imagePath in imagePaths:
	image = cv2.imread(imagePath)
	images.append(image)

# initialize OpenCV's image sticher object and then perform the image
# stitching
print("[INFO] stitching images...")
stitcher = cv2.createStitcher() if imutils.is_cv3() else cv2.Stitcher_create()
(status, stitched) = stitcher.stitch(images)

# if the status is '0', then OpenCV successfully performed image
# stitching
if status == 0:
	# write the output stitched image to disk
	cv2.imwrite(args["output"], stitched)

	# display the output stitched image to our screen
	cv2.imshow("Stitched", stitched)
	cv2.waitKey(0)

# otherwise the stitching failed, likely due to not enough keypoints)
# being detected
else:
	print("[INFO] image stitching failed ({})".format(status))
```
3.	Lakukan perintah berikut untuk mengeksekusi.
```bash
python3 <program_yang_akan_dijalankan> --images <direktori_gambar_yang_akan_disatukan> --output <nama_file_output>
```
Sesuaikan dengan program yang akan dijalankan
```bash
python3 image_stitching_simple.py --images images/scottslade --output pp.png
```
Output akan otomatis tersimpan di dalam direktori dengan nama file yang telah ditentukan pada perintah saat eksekusi.
Berikut adalah tampilan output dari image stitching yang telah dilakukan:

![image](https://github.com/renn31/Image-Stitching/assets/128461789/eddfdb5a-35ab-46f4-8ddd-c7707cfa902d)



