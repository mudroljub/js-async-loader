# JavaScript Async Loader
#### *load asynchronously, execute consequently*

The simplest possible solution to help you eliminate render-blocking JavaScript.

* No additional library.
* No additional HTTP request.
* Just a little inline script.
* Ideal for Google PageSpeed test.

See it in action: [mudroljub.github.io/js-async-loader](http://mudroljub.github.io/js-async-loader/)

## How to use

* Copy this script to your HTML. 
* Replace the key/value pairs in the `libs` object:

```html
  <script>
    // put all your JS files here, in correct order
    var libs = {
      "jquery": "https://code.jquery.com/jquery-2.1.4.min.js",
      "bxSlider": "https://cdnjs.cloudflare.com/ajax/libs/bxslider/4.2.5/jquery.bxslider.min.js",
      "angular": "https://ajax.googleapis.com/ajax/libs/angularjs/1.5.0-beta.2/angular.min.js",
      "ngAnimate": "https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.5.0-beta.2/angular-animate.min.js"
    };
    var loadedLibs = {};
    var counter = 0;

    var loadAsync = function(lib) {
      var http = new XMLHttpRequest();
      http.open("GET", libs[lib]);
      http.onload = () => {
        loadedLibs[lib] = http.responseText;
        if (++counter == Object.keys(libs).length) startScripts();
      }
      http.send();
    }
    var startScripts = () => {
      for (var lib in libs) eval(loadedLibs[lib]);
      console.log("allLoaded");
    }

    for (var lib in libs) loadAsync(lib);
  </script>
  ```
