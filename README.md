## [@jasonfleischer/spectrogram](https://www.npmjs.com/package/@jasonfleischer/spectrogram)

A package for displaying a spectrogram. A spectrogram is a visual representation of the spectrum of frequencies of a signal as it varies with time. Click [HERE](https://jasonfleischer.github.io/npm-spectrogram-demo/) to see a demo.

![Screenshot](https://jasonfleischer.github.io/npm-spectrogram-demo/screenshot/screen.png "Screenshot")

#### Installation
```bash
$ npm i @jasonfleischer/spectrogram
```

#### Usage
``` html
<div style="width: 500px; height: 320px" id="your_spectrogram_id"></div>

<button id="your_button_id">Start</button>

```

``` javascript

// STEP 1. create spectrogram
const Spectrogram = require("@jasonfleischer/spectrogram");

var spectrogram = new Spectrogram(id = "your_spectrogram_id", useHeatMapColors = true, highlightPeaks = false, darkMode = true, minimumFrequency = 0, maximumFrequency = 22050 );

var audioContext = {};

document.getElementById("your_button_id").onclick = onStartClickEvent;

function onStartClickEvent(){

	// STEP 2. build analyzerNode
	audioContext = new AudioContext();
	var analyzerNode = audioContext.createAnalyser();
	analyzerNode.smoothingTimeConstant = 0;
	analyzerNode.fftSize = 1024;

	// STEP 3. request microphone access
	navigator.mediaDevices.getUserMedia({ video: false, audio: true })
	  	.then( (mediaStreamObj) => {
	  		onStreamAquired(mediaStreamObj, analyzerNode);
		})
		.catch( (err) => {
		 	console.log("getUserMedia: " + err);
		});

	// ---- OR ----

	// STEP 3. setup audio element
	/*var audioElement = document.createElement("AUDIO");
	audioElement.src = "audio/your_audio_file.mp3";		
	audioElement.autoplay = true;	
	audioElement.oncanplay = function () { 
		var mediaStreamObj = audioElement.captureStream();
		onStreamAquired(mediaStreamObj, analyzerNode);
	}*/
}

// STEP 4. connect spectrogram
function onStreamAquired(mediaStreamObj, analyzerNode) {
	var sourceNode = audioContext.createMediaStreamSource(mediaStreamObj);
	sourceNode.connect(analyzerNode);
	spectrogram.draw(analyzerNode, audioContext.sampleRate);
}

// Additional commands

/*spectrogram.resume();
spectrogram.pause();*/

```

#### Sample Projects

- [Demo](https://jasonfleischer.github.io/npm-spectrogram-demo/)
- [Spectrogram website](https://jasonfleischer.github.io/spectrogram/)
