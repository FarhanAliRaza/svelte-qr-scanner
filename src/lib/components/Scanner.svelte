<script>
	import { Html5Qrcode } from 'html5-qrcode';

	import { onDestroy, onMount } from 'svelte';
	export let scanner;
	let reader;

	export let classes = '';

	export let cameraView = 'environment';
	export let fps = 10;

	export let onScanSuccess = function (decodedText, decodedResult) {
		// handle the scanned code as you like, for example:
		console.log(`Code matched = ${decodedText}`, decodedResult);
	};

	function onScanFailure(error) {
		// console.warn(`Code scan error = ${error}`);
	}

	export let qrboxFunction = function (viewfinderWidth, viewfinderHeight) {
		let minEdgePercentage = 0.7; // 70%
		let minEdgeSize = Math.min(viewfinderWidth, viewfinderHeight);
		let qrboxSize = Math.floor(minEdgeSize * minEdgePercentage);
		return {
			width: qrboxSize,
			height: qrboxSize
		};
	};

	function init() {
		Html5Qrcode.getCameras()
			.then((devices) => {
				if (devices && devices.length) {
					scanner = new Html5Qrcode('reader');
					scanner.start(
						{ facingMode: cameraView },
						{ fps: fps, qrbox: qrboxFunction },
						onScanSuccess,
						onScanFailure
					);
				}
			})
			.catch((err) => {
				console.log(err);
				alert(err);
			});
	}

	onMount(() => {
		init();
	});

	function onClose() {
		if (scanner) {
			let state = scanner.getState();
			console.log(state);
			if (state == 1) {
				// not started
				scanner.clear();
			}
			if (state == 3) {
				// paused
				scanner.stop().then((_) => {});
			}
			if (state == 2) {
				// scanning
				scanner.stop().then((_) => {});
			}
			if (state == 0) {
				// unknown
			}
		}
	}
</script>

<div class={classes} bind:this={reader} id="reader" />
