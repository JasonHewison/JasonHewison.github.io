---
layout: post
title: gulp-csslint-teamcity
tags: repository

links:
  src: https://github.com/ChunkySamurai/csCancellable
---

#gulp-csslint-teamcity
> A team city reporter for gulp-csslint (Inspired by jshint-teamcity)

## Usage

First, install `gulp-csslint-teamcity` as a development dependency:

```bash
npm install --save-dev gulp-csslint-teamcity
```

Then, add it to your `gulpfile.js`:

```javascript
var teamcity = require('gulp-csslint-teamcity');

gulp.task('css', function () {
  gulp.src('client/css/*.css')
    .pipe(csslint())
    .pipe(csslint.reporter(teamcity));
});
```

Unfortunately this is going to fill your console window with ugly csslint errors that are only intended for teamcity. What you really want to do is use gulp-util[https://github.com/gulpjs/gulp-util] to have the reporter only used in a team city build:

```javascript
var gutil = require('gulp-util');
var teamcity = require('gulp-csslint-teamcity');

gulp.task('css', function () {
  gulp.src('client/css/*.css')
    .pipe(csslint())
    .pipe(csslint.reporter(gutil.env.teamcity ? teamcity : undefined));
});
```

Then make sure teamcity builds the project with the --teamcity argument:

```bash
gulp build --teamcity
```
