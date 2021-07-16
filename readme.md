## AssetManager

- Loads and unloads image, video, audio and data assets
- Centralizes asset management
- Reduces memory consumption
- Easy to use
- No dependencies

### Installation
```shell
npm add @mediamonks/assetmanager
```

### Usage
```javascript
import assetManager from '@mediamonks/assetmanager';

// loading a single file
assetManager.load('https://catpics.com/cat.png');

// loading multiple files
assetManager.load(['meow.mp3', 'wavs/lol.wav']);

// loading into a namespace
assetManager.load(['data/data.json', 'videos/video.mp4'], 'main');

// loading with progress callback
assetManager.load(allTheFiles, progress => {
    console.log(`${Math.floor(progress * 100)}%`);
});

// loading into a namespace with progress callback
assetManager.load(catMediaFiles, 'catMedia', progress => {
    console.log(`${Math.floor(progress * 100)}%`);
});


// using an image asset
image.src = assetManager.get('https://catpics.com/cat.png'); // returns HTMLImageElement

// using a video asset
video.src = assetManager.get('videos/video.mp4'); // returns object URL

// using an audio asset
const audioContext = new AudioContext();
const source = audioContext.createBufferSource();
source.buffer = assetManager.get('meow.mp3'); // returns AudioBuffer
source.start();

// using a data asset
const data = assetManager.get('data/data.json'); // returns Object


// unloading a single file
assetManager.release('meow.mp3');

// unloading multiple files
assetManager.release(['meow.mp3', 'lol.wav']);

// unloading a namespace
assetManager.release('main');

// unloading everything
assetManager.release();
```

Note: Keep in mind that garbage collection can't actually free up the memory unless the asset is no longer referenced anywhere, so make sure you also unset any variables, properties and DOM references that point to the asset.
When using a modern framework, this means that as long as you keep all your references to an asset within a component and properly scope your variables, destroying the component should take care of this.

### In Vue.js
```javascript
import assetManager from '@mediamonks/assetmanager';

Vue.use(assetManager, {
	root: 'assets/' // optional. specifies a root path to be prefixed to all relative paths
});
```

#### Loading/using/unloading in a component
```javascript
this.$assets.load(['image.png', 'data.json']);

const { value } = this.$assets.get('data.json');

this.$assets.release('data.json');
```

#### Using in a template
```vue
<img :src="$assets.get('images/image.png')" />
```
