# gulp-md5-assets

This is a fork of [gulp-md5-assets](https://github.com/stipsan/gulp-md5-assets)

The difference between gulp-md5-plus and gulp-md5-assets is the result:
```html
	Sample from a index.html file before transformation:
	<link rel="stylesheet" type="text/css" href="main.css">
	gulp-md5-plus
	<link rel="stylesheet" type="text/css" href="main_afd9d92ebe.css">
	gulp-md5-assets
	<link rel="stylesheet" type="text/css" href="main.css?afd9d92ebe">
```

But gulp-md5-assets will cause ```main.css?afd9d92ebe``` saved on disk. This fork just save ```main.css``` for the ease to upload static files to server.

## Usage

First, install `gulp-md5-assets` as a development dependency:

```shell
npm install --save-dev gulp-md5-assets
```

Then, add it to your `gulpfile.js`:

```javascript
var md5 = require("gulp-md5-assets");

gulp.src("./src/*.css")
	.pipe(md5(10,'./output/index.html'))
	.pipe(gulp.dest("./dist"));
```

md5 all css files in the src folder and change these css names in the quoted html--index.html


```javascript

gulp.task('img' ,function() {
    var imgSrc = './static/img/**',
        quoteSrc = './output/static/css/**/*.css',
        imgDst = './output/static/img';

    return gulp.src(imgSrc)
        .pipe(imagemin())
        .pipe(md5(10 ,quoteSrc))
        .pipe(gulp.dest(imgDst));
});

```

first, optimize all images in the img folder including all sub folders; then md5 all these images and change these images' names in the quoted css files ;
####note
the directory of the md5ed files in the imgDst folder is the same as that of original files in the imgSrc folder; and css files can refer the image file with the same name in different folder rightly;

## API

### md5(size,file)

#### size
Type: `String`
Default: null

Optionnal: you can pass the size to limit the size of the hash that is appended.

#### file
Type: `String`
Default: null

Optionnal: the file need to replace the file name of the md5ed files. dir is also supported

Example:
```javascript
	gulp.src('static/js/*')
        .pipe(md5(10,'./output/html'))
        .pipe(gulp.dest('./output'));
```

The sample above will append the md5 hash(length : 10) to each of the file in the static/js folder then repalce the link file name in the output/html/ using md5ed file name; at last store all of that into the *output* folder.


## License

http://en.wikipedia.org/wiki/MIT_License[MIT License]


