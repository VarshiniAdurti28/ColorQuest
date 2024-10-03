<script>
  let hexCont, hsvCont, hslCont, cmykCont;
  let rgbCont= "rgb(0, 0, 0)";

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

 label{
  cursor: pointer;
 }

</style>




<div class="cont">
  <div class= "colors">
    <div class= "dispColor" style= "--pick-color: {rgbCont}">

    </div>
    <div>
      
    </div>
  </div>
  

  <div class="colorbar">
    <div class="eachInp">
      <label> HEX
        <input type="text" bind:value = {hexCont}>
      </label>
    </div>
    
    <div class="eachInp">
      <label> HSV
        <input type="text" bind:value = {hsvCont}>
      </label>
    </div>
    

    <div class="eachInp">
      <label> HSL
        <input type="text" bind:value = {hslCont} >
      </label>
    </div>
    

    <div class="eachInp">
    <label> CMYK
      <input type="text" bind:value = {cmykCont}>
    </label>
    </div>


    <div class="eachInp">
    <label> RGB
      <input type="text" bind:value = {rgbCont}>
    </label>

    </div>

  
   

  </div>
</div>