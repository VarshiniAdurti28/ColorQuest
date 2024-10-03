<script>
  //chroma.js library for the conversions
  import chroma from 'chroma-js';

  let selectedCol ="#522828"; 
  let rgbCol = '', cmykCol='', hslCol='', hsvCol='', hexCol='';
  


 
  $: {
  
  //HEX: Our selected Color is in Hex
  hexCol= chroma(selectedCol).hex();

  //RGB
  let rgbColor = chroma(selectedCol).rgb(); 
  rgbCol = `${rgbColor[0]}, ${rgbColor[1]}, ${rgbColor[2]}`;

  //CMYK
  let cmykColor = chroma(selectedCol).cmyk(); 
  cmykCol = `${Math.round(cmykColor[0] * 100)}%, ${Math.round(cmykColor[1] * 100)}%, ${Math.round(cmykColor[2] * 100)}%, ${Math.round(cmykColor[3] * 100)}%`;
  }

  // HSV
  let hsvColor = chroma(selectedCol).hsv();
  hsvCol = `${Math.round(hsvColor[0])}°, ${Math.round(hsvColor[1] * 100)}%, ${Math.round(hsvColor[2] * 100)}%`;


  // HSL
  let hslColor = chroma(selectedCol).hsl(); 
  hslCol = `${Math.round(hslColor[0])}°, ${Math.round(hslColor[1] * 100)}%, ${Math.round(hslColor[2] * 100)}%`;

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
        <input type="text" bind:this = {selectedCol} value = {hexCol} on:input={()=> selectedCol= hexCol}>
      </label>
    </div>
    
   
    <div class="eachInp">
      <label> RGB
        <input type="text" bind:this = {selectedCol} value={rgbCol} on:input={()=> selectedCol= rgbCol}>
      </label>
  
    </div>
  

    <div class="eachInp">
    <label> CMYK
      <input type="text" bind:this = {selectedCol} value={cmykCol} on:input={()=> selectedCol= cmykCol}>
    </label>
    </div>

    <div class="eachInp">
      <label> HSV
        <input type="text" bind:this = {selectedCol} value={hsvCol} on:input={()=> selectedCol= hsvCol}>
      </label>
    </div>

    

    <div class="eachInp">
      <label> HSL
        <input type="text" bind:this = {selectedCol} value={hslCol} on:input={()=> selectedCol= hslCol}>
      </label>
    </div>


    
  
   

  </div>
</div>