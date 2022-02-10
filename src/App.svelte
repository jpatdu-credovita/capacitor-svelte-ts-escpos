<script lang="ts">
	import { ThermalPrinterPlugin } from 'thermal-printer-cordova-plugin/src';
	declare let ThermalPrinter: ThermalPrinterPlugin;

	export let ip: string, port: string = '9100', text: string;

	function print() {
		ThermalPrinter.printFormattedText({
			type: 'tcp',
			address: ip,
			port: port,
			id: 'tcp-printer-001',
			text: `[L]${text}[R]--`
		}, function() {
			console.log('Successfully printed!');
		}, function(error) {
			console.error('Printing error', error);
		});
	}
</script>

<main>
	<p>IP address</p>
	<input bind:value={ip}>

	<p>Port</p>
	<input bind:value={port}>

	<p>Text</p>
	<textarea rows="20" bind:value={text}></textarea>

	<button on:click={print}>Print</button>

	<pre>{ip}:{port}</pre>
	<pre>{text}</pre>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	pre {
		white-space: pre-wrap;       /* Since CSS 2.1 */
		white-space: -moz-pre-wrap;  /* Mozilla, since 1999 */
		white-space: -pre-wrap;      /* Opera 4-6 */
		white-space: -o-pre-wrap;    /* Opera 7 */
		word-wrap: break-word;       /* Internet Explorer 5.5+ */
	}
</style>