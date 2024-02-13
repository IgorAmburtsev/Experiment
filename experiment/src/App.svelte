<script>
	// @ts-nocheck

	import { onMount } from "svelte";

	let x = 300;
	let y = 300;
	let zoom = 1;
	let scale = 1;
	let zoomComp;
  let square;
  let intervaled = false
  let mousepos


  const handleClick = () => {
    // intervaled = !intervaled
    // const posBlockX = zoomComp.getBoundingClientRect().x
    // const posBlockY = zoomComp.getBoundingClientRect().y
    // const posX = square.getBoundingClientRect().x
    // const posY = square.getBoundingClientRect().y
    // zoomComp.style.transform = `scale(${2})`;
    console.log(zoomComp.offsetTop)
    console.log(zoomComp.offsetLeft)
    console.log(square.offsetTop)
    console.log(square.offsetLeft)
    // console.log(zoom.clientX)
   
  }
		// square

  // const dblclick = () => {
  //   moving = setInterval(() => {
  //   movingFn()
	// }, 1000);
  // }

	const scrollFunc = (e) => {
		scale += e.deltaY * -0.0001;
		zoomComp.style.transform = `scale(${scale})`;
	};

  const movingFn = () => {
		x = Math.min(550, Math.max(50, x + (Math.random() < 0.5 ? -25 : 25)));
		y = Math.min(550, Math.max(50, y + (Math.random() < 0.5 ? -25 : 25)));
  }

	setInterval(() => {
    if (!intervaled) {
      movingFn()
    }
	}, 1000);

  // $:

  $: if (zoomComp && (x || y)) {
    handleClick()
  }

  $: console.log(mousepos)

  // $: if (intervaled === false) {
  //   moving = setInterval(() => {
  //     movingFn()
  //   }, 1000);
  // }
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="bounding">
  <div class="vertical" />
  <div class="horizontal" />
</div>
<div class="zooms" on:mousewheel={(e) => scrollFunc(e)} bind:this={zoomComp} on:mousemove={(e) => mousepos = e}>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="square" on:click={(e) => handleClick(e)} style={`left: ${x - 25}px; top: ${y - 25}px`} bind:this={square}></div>
</div>

<style>

  .bounding {
    position: absolute;
    width: 100%;
    height: 100%;
    /* border: 1px solid blue; */
    top: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    left: 0;
  }

  .vertical {
    position: absolute;
    width: 100%;
    border: 1px solid yellow;
  }

  .horizontal {
    width: 100%;
    transform: rotate(90deg);
    border: 1px solid yellow;
  }

	.zooms {
		transition: 0.3s ease;
    border: 1px solid red;
    width: 600px;
    position: relative;
    height: 600px;
    -ms-overflow-style: none;
    scrollbar-width: none;
    overflow-y: scroll;
	}

  .zooms::-webkit-scrollbar {
    display: none;
  }

	.container {
		position: relative;
		width: 600px;
		height: 600px;
		/* border: 1px solid lime; */
	}

  .container::-webkit-scrollbar {
    display: none;
  }

	.square {
		position: absolute;
		width: 50px;
		height: 50px;
		background-color: red;
		transition: transform 0.5s;
		transform-origin: center;
		transition: 0.1s ease;
    z-index: 10;
		/* transform: translate(-50%, -50%) scale(2); */
	}
</style>
