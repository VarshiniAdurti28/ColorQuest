<script>
  //chroma.js library for the conversions
  import chroma from 'chroma-js';

  let selectedCol ="#ff0000"; 
  let deg= 0;

  let rgbCol = '', cmykCol='', hslCol='', hsvCol='', hexCol='';
  


  function handleDeg(e){
    deg= e.target.value;
    console.log(deg);
    const hslValues = hslCol.split(',').map(v => parseFloat(v.trim()));
    
    selectedCol = chroma.hsl(deg, hslValues[1] / 100, hslValues[2] / 100).hex();

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
  }

  function handleHsv(e) {
    const hsvValues = e.target.value.split(',').map(v => parseFloat(v.trim()));
    selectedCol = chroma.hsv(hsvValues[0], hsvValues[1] / 100, hsvValues[2] / 100).hex(); 
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
  let hsvColor = chroma(selectedCol).hsv();
  hsvCol = `${Math.round(isNaN(hsvColor[0]) ? 0 : hsvColor[0])}°, ${Math.round(hsvColor[1] * 100)}%, ${Math.round(hsvColor[2] * 100)}%`;


  // HSL (Black led to NaN value for H: hence that has been taken careof)
  let hslColor = chroma(selectedCol).hsl(); 
  hslCol = `${Math.round(isNaN(hslColor[0]) ? 0 : hslColor[0])}°, ${Math.round(hslColor[1] * 100)}%, ${Math.round(hslColor[2] * 100)}%`;

  } 

</script>




<style>
  .colors{
    display: flex;
    flex-direction: row;
 
    height: 150px;
  }

  .dispColor{
    /* used css variable to link the selected Color */
    background-color: var(--pick-color); 
    width: 30%;
    
  }


  .colorbar{
   display: flex;
   flex-direction: column;
    align-items: center;


    padding: 50px;

  }

  .hueCont{
    margin: 20px;
    text-align: center;
  }

  .hueSlider{
    border-width: 5px;
    border-radius: 10px;
    -webkit-appearance: none;
    height: 15px;
    width: 350px;
    background: linear-gradient(to right, hsl(0, 100%, 50%), hsl(60, 100%, 50%), hsl(120, 100%, 50%), hsl(180, 100%, 50%), hsl(240, 100%, 50%), hsl(300, 100%, 50%), hsl(360, 100%, 50%));
  }


  .eachInp{
    padding: 20px;
    
  }

  input{
    width: 300px;
  }

 label{
  cursor: pointer;
 }

/* styling the handle or the thumb of the slider */
 .hueSlider::-webkit-slider-thumb {
  -webkit-appearance: none;
  background-color: rgb(0, 0, 0);
  border-radius: 50%;

  width: 20px;
  height: 20px;
  cursor: pointer;

 }

</style>




<div class="cont">
  <div class= "colors">
    <!-- A div to display what color we have chosen! -->
    <div class= "dispColor" style= "--pick-color: {selectedCol}">
      
    </div>
    <!-- A test para -->
    <!-- <p>You have selected {selectedCol}</p> -->
    <div>
      
    </div>
  </div>

  <!-- implementing the hue slider  -->
  <div class="hueCont">
    <input type="range" min="0" max="360" value={deg} class="hueSlider" on:input={handleDeg}>
  </div>
  

  <div class="colorbar">
    <div class="eachInp">
      <label> HEX
        <input type="text" value = {hexCol} on:input={handleHex}>
      </label>
    </div>
    
   
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