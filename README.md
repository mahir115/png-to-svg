# png-to-svg
a free working png to svg converter without issues and works locally.

it's not useless this time it actually converts any png image to svg without uploading it to a third-party server and works locally and also the svg version looks exactly like the png image so it don't look less graphics.

# why this is better?

1. doesn't upload to any servers which means you don't wait for it to upload it uploads very quickly.
2. the svg version looks exactly the same comparing with the png version unlike other sites makes it less graphics.
3. free and unlimited.
4. open-source so you trust it.

# why doesn't use backend?

1. you make sure your images won't be available anywhere in servers.
2. quick upload and quick download.
3. this service doesn't even require backend servers.

# how to use it?

1. you can download the html file.
2. you can view it's source and even you're free to use it in a website.
3. you can open the html file with your browser and use it.

# how to get the source code?

- you can find html file in the source code and just copy or download it, here is the html just for quick.
````html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>PNG to SVG Converter</title>
  <script src="https://cdn.jsdelivr.net/npm/potrace@2.0.0/potrace.min.js"></script>
  <style>
    body { font-family: sans-serif; margin: 2em; }
    #preview { max-width: 300px; max-height: 300px; display: block; margin-bottom: 1em; }
    #svg-output { display: block; margin-top: 1em; max-width: 300px; max-height: 300px; }
  </style>
</head>
<body>
  <h1>PNG to SVG Converter</h1>
  <input type="file" id="file-input" accept="image/png" />
  <br>
  <img id="preview" src="" alt="Preview" style="display:none;" />
  <br>
  <button id="download-btn" disabled>Download SVG</button>
  <div id="svg-output"></div>
  <script>
    const fileInput = document.getElementById('file-input');
    const preview = document.getElementById('preview');
    const downloadBtn = document.getElementById('download-btn');
    const svgOutput = document.getElementById('svg-output');
    let imgWidth = 0, imgHeight = 0, imgDataUrl = '';

    fileInput.addEventListener('change', function(e) {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(evt) {
        preview.src = evt.target.result;
        preview.style.display = 'block';
        downloadBtn.disabled = false;
        imgDataUrl = evt.target.result;
        // Get image dimensions for SVG
        const tempImg = new Image();
        tempImg.onload = function() {
          imgWidth = tempImg.width;
          imgHeight = tempImg.height;
        };
        tempImg.src = evt.target.result;
      };
      reader.readAsDataURL(file);
    });

    downloadBtn.addEventListener('click', function() {
      if (!imgDataUrl || !imgWidth || !imgHeight) return;
      // Embed the PNG as an <image> in SVG
      const svg = `<svg xmlns="http://www.w3.org/2000/svg" width="${imgWidth}" height="${imgHeight}">
  <image href="${imgDataUrl}" width="${imgWidth}" height="${imgHeight}"/>
</svg>`;
      svgOutput.innerHTML = svg;
      const blob = new Blob([svg], {type: 'image/svg+xml'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'image.svg';
      document.body.appendChild(a);
      a.click();
      setTimeout(() => {
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
      }, 100);
    });
  </script>
</body>
</html>
<style>
body {
    background-color: #121212;
    color: #ffffff;
}
</style>
````
