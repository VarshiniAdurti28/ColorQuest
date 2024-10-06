<script>
  //chroma.js library for the conversions
  import chroma from 'chroma-js';


  // initially set to red 
  let selectedCol ="#ff0000"; 
  let box, sat, val ;
  
  let deg= 0;
  let isDragging = 0;
  let hsvColor=[];
  let hslColor=[];
  

  let rgbCol = '', cmykCol='', hslCol='', hsvCol='', hexCol='';
  

  function Enable(){
    isDragging = 1;
  }

  function Disable(){
    isDragging = 0;
  }
  

  function handleDeg(e){
    deg= e.target.value;
    // console.log(deg);
    const hslValues = hslCol.split(',').map(v => parseFloat(v.trim()));
    
    selectedCol = chroma.hsl(deg, hslValues[1] / 100, hslValues[2] / 100).hex();
  }


  function getCoordinates(e){
    if(!isDragging)return ;
    //X axis gives saturation and Y axis gives value in HSV
    const rect= box.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top ;

    //Calculating saturation and value based on x and y and adjusting them
    //to lie between 0% and 100%
    sat = Math.round((x / box.width) * 100);
    val = Math.round(((box.height - y) / box.height) * 100);

    
    selectedCol = chroma.hsv(deg,  sat/100, val/100).hex();

  

  }



  //converting all values to hex for uniformity
  function handleHex(e) {
    selectedCol = e.target.value;
  }

  function handleRgb(e) {
    selectedCol = chroma(`rgb(${e.target.value})`).hex(); 
  }

  function handleCmyk(e) {
    const cmykValues = e.target.value.split(',').map(v => parseFloat(v.trim()) / 100);
    selectedCol = chroma.cmyk(...cmykValues).hex(); 
  }

  function handleHsl(e) {
    const hslValues = e.target.value.split(',').map(v => parseFloat(v.trim()));
    selectedCol = chroma.hsl(hslValues[0], hslValues[1] / 100, hslValues[2] / 100).hex(); 
    deg = hslValues[0];
  }

  function handleHsv(e) {
    const hsvValues = e.target.value.split(',').map(v => parseFloat(v.trim()));
    selectedCol = chroma.hsv(hsvValues[0], hsvValues[1] / 100, hsvValues[2] / 100).hex();
    deg = hsvValues[0]; 
  }

 
  $: {
   
  
 
  hexCol= selectedCol;
  //RGB
  let rgbColor = chroma(selectedCol).rgb(); 
  rgbCol = `${rgbColor[0]}, ${rgbColor[1]}, ${rgbColor[2]}`;

  //CMYK
  let cmykColor = chroma(selectedCol).cmyk(); 
  cmykCol = `${Math.round(cmykColor[0] * 100)}%, ${Math.round(cmykColor[1] * 100)}%, ${Math.round(cmykColor[2] * 100)}%, ${Math.round(cmykColor[3] * 100)}%`;
  

  // HSV (Black led to NaN value for H: hence that has been taken careof)
  hsvColor = chroma(selectedCol).hsv();
  hsvCol = `${Math.round(isNaN(hsvColor[0]) ? 0 : hsvColor[0])}°, ${Math.round(hsvColor[1] * 100)}%, ${Math.round(hsvColor[2] * 100)}%`;


  // HSL (Black led to NaN value for H: hence that has been taken careof)
  hslColor = chroma(selectedCol).hsl(); 
  hslCol = `${Math.round(isNaN(hslColor[0]) ? 0 : hslColor[0])}°, ${Math.round(hslColor[1] * 100)}%, ${Math.round(hslColor[2] * 100)}%`;

  } 



 
</script>




<style>
  @import './style.css';
</style>

<div class= "colorPicker">
  <h1>Color Picker</h1>
  <div class= "colors">
    <!-- A div to display what color we have chosen! -->
    <div class= "dispColor" style= "--pick-color: {selectedCol}">
      
    </div>

    <!-- Saturation/value picker -->
    <!-- Adding width height attributes describes the internal size of the canvas,
     When not specified box.width, box.height takes up the default width height of the canvas,
     and not the ones specified in css -->

     <!-- Handling drag selector using mousedown, mouseup, mousemove options -->
    <canvas class= "GradSelector" width= 450px height= 250px style= "--grad-color: {hsvColor[0]}" bind:this={box} on:mousedown = {Enable} on:mousemove= {getCoordinates} on:mouseup= {Disable}>
      
    </canvas>
  </div>

  
    <!-- implementing the hue slider  -->
  <div class="hueCont">
    <input type="range" min="0" max="360" bind:value={deg} class="hueSlider" on:input={handleDeg}>
  </div>
  

  <div class= "HexCont">
    <div class="Hex eachInp">
      <label> HEX
        <input type="text" value = {hexCol} on:input={handleHex}>
      </label>
    </div>
  </div>
  


  <div class="colorbar">
    
   
    <div class="eachInp">
      <label> RGB
        <input type="text" value = {rgbCol} on:input={handleRgb} >
      </label>
  
    </div>
  

    <div class="eachInp">
    <label> CMYK
      <input type="text" value = {cmykCol} on:input={handleCmyk} >
    </label>
    </div>

    <div class="eachInp">
      <label> HSV
        <input type="text" value = {hsvCol} on:input={handleHsv} >
      </label>
    </div>

    

    <div class="eachInp">
      <label> HSL
        <input type="text" value = {hslCol} on:input={handleHsl} >
      </label>
    </div>


    
  
   
  </div>
  

 

</div>
 