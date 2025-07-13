# Image-to-PDF-converter
convert multiple images into 1 pdf and reduce the size 

import os
from PIL import Image

print("--------Welcomr TO IMAGE COMPRESSOR--------")

print("Enter the path of image one by one (type 'done' when finished): ")
image_paths = []                                                     # Empty list

while True:
    path = input("Image path:")                                      # give input as image adress or path
    if path.lower() == "done":
        break
    if os.path.exists(path):                                         # check the existance of image
        image_paths.append(path)
    else:
        print("File not found. Please try again!")

if not image_paths:
    print("File was not found. Try again ")

else:
    
    images = []
    total_original_size = 0
    for path in image_paths:
        total_original_size += os.path.getsize(path) / (1024 * 1024)                      # convert size into MB
        img = Image.open(path)
        if img.mode == "RGBA":
            img= img.convert("RGB")                                                         
        images.append(img)

    output_pdf = input("Enter the name of new file (do not include = .pdf): ")
    new_pdf = output_pdf + ".pdf"

    images[0].save(new_pdf,save_all = True, append_images = images[1:], format="PDF")
    pdf_size = os.path.getsize(new_pdf) / (1024 * 1024)


    print("Conversion Complete")
    print(f"Original image size : {total_original_size:.2f} MB")
    print(f"New image size : {pdf_size:.2f} MB")
    print(f"Saved as : {new_pdf}")
