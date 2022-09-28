## [@jasonfleischer/spectrogram](https://www.npmjs.com/package/@jasonfleischer/spectrogram)

A package for displaying a spectrogram. Click [HERE](https://jasonfleischer.github.io/npm-spectrogram-demo/) to see a demo

![Screenshot](https://jasonfleischer.github.io/npm-spectrogram-demo/screenshot/screen.png "Screenshot")

#### Installation
```bash
$ npm i @jasonfleischer/spectrogram
```

#### Usage
``` html
<div id="your_spectrogram_id"></div>
```

``` javascript

// STEP 1. create spectrogram
const Spectrogram = require("@jasonfleischer/spectrogram");

var spectrogram = new Spectrogram(id = "your_spectrogram_id", useHeatMapColors = true, highlightPeaks = false, darkMode = true, minimumFrequency = 0, maximumFrequency = 22050 );

// STEP 2. build analyzerNode
var ctx = new AudioContext();
var analyzerNode = audio_controller.ctx.createAnalyser();
analyzerNode.smoothingTimeConstant = 0;
analyzerNode.fftSize = fftSize;

// STEP 3. request microphone access
navigator.mediaDevices.getUserMedia({ video: false, audio: true })
  	.then( (mediaStreamObj) => {
  		onStreamAquired(mediaStreamObj);
		var sourceNode = ctx.createMediaStreamSource(mediaStreamObj);
		sourceNode.connect(analyzerNode);
		spectrogram.draw(analyzerNode, ctx.sampleRate);
	})
	.catch( (err) => {
	 	console.log("getUserMedia: " + err);
	});

// ---- OR ----

// STEP 3. setup audio element
audio_controller.audioElement = document.createElement("your_audio-element_id");
audio_controller.audioElement.src = "audio/your_audio_path.mp3";			
audio_controller.audioElement.oncanplay = function () { 
	var mediaStreamObj = audio_controller.audioElement.captureStream();
	onStreamAquired(mediaStreamObj);
}

// STEP 4. connect spectrogram
function onStreamAquired(mediaStreamObj) {
	var sourceNode = ctx.createMediaStreamSource(mediaStreamObj);
	sourceNode.connect(analyzerNode);
	spectrogram.draw(analyzerNode, ctx.sampleRate);
}

// Additional commands

spectrogram.resume();
spectrogram.pause();

```

#### Sample Projects

- [Demo](https://jasonfleischer.github.io/npm-spectrogram-demo/)
- [Spectrogram](https://jasonfleischer.github.io/spectrogram/)
