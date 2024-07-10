# How to convert lot of images?
### This text explain how to convert lof of images of lot of folders.

We will to use the ***convert*** command, bash, convert - https://packages.ubuntu.com/disco/graphicsmagick-imagemagick-compat

This is a sample
```
cd /tmp/my-albuns
ls -la
drwxrwxr-x  2 user user    4096 Out  4 19:10 ci
drwxrwxr-x  2 user user    4096 Jul 12 16:07 eletrica
drwxrwxr-x  2 user user    4096 Out 13 19:11 componentes-diversos
```

set variables
```
SIZE='50%'	# resize image to 50% of owner size
OUT='800'	# output to converted folder name, 800x600
```

What the script will do?
1.	create a folder with name-800
2.	convert all images of folder to 50% of original size

F: Folder name
I: Image file
```
cd /tmp/my-albuns
SIZE='50%'
OUT='800'
for F in $(ls)
	do
	mkdir $F-$OUT
	for I in $(ls $F)
		do
		echo "+ $F/$I";
		convert -resize $SIZE $F/$I $F-$OUT/$I;
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
