# DT173G-Webbutveckling-3
School assignment to learn git

## Assignment 2

NodeJs and automatisation with Gulp.

### Purpose

The purpose of this assigment is to learn the basics of gulp and using it to automate tasks.

In this assigment I will use gulp with npm packages from https://www.npmjs.com/
To merge and minimize CSS files, JS files, minimize pictures and automaticly transfer them and html files
from a sourch map to a published map. 

Note: added /node_modules to gitignore, so they wont be uploded to the repo.

### Gulp - https://www.npmjs.com/package/gulp

Will be used for this assigment, the gulp functions I will use is "src, dest, parallel, series, watch"

1. **src**
This is for deciding our source map.
    
2. **dest**
This is for deciding our published map.

3. **parallel**
This is so our files can be written and handled at the same time from the src map to the pub map.

4. **series**
This is for queue more then one commands.

5. **watch**
This is so we can watch for changes in our files and automaticly updating them.

### gulp-concat - https://www.npmjs.com/package/gulp-concat

Will be used for for merging togheter my CSS and JS files.

This was a good alternative since it works for both css and js files.

### gulp-terser - https://www.npmjs.com/package/gulp-terser

Tereser is used to minimize js files (removing comment and spaces to make the file smaller)

This seamed like a good alternative for JS minimizing. 

### gulp-cssnano - https://www.npmjs.com/package/gulp-cssnano

Cssnano was used to minimize the css file. 

However the v8.0 has an error, so I had to use the older version 7.1 as can be seen in the 
package.json file. ("gulp-imagemin": "^7.1.0",) maybe there is a better alternative,
but the old version seams to work just fine.

### How it was created

#### The projekt with gulp

First I initiated a new npm projekt by using npm init, I filled in the settings.

After this I got my package.json file.

Then I created my source files. 

I installed gulp with "npm i gulp --save-dev"

The I created a gulpfile.js to save my gulp task in. 

In the beggining of this file I will get the gulp files and packages files needed for this assigment. 

#### The variables

I will start with an object that determs wich gulp files I will use. const {
    src, dest, parallel, series, watch} = require('gulp');

Then I will make variables for the packages I'm using
const conCat = require('gulp-concat')

const terser = require('gulp-terser');

const cssnano = require('gulp-cssnano');

const imagemin = require('gulp-imagemin');

Then I will decide where the sourch files will be and what files will be taken from them
const files = {
    htmlPath: "src/**/*.html",
    cssPath: "src/css/*.css",
    jsPath: "src/js/*.js",
    imgPath: "src/img/*"
}
All html files, all css files, all js files and then all files in the image folder.

#### The tasks

Here I will set up diffrent functions to do the requiered tasks.

**Html**
the first function will copy over the html files, no minimising or changes will be done.

I will use a  return src(files.htmlPath) this conects to our html path in the const files.
Then a .pipe(dest('pub')); to decide where the files should be transfered to.

**CSS**
Then a function for our css task, this task will find the source then run a .pipe(conCat('main.css'))
putting all css files togheter into one file named main.css. 

Then run a .pipe(cssnano()) minimizing the file.

Then .pipe(dest('pub/css')); to send them to thier destination.

**JS**

Then I will do the exact same thing with the Javascript files.
The only diffrence is that I will use .pipe(terser()) to minimize the files.

**IMG**
In the img task I will return src file use a .pipe(imagemin()) to minimize all images in the map
before sneding the to the pub map.

**Watch**

Then I will use the Gulp command watch for the watch funktion.
I will use a array with watch with the paths inside the array (files.htmlPath, files.cssPath, files.jsPath, files.imgPath) This will tell the watch wich files to listen to for changes.
Then I will add a parallel(copyHTML, cssTask, jsTask, imageTask)); this will tell the watch what to do when 
one of the files changes.

**Export**
Then I will export the files by adding them to a exports.defult = series object, the series will ensure it does one of the things at a time. Inside this object I will first send all the files togheter with  parallel(copyHTML, cssTask, jsTask, imageTask) and then I will start the watchTask that will automaticly update the files, minimize and merge them into the pub map.

### How to use

To use these files yourshelfe I recommend to use Visual studio code.
Clone the repository with git clone https://github.com/JohnJohansson/DT173G-Uppgift-2.git in the terminal.
Check if you have gulp installed with "gulp --version" If its not install it with "npm install gulp-cli -g"
With gulp installed you can write "npm install" in the Terminal and it will automaticly downlode all the dependencies.

To start gulp and run the code you just need to write "gulp" in the terminal, now all changes you do to the html files, the css files, js files and images will automaticly be sent to the pub map and minimized.

You cant use the terminal while running the autmatic updater, to stop it hold down ctrl+C in the terminal.











