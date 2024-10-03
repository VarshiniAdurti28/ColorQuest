<script>
  //chroma.js library for the conversions
  import chroma from 'chroma-js';

  let selectedCol ="#4340a3"; 
  let rgbCol = '', cmykCol='', hslCol='', hsvCol='', hexCol='';
  


 
  $: {

  //HEX: Our selected Color is in Hex
  hexCol= selectedCol;

  //RGB
  let rgbColor = chroma(selectedCol).rgb(); 
  rgbCol = `${rgbColor[0]}, ${rgbColor[1]}, ${rgbColor[2]}`;

  //CMYK
  let cmykColor = chroma(selectedCol).cmyk(); 
  cmykCol = `${Math.round(cmykColor[0] * 100)}%, ${Math.round(cmykColor[1] * 100)}%, ${Math.round(cmykColor[2] * 100)}%, ${Math.round(cmykColor[3] * 100)}%`;
  }

   // HSL
  let hslColor = chroma(selectedCol).hsl(); 
  hslCol = `${Math.round(hslCol[0])}°, ${Math.round(hslCol[1] * 100)}%, ${Math.round(hslCol[2] * 100)}%`;

  // HSV
  let hsvColor = chroma(selectedCol).hsv();
  hsvCol = `${Math.round(hsvColor[0])}°, ${Math.round(hsvColor[1] * 100)}%, ${Math.round(hsvColor[2] * 100)}%`;

</script>




<style>
  .colors{
    display: flex;
    flex-direction: row;
    /* background-color: green; */
    height: 150px;
  }

  .dispColor{
    background-color: var(--pick-color);
    width: 30%;
    
  }


  .colorbar{
   display: flex;
   flex-direction: column;
    align-items: center;


    padding: 50px;

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

</style>




<div class="cont">
  <div class= "colors">
    <div class= "dispColor" style= "--pick-color: {selectedCol}">

    </div>
    <div>
      
    </div>
  </div>
  

  <div class="colorbar">
    <div class="eachInp">
      <label> HEX
        <input type="text" bind:value = {hexCol}>
      </label>
    </div>
    
    <div class="eachInp">
      <label> HSV
        <input type="text" bind:value = {hsvCol}>
      </label>
    </div>
    

    <div class="eachInp">
      <label> HSL
        <input type="text" bind:value = {hslCol} >
      </label>
    </div>
    

    <div class="eachInp">
    <label> CMYK
      <input type="text" bind:value = {cmykCol}>
    </label>
    </div>


    <div class="eachInp">
    <label> RGB
      <input type="text" bind:value = {rgbCol}>
    </label>

    </div>

  
   

  </div>
</div>