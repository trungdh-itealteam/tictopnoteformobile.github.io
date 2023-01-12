# ITL Drawer widget

Plugin of drawing editor for web application

## How to use

**Step 1: Import javascript file**

```
<script type="text/javascript" src="path_to/drawer-widget.js"></script>
```

**Step 2: Add HTML**

```
<div style="height: 500px">
  <itl-drawer></itl-drawer>
</div>
```

## Supported functions

```
const drawer = document.querySelector('itl-drawer');
```

**1. setDrawerOptions(options: DrawerOptions)**

- Set drawer options

```
export interface DrawerOptions {
    imagePasteRatio?: number;
    viewOnly?: boolean;
}
```

###### imagePasteRatio

- Set maximum size of image when pasting to drawer
- Default = 0.75, ratio with container
- Set = 0 to keep original image size

###### viewOnly

- Set drawer is view only or editable
- Default = false

**2. loadObjects(json)**

- Load canvas objects from JSON objects

```
const json = {objects: [....]}

drawer.loadObjects(json);
```

**3. pasteImage(img)**

- Draw image from clipboard

```
document.onpaste = function(event){
  var items = (event.clipboardData || event.originalEvent.clipboardData).items;
  
  for (index in items) {
    var item = items[index];
	
    if (item.kind === 'file') {
      var blob = item.getAsFile();   

      drawer.pasteImage(blob);
    }
  }
}
```

**4. addAudio(audio: File | string)**

- Add audio file to drawer

```
const audio = new File([], 'myaudio.wav');
// OR
const audio = 'path/to/audio.wav';

drawer.addAudio(audio);
```

**4. getAsObjects()** : JSON

- Get canvas data as JSON objects

```
const canvasData = drawer.getAsObjects();
```

**5. getAsImageData(options?: ImageDataOptions)** : string base64

- Get canvas data as image data

```
export interface ImageDataOptions {
  keepOriginalSize?: boolean;
  paddingContent?: number;
}
```

###### keepOriginalSize

- Keep drawer original size
- Default = false

###### paddingContent

- Only if keepOriginalSize = false
- Crop an image bounding only drew objects with a padding
- Default = 30 (px)

## Supported events

**1. imageAddClick**

```
drawer.addEventListener('imageAddClick', () => {
});
```

**2. audioAddClick**

```
drawer.addEventListener('audioAddClick', () => {
});
```

**3. audioDbClick**

```
drawer.addEventListener('audioDbClick', (event) => {
  console.log(event.detail) // audioUrl here
});
```

**4. hasChange**

```
drawer.addEventListener('hasChange', (event) => {
  console.log(event.detail)
});
```
