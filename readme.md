## Simple Asset Manager (SAM)

- Load and unload image, video, audio and data assets
- Reduces memory consumption
- Easy to use
- No dependencies

### Installation
```shell
npm install simple-asset-manager
```

### Usage
```ecmascript 6
import sam from 'simple-asset-manager';

// loading a single file
sam.load('https://catpics.com/cat.png');

// loading multiple files
sam.load(['meow.mp3', 'lol.wav']);

// loading into a namespace
sam.load(['data/data.json', 'videos/video.mp4'], 'main');

// loading with progress callback
sam.load(aLotOfFiles, progress => {
    console.log(`${Math.floor(progress * 100)}%`);
});

// loading into a namespace with progress callback
sam.load(allTheFiles, 'files', progress => {
    console.log(`${Math.floor(progress * 100)}%`);
});


// using an image asset
image.src = sam.get('https://catpics.com/cat.png'); // returns HTMLImageElement

// using a video asset
video.src = sam.get('videos/video.mp4'); // returns object URL

// using an audio asset
const audioContext = new AudioContext();
const source = audioContext.createBufferSource();
source.buffer = sam.get('meow.mp3'); // returns AudioBuffer
source.start();

// using a data asset
const data = sam.get('data/data.json'); // returns Object


// unloading a single file
sam.release('meow.mp3');

// unloading multiple files
sam.release(['meow.mp3', 'lol.wav']);

// unloading a namespace
sam.release('main');

// unloading everything
sam.release();
```

### In Vue.js
```ecmascript 6
import sam from 'simple-asset-manager';

Vue.use(sam, { root: 'assets/' });
```

#### Loading/using/unloading in a component
```ecmascript 6
this.$assets.load(['image.png', 'data.json']);

const { value } = this.$assets.get('data.json');

this.$assets.release('data.json');
```

#### Using in a template
```vue
<img :src="$assets.get(...)" />
```
