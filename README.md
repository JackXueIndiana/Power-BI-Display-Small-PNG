# Power-BI-Display-Small-PNG
Currently, in Power BI you can write R code to display PNG images but can not retrieve the image from URL. As a work around, to display small PGN you may use Base64 encode/decode.

I made the following code working in powerbi.com:


library(base64enc)
library(png)

base64String <- "iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAABGdBTUEAAK/INwWK6QAAAdFJREFUWMPll79Lw0AUxzMWpw4iKKKHIAZcblQQDBScBLu6VRwj2FFcblOEThYnwfwBLm4OHSounaSruBRcHTo4OZ3vW1KJyTvJpWdrMfCB8u77vnyb+5HE01p7k8T7UwHGdU1FgBLRICKGE4PvTz2NeDx3gEa9XtdKqQy1Wg3CFhOgZepBPQ5hF8B0CSEgriT0FSmlUV8kAG6X7vVeqPyRIYquIe4k9B3UOC084GU7Bbia1eould9ZhFga3oUKfpt08IBX0V3Qb7fvaOgtQxQ1h3ehg9+cBr3wGGUbhlKu09ArixCLA0zjQbAJ03DUc4D+4TkNP2dQ6kibxlBPrZPCAWiOF3S//0CSp2+gxtUBelI7xTpAGM/fAKUOSPKYC2iTvelpyBNgS8oVWkQXX3S7VyS5zwW0yV54wdMmQDUIsPhunQAveFoG8Kl04wR4FQiwSqVLJ8DLNoAXP3A0h9ZnLCZ9+uGVJ8BsuVyi5MssWp+ymPTwgqflFOCEO3YCvAqsgXkqHToBXgUCzFFp3wnwsg3gCzFDJ9oai9Z7LCY9vOBpuwt8w/sdSXdY4hXP9fgu34pJus0SB/j113KSbrCMK0Ar74Ez1R8mkwnwL7+OPwFmauaESwFeIAAAAABJRU5ErkJggg=="

#read the PNG image file
base64StringDecoded <- base64decode(base64String)
fileConn<-file(tf <- tempfile(fileext = "logo1.png"), "wb")
writeBin(base64StringDecoded , fileConn)
close(fileConn)

pic <- readPNG(tf)
file.remove(tf) # cleanup

plot(0:1,0:1,type="n",ann=FALSE,axes=FALSE)

rasterImage(pic,0,0,1,1)


I used a web site, https://www.base64-image.de/encode, to convert the PNG to a Basse64 string.
