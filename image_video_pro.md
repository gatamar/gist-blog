### install ImageMagick MacOS
```
brew install imagemagick
```

### create image of size with solid color
```
convert -size 100x100 xc:#00AAAA 1.png
```

### crop image
```
convert "1.png" -crop "64x64+0+16" +repage -strip -resample 72 "2.png"
```

### merge few images horizontally
```
convert in-1.jpg in-5.jpg in-N.jpg +append out-in1-plus-in5-and-inN.jpg
```

### remove sensitive metadata from image 
```
exiftool -all= path/to/image.jpg
```

### convert into another format
```
convert rose.jpg rose.png
```

### edit pano360 metadata (ExifTool)
```
exiftool -FullPanoWidthPixels=2000 -FullPanoHeightPixels=1000 -CroppedAreaLeftPixels=0 -CroppedAreaTopPixels=0 \
         -CroppedAreaImageWidthPixels=2000 -CroppedAreaImageHeightPixels=1000 -ProjectionType="equirectangular" panorama.jpg
```

### create loop from video
https://clideo.com/editor/loop-video
