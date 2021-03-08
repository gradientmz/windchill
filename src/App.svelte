<!-- Hello! This is my take on a windchill calculator.
Windchill is what tempurature it feels like outside accounting for wind.
Below contains the forumlas for calculating windchill values in metric and imperial (c/kph, f/mph)

This was my first project using Svelte! Completed 3/7/2021 -->

<script>
	var system = "metric";
	var windchillresult = 0;
	var temp = "";
	var speed = "";
	
	function windchill() {
		if (system == "metric") {
			var formulametric = `13.12+0.6215${temp}-11.37*${speed}^0.16+0.3965*${temp}*${speed}^0.16`
			windchillresult = math.round(math.evaluate(formulametric), 2)
		}
		else if (system == "imperial") {
			var formulaimperial = `35.74+0.6215${temp}-35.75*${speed}^0.16+0.4275*${temp}*${speed}^0.16`
			windchillresult = math.round((math.evaluate(formulaimperial)*(9/5)+32), 2)
		}
		console.log("Windchill triggered!")
		console.log(windchillresult)
	}
</script>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Mono&display=swap');
	body {
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		font-family: 'Ubuntu Mono', monospace;
		background-color: aliceblue;
		font-size: 1.5rem;
		background-image: url("https://i.ibb.co/rGkGwp0/sky.jpg");
		background-size: cover;
		background-position: 50% 50%;
		background-repeat: no-repeat;
		overflow: hidden;
	}
	input {
		border-radius: 0.75rem;
		text-align: center;
		font-size: 1.5rem;
		transition: 0.2s;
		width: 75%;
		max-width: 40rem;
	}
	container {
		border-radius: 1.5rem;
		border: 0.2rem solid #E1E1E2;
		width: 80vw;
		max-width: 100rem;
		padding-top: 5vh;
		padding-bottom: 5vh;
		background-color: white;
		box-shadow: #2E4797 0px 10px 40px 0px;
		font-size: 1.5rem;
		transition: 0.2s;
	}
	.buttoncontainer {
		margin: auto;
		width: 75%;
		max-width: 40rem;
		display: flex;
	}
	.codetext {
		display: block;
		font-size: 1.25rem;
		color: #79A8D8;
		white-space: nowrap; 
  	overflow: hidden;
 		text-overflow: ellipsis;
		margin: 0rem 1rem;
	}
	.systembutton {
		flex-grow: 2;
		flex-basis: 2rem;
		padding: 0.5rem 1rem;
		border-radius: 0.75rem;
		transition: 0.2s;
		font-size: 1.5rem;
		
		white-space: nowrap; 
  	overflow: hidden;
 		text-overflow: ellipsis;
	}
	.systembutton:active {
		color: white;
		background-color: #396691;
	}
	.calculate {
		width: 75%;
		max-width: 40rem;
		border: 1px solid #63bcd6;
		background-color: #8AE5FF;
		transition: 0.2s;
		border-radius: 0.75rem;
	}
	.calculate:active {
		background-color: #53afc9;
	}
	.active {
		background-color: #5A94CB;
		border: 1px solid #4275a6;
		color: white;
	}
	button:first-child {
		margin-right: 0.75rem;
	}
	.fas.fa-location-circle {
		font-size: 2.25rem;
		color: #0050A0;
		margin: 0;
		margin: 1.25rem;
		transition: 0.2s;
	}
	.fas.fa-location-circle:hover {
		color: #2f7ac4;
	}
	.title {
		font-size: 3rem;
		font-weight: bold;
		color: #4875B7;
		margin: 0rem 1rem;
		white-space: nowrap; 
  	overflow: hidden;
 		text-overflow: ellipsis;
	}
	.subtitle {
		margin: 0.5rem 0rem 2rem 0rem;
		font-weight: normal;
		color: #B0C5DA;
		white-space: nowrap; 
  	overflow: hidden;
 		text-overflow: ellipsis;
		margin: 0.5rem 1rem 0rem 1rem;
	}
	.output {
		font-weight: normal;
		color: gray;
		font-size: 2rem;
		white-space: nowrap; 
  	overflow: hidden;
 		text-overflow: ellipsis;
		margin: 2rem;
	}
</style>

<body>
	<head>
		<script src="https://unpkg.com/mathjs@9.2.0/lib/browser/math.js"></script>
		<script src="https://kit.fontawesome.com/1304ec19c5.js" crossorigin="anonymous"></script>
		<script src="https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.7.0/vanilla-tilt.min.js"></script>
	</head>
<container data-tilt data-tilt-scale="1.05" data-tilt-perspective="2000">
	<h1 class="title">Windchill</h1>
	<h4 class="subtitle">
		By Mark Zhou
	</h4>
	<i class="fas fa-location-circle"></i>
	<div>
		<input
			placeholder="Tempurature"
			bind:value={temp}/>
	</div>
	<div>
		<input 
			placeholder="Wind Speed"
			bind:value={speed}/>
	</div>
	<div class="buttoncontainer">
		<button
			class="systembutton"
			class:active="{system === "metric"}"
			on:click="{() => system = "metric"}">
		Metric
		</button>
		<button
			class="systembutton"
			class:active="{system === "imperial"}"
			on:click="{() => system = "imperial"}">
		Imperial
		</button>
	</div>
	<button
			class="calculate"
			on:click="{windchill}">
		Calculate
		</button>
	<h2 class="output">
		{#if system == "metric"}
			Windchill: {windchillresult}c
		{/if}
		{#if system == "imperial"}
			Windchill: {windchillresult}f
		{/if}
	</h2>
	<a class="codetext" href="https://svelte.dev/repl/148566d93a8948eb9b6e9f79500e4d97?version=3.35.0">The code (with formula!)</a>
</container>	
</body>