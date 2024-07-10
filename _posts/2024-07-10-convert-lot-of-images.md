# How to convert lot of images?
### This text explain how to convert lof of images of lot of folders.

We will to use the *convert* command, bash, convert - https://packages.ubuntu.com/disco/graphicsmagick-imagemagick-compat

This is a sample
```
cd /tmp/my-albuns
ls -la
drwxrwxr-x  2 user user    4096 Out  4 19:10 ci
drwxrwxr-x  2 user user    4096 Jul 12 16:07 eletrica
drwxrwxr-x  2 user user    4096 Out 13 19:11 componentes-diversos
```
1.	create a folder with name-800
2.	convert all images of folder to 50% of original size.
set variables
```
SIZE='50%'		# resize image to 50% of owner size
OUT='800'		# output to converted folder name
```
convert all images of all folders
```
cd /tmp/my-albuns
for x in $(ls)
	do
	mkdir $x-$OUT
	for xx in $(ls $x)
		do
		echo "+ $x/$xx";
		convert -resize $SIZE $x/$xx $x-$OUT/$xx;
	done
done
```
output
```
drwxrwxr-x  2 user user    4096 Out  4 19:10 ci
drwxrwxr-x  2 user user    4096 Out  4 19:10 ci-800
drwxrwxr-x  2 user user    4096 Out 13 19:11 componentes-diversos
drwxrwxr-x  2 user user    4096 Out 13 19:11 componentes-diversos-800
drwxrwxr-x  2 user user    4096 Jul 12 16:07 eletrica
drwxrwxr-x  2 user user    4096 Jul 12 16:07 eletrica-800
```
***Be carefull*** To Delete folder that contain 800 at end of name and all content.
```
find . -name '*800' -exec rm -rf '{}' \;
```
