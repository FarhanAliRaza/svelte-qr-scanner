# Svelte Qr Scanner

Everything you need to build a qr scanner, powered by [`html5-qrcode`](https://github.com/mebjas/html5-qrcode).

## Getting Started

```svelte
<script>
    import {Scanner} from "svelte-easy-qr";

    //default
const onScanSuccess = function (decodedText, decodedResult) {
		// handle the scanned code as you like, for example:
		console.log(`Code matched = ${decodedText}`, decodedResult);
	};
 //default
const qrboxFunction = function (viewfinderWidth, viewfinderHeight) {
		let minEdgePercentage = 0.7; // 70%
		let minEdgeSize = Math.min(viewfinderWidth, viewfinderHeight);
		let qrboxSize = Math.floor(minEdgeSize * minEdgePercentage);
		return {
			width: qrboxSize,
			height: qrboxSize
		};
	};
 //default
const cameraView = 'environment'; // user | environment
 //default
const fps = 10;


<script>


<Scanner classes="someclass" // some styling
{onScanSuccess}
{qrboxFunction}
{cameraView}
{fps}

/>


```

## Customization

You can customize scanner according to the documentation [`html5-qrcode`](https://scanapp.org/html5-qrcode-docs/docs/apis/classes/Html5Qrcode)

```svelte

<script>
    import {Scanner} from "svelte-easy-qr";
    let scanner;

    //default
const onScanSuccess = function (decodedText, decodedResult) {
		// handle the scanned code as you like, for example:
		console.log(`Code matched = ${decodedText}`, decodedResult);
        scanner.stop()
	};
 //default
const qrboxFunction = function (viewfinderWidth, viewfinderHeight) {
		let minEdgePercentage = 0.7; // 70%
		let minEdgeSize = Math.min(viewfinderWidth, viewfinderHeight);
		let qrboxSize = Math.floor(minEdgeSize * minEdgePercentage);
		return {
			width: qrboxSize,
			height: qrboxSize
		};
	};
 //default
const cameraView = 'environment'; // user | environment
 //default
const fps = 10;




<script>


<Scanner classes="someclass" // some styling
{onScanSuccess}
{qrboxFunction}
{cameraView}
{fps}
bind:scanner={scanner}

/>



```

You can contribute and report issues at [Github](https://github.com/FarhanAliRaza/svelte-simple-forms).
