
<script>
	import P5Canvas from "./P5Canvas.svelte";
	import AudioPlayer, { stopAll } from './AudioPlayer.svelte';
	// import sketch from './sketch1.svelte'

	let sketch = function(p5) {

		let xspacing = 10;	// space between samples
		let w;				// width
		let numwaves = 10;

		let theta = 0.0;
		let amplitude;
		let dx;
		let yvalues;

		p5.preload = () => {
			amplitude = new Array(numwaves); // Height of wave
			// Value for incrementing X, to be calculated
			// as a function of period and xspacing
			dx = new Array(numwaves);
			// Using an array to store height values
			// for the wave (not entirely necessary)
			yvalues = new Array(120);			// FIXME

		};

		p5.setup = () => {
			p5.createCanvas(window.innerWidth- 20, 500);
			p5.frameRate(30);					// FIXME
			w = p5.width + 16;
			
			for (let i = 0; i < numwaves; i++)
			{
				amplitude[i] = p5.random(10,30);
				let period = p5.random(100, 110);	// FIXME
				dx[i] = (p5.TWO_PI / period) * xspacing;
			}

		};

		p5.calcWave = () => {
		  // Increment theta (try different values
		  // for 'angular velocity' here
		  theta += 0.02;

		  // Set all height values to zero
		  for (let i = 0; i < yvalues.length; i++) {
		    yvalues[i] = 0;
		  }

		  // Accumulate wave height values
		  for (let j = 0; j < numwaves; j++) {
		    let x = theta;
		    for (let i = 0; i < yvalues.length; i++) {
		      // Every other wave is cosine instead of sine
		      if (j % 2 == 0) yvalues[i] += p5.sin(x) * amplitude[j];
		      else yvalues[i] += p5.cos(x) * amplitude[j];
		      x += dx[j];
		    }
		  }
		};


		p5.renderWave = () => {
		  // A simple way to draw the wave with an ellipse at each location

		};

		p5.draw = () => {
		  p5.background(0,122,122);
		  p5.calcWave();

		  // p5.noStroke();
		  // p5.fill(255, 50);
		  // p5.ellipseMode(CENTER);
		  // p5.rect(10,10,10,10);
		  for (let x = 0; x < yvalues.length; x++) {
		    // p5.rect(x * xspacing, 100, 16, 16);
		    p5.rect(x * xspacing, p5.height / 2 + yvalues[x], 5, 5);
		  }
		};

		// reset board when mouse is pressed
		p5.mousePressed = () => {
		// p5.init();
		};

	};
</script>

<style>
  
  main { font-family: sans-serif; background-color: #00000F; 
  	margin: auto;
  	width: 50%;
  	padding: 5em;
  }

  div { color: #d3d3ff; }

</style>

<main>
	<div>
		<h1>Landing Page</h1>
		  <P5Canvas sketch={sketch}/>

	</div>
	
	<!-- https://musopen.org/music/43683-requiem-in-d-minor-k-626/ -->
	<AudioPlayer
		src="https://sveltejs.github.io/assets/music/mozart.mp3"
		title=""
		composer="Wolfgang Amadeus Mozart"
		performer="Markus Staab"
	/>
</main>


