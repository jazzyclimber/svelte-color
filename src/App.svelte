<script>
	export let color = "ffffff";
  export let bgColor = "#ffffff";
  export let textColor = "#000000";
  export let error = false;
  let lastColor =  "ffffff";
  color = "#" + color;

  function validateColor() {
    let tempColor = color;
    let split = tempColor.split("");
    split[0] == "#" ?   null : tempColor = "#" + tempColor;
    if (tempColor.length == 4 || tempColor.length == 7) {
      bgColor = tempColor;
    }
    return split.length <= 7 ? error = false : error = true;
  }

  function invertColor() {
    let localColor = bgColor;
    if (localColor.indexOf('#') === 0) {
        localColor = localColor.slice(1);
    }
    // convert 3-digit localColor to 6-digits.
    if (localColor.length === 3) {
        localColor = localColor[0] + localColor[0] + localColor[1] + localColor[1] + localColor[2] + localColor[2];
    }
    if (localColor.length !== 6) {
        throw new Error('Invalid color color.');
    }
    var r = parseInt(localColor.slice(0, 2), 16),
        g = parseInt(localColor.slice(2, 4), 16),
        b = parseInt(localColor.slice(4, 6), 16);

    // https://stackoverflow.com/a/3943023/112731
    return (r * 0.299 + g * 0.587 + b * 0.114) > 186
        ? textColor = '#000000'
        : textColor = '#FFFFFF';
}

  function handleInput() {
    validateColor()
    if (error) {
      textColor = "#000000"
      color = "#ffffff";
    } 
    invertColor()
  }
invertColor();
  
</script>

<main style="background-color: {bgColor};">
	<h1 style="color: {textColor};">color Color Display: {bgColor}</h1>
  <input type="text" bind:value={color} on:keyup={handleInput} >
  {#if error }
  <div class="err-msg" style="color: {textColor};">There is an error with your color. Please select new color.</div>
  {/if}
</main>

<style>
	main {
		text-align: center;
		min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transition: background-color .2s ease;
	}

	h1 {
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 700;
    margin-top: 0;

	}

</style>