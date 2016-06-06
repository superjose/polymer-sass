## Synopsis

This shows you how to integrate your sass files with Polymer's custom element. Thanks goes to [David Vega](http://stackoverflow.com/a/33875597/1057052) for showing how it is done. This script is done using gulp, and what it does is that it injects your sass file's processed content into a shared style html.

## Code Example

This assumes that you have your files inside an "app" folder. This can be modified inside the gulpfile. 
```javascript
 gulpfile.js
 /app
     /whatever
             -your-component.html
             -your-component-styles.html
             -your-component-styles.scss
      /hero-tournament
                      -hero-tournament.html
                      -hero-tournament-styles.html
                      -hero-tournament-styles.scss
```

Note that the most important thing is that the styles scss file has the same name as the .html file

If you have an element called "hero-tournament":
```javascript
<dom-module id="hero-tournament">
  <template>
    <style>    </style>
  </template>
  <script>
    (function() {
      'use strict';
      Polymer({
        is: 'hero-tournament',
      });
    })();
  </script>
</dom-module>
```
Create two new  files (Files do not need to be in the same tree structure, but they must be inside the app folder. For this example they are adjacent, or at the same level as hero-tournament.html. If you move them, then remember to do the required changes for the referencing):
    
```
 -hero-tournament-styles.html
 -hero-tournament-styles.scss
```
Your -hero-tournament-styles.html file will have the following:
```html
<!-- pgarena-hero-tournament-style.html -->
<dom-module id="hero-tournament-style">
  <template>
    <!-- Start Style -->
      <style>
      </style>
    <!-- End Style -->
  </template>
</dom-module>
```

Note the HTML comments: Start Style and End Style? They are super important. **Do not remove them**. Inside them, your processed sass content will be injected. 

Then, in your hero-tournament-styles.scss put all your sass or css: 
(Example):
```css
:host{
 background-color: #FFF; /*Yes! :host element works*/
}
.blank{
display: none;
}
```

Now, it's time to run your gulpfile, which you should have put besides your "app" folder. 
```javascript
gulp watchSass
```

Now, any changes that you make to your .scss files will be injected to your -styles.html file. 
```html
<dom-module id="hero-tournament-style">
  <template>
<!-- Start Style -->
<style>.blank{display:none}
</style><!-- End Style -->
  </template>
</dom-module>
```


**One Last Thing**
We need to reference your hero-tournament-styles.html file into hero-tournament.html! 
This is done through these lines of code:
```html
<link rel="import" href"hero-tournament-styles.html">
<style include="shared-styles"></style>
```
Which in the example element, would be placed like this:
```html

<link rel="import" href"hero-tournament-styles.html">
<dom-module id="hero-tournament">
  <template>
    <!-- include the style module by name -->
<style include="hero-tournament-styles"></style>
  </template>
  <script>
    (function() {
      'use strict';
      Polymer({
        is: 'hero-tournament',
      });
    })();
  </script>
</dom-module>
```
That's it. Worry not if you modify your .scss files, it will automatically update them for you!! Just be sure not to remove the  <!-- Start Style --> and  <!-- End Style --> HTML comments from your hero-tournament-styles.html file!!

## Motivation

A short description of the motivation behind the creation and maintenance of the project. This should explain **why** the project exists.

## Installation

Go to your project, before the "app" folder and place the "gulpfile.js" and "package.json" (Careful with the latter one, I recommend you to open it and copy and paste the different ones into your own package.json file)

The project needs gulp to be installed:
**1** Download NodeJs. 
**2** run cmd, or terminal. Type "npm install gulp -g" 

If on Windows: 
**3** 
```
cd /d "Path to my application\with the backward\slashes\before\the\app\folder"
```
Type again "npm install" to grab the dependencies:

## API Reference

run the gulpfile.js:
```javascript
gulp watchSass
```
If you want it to keep track of your changes, OR:

```javascript
gulp injectSass
```
If you want it to run it once. 

## Contributors
You can do whatever you want with the project!!!

## License

MIT LICENSE
Copyright (c) <2016> <David Vega, Jose Asilis>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
