# Hosting maximilian.js 

If you want to run [maximilian.js](https://mimicproject.com/guides/maximJS) (the Web Audio version of [maximilian](https://github.com/micknoise/Maximilian) )on something other than the mimicproject.com website, you've come to the right place.

To do thus, you will need to access following 4 files.

* ``maximilian.v.0.1.js``

* ``index.mjs``

* ``ringbuf.js``

* ``maxi-processor.js``

There are some specfic headers related to [SharedArrayBuffers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer#security_requirements) that mean serving these will only work under certain circumstances. We give examples of either running this fully locally serving the files yourself, or using the versions hosted on mimicproject.com

## Running on GitHub Pages

You can see a demo of this repository running [here](https://louismac.github.io/maximilian-js-local/)

Include the libraries, and also the ``enable-threads.js`` file (this injects in some headers and is neccessary to get this to work when you are not in control of how the page is served)

```
<script crossorigin src = "./maximilian.v.0.1.js"></script>
<script crossorigin src = "./enable-threads.js"></script>
```

Tell ``maximilian.js`` where to find libraries. You can put in the url of **your own GitHub pages repo**.

```
let maxi;
initAudioEngine("https://louismac.github.io/maximilian-js-local").then((dspEngine)=>{
  maxi = dspEngine;
  //Get audio code from script element
  maxi.setAudioCode("myAudioScript");
})
```

## Running Locally

To run on your local machine 

### Use libraries hosted on mimicproject.com

If you have access to the internet whilst running libraries, this may be the best option.

Include the libraries

``<script crossorigin src = "https://mimicproject.com/libs/maximilian.v.0.1.js"></script>``

Tell ``maximilian.js`` where to find libraries

```
let maxi;
initAudioEngine("https://mimicproject.com/libs").then((dspEngine)=>{
  maxi = dspEngine;
  //Get audio code from script element
  maxi.setAudioCode("myAudioScript");
})
```

You can change the urls appropriately if you are hosting elsewhere

### Running on p5.js Web Editor 

You can see can example [here](https://editor.p5js.org/Louismac/sketches/odTpTQuv1)

Include the hosted library in the ``index.html``

```
<script crossorigin src = "https://mimicproject.com/libs/maximilian.v.0.1.js"></script>
```

Run the code in the ``sketch.js``

```
let maxi;
initAudioEngine("https://mimicproject.com/libs").then((dspEngine)=>{
  maxi = dspEngine;
  //Get audio code from script element
  maxi.setAudioCode(`
    var osc1 = new Maximilian.maxiOsc();
    var osc2 = new Maximilian.maxiOsc();
    function play() {
      return osc1.saw(100) + osc2.saw(100.2)
    }
  `);
})
```

### Locally hosted library

The recommended way to do this is to use the python server we have provided (server.py).

Then when in the project folder in the terminal run the command below.

``python server.py``

This serves the files in the folder at ``http://localhost:4200`` and adds a header to get around CORS issues.

Include the libraries

``<script crossorigin src = "./maximilian.v.0.1.js"></script>``

Tell ``maximilian.js`` where to find libraries

```
let maxi;
initAudioEngine("http://localhost:4200").then((dspEngine)=>{
  maxi = dspEngine;
  //Get audio code from script element
  maxi.setAudioCode("myAudioScript");
})
```

### Run demo locally!

Download this repo. Then when in the project folder in the terminal run the command below.

``python server.py``

Then all you need to do is visit ``http://localhost:4200`` to see the demo running
