# Tools

## ImageMagick

### install ImageMagick MacOS
```
brew install imagemagick
```

### create image of size with solid color
```
convert -size 100x100 xc:#00AAAA 1.png
```

### create image with filled rect inside
```
# here "rectangle" takes LT+RB, not LT+WH 
convert -size 300x300 xc:black -fill xc:blue -draw "rectangle 100,100 200,200" hole.png
```

### crop image
```
convert "1.png" -crop "64x64+0+16" +repage -strip -resample 72 "2.png"
```

### resize image (assuming aspect ratio is the same)
```
convert input.gif -resize 256x256 output.gif
```

### merge few images horizontally
```
convert in-1.jpg in-5.jpg in-N.jpg +append out-in1-plus-in5-and-inN.jpg
```

### merge few images vertically
```
convert in-1.jpg in-5.jpg in-N.jpg -append out-in1-plus-in5-and-inN.jpg
```

### convert into another format
```
convert rose.jpg rose.png
```

## ExifTool

### remove sensitive metadata from image 
```
exiftool -all= path/to/image.jpg
```

### change orientation 
```
exiftool -orientation#=6 image.jpeg
```

### edit pano360 metadata (ExifTool)
```
exiftool -FullPanoWidthPixels=2000 -FullPanoHeightPixels=1000 -CroppedAreaLeftPixels=0 -CroppedAreaTopPixels=0 \
         -CroppedAreaImageWidthPixels=2000 -CroppedAreaImageHeightPixels=1000 -ProjectionType="equirectangular" panorama.jpg
```

## ffmpeg

`brew install ffmpeg`

### MOV to MP4

```
ffmpeg -i my-video.mov -vcodec h264 -acodec mp2 my-video.mp4
```

## Other

### create loop from video
https://clideo.com/editor/loop-video

# Processes

## 🎬 Create your custom MOVIE

So I have a bunch of videos from the hiking mountain trip.
Now I want to make a "movie" and post in on Youtube via a private link.
I have two apps installed: iMovie and LumaFusion, and they say it's more than enough.
I'm very new to this stuff, so the UX seems terrible to me in the both apps.

This is an "algorithm" of how I see such movie creation:
1. Prepare a folder with the videos I want to merge into a one "movie".
2. Merge that videos into a one big movie.
3. Speed up some chunks of the movie as they are not so dynamic.
4. Remove some chunks of the movie as they are not so interesting/appropriate.
5. Make spoilers - copy some chunks of the movie and insert them at the beginning of the movie.
6. For some chunks of the movie, remove the sound.
6. For some chunks of the movie, overlay the music.
7. For some chunks of the movie, overlay the text.
8. For some chunks of the movie, overlay my voice with some comments.
8. Insert photos into some places between the frames.
9. Make animations at the edges.
