gulp-sass
=========

SASS plugin for [gulp](https://github.com/wearefractal/gulp).

#Install

```
npm install gulp-sass
```

#Basic Usage

Something like this:

```javascript
var gulp = require('gulp');
var sass = require('gulp-sass')

gulp.task('sass', function () {
	gulp.src('./scss/*.scss')
		.pipe(sass())
		.pipe(gulp.dest('./css'));
});
```

Options passed as a hash into ```sass()``` will be passed along to [```node-sass```](https://github.com/andrew/node-sass)

#Imports and Partials

If you want to use imports or partials templates, you'll need to pass the ```includePaths``` option along to node-sass. So if you have files like this:

scss/includes/_settings.scss:

```sass
$blue: #3bbfce;
$margin: 16px;
```

scss/style.scss:

```sass
@import "settings";

.content-navigation {
  border-color: $blue;
  color:
    darken($blue, 9%);
}

.border {
  padding: $margin / 2;
  margin: $margin / 2;
  border-color: $blue;
}
```

Your code should look something like this:

```javascript
gulp.task('sass', function () {
  gulp.src('./scss/*.scss')
    .pipe(sass({includePaths: ['scss/includes']}))
    .pipe(gulp.dest('./css'));
});
```

