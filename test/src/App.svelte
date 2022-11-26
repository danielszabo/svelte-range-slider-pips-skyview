<script>

  import RangeSlider from "../../src/RangeSlider.svelte";

  let disabled = false;

  let effort = {
    start   : 5,
    stop    : 95,
    percent : 50,
    title   : "This is my title",
  };

  let rangeValues = [effort.start,effort.stop];
  let percValue   = [effort.percent];

  let min     = 0;
  let max     = 100;

  let color      = "blue";
  let lightColor = "lightblue";

  function handleDateChange(){
    effort.start = rangeValues[0];
    effort.stop  = rangeValues[1];

    if ( effort.start === 50 ){
      effort.start = 0;
    }
  }
  function handlePercentChange(){
    effort.percent = percValue[0];
  }

</script>

<svelte:head>
<style>
  
</style>
</svelte:head>


<main>
	
  <div class="content" style="--range-handle-focus: {color}; --range-handle: {lightColor}">

    
    <br>
    <h2>TaskSlider</h2>
    <br>
    <div>
      Start: {effort.start} Stop: {effort.stop} %: {effort.percent} Title: {effort.title} Min: {min} Max: {max}
    </div>
    <div>
      <input type="text"   bind:value={effort.start}/>
      <input type="text"   bind:value={effort.stop}/>
      <input type="number" bind:value={effort.percent}/>
    </div>
      

    <!-- Outer Range Selector for start/stop dates -->
    <RangeSlider range pushy float {disabled} {min} {max}
      bind:values={rangeValues}
      on:change={(e)=>handleDateChange(e)}>

      <div style="--range-handle-focus: red; --range-handle: green; --range-slider: pink;">
        <div>
          {effort.title}
        </div>

        <!-- Inner-range selector for Percent -->
        <div class="percentSlider">
          <RangeSlider 
            range="min" 
            bind:values={percValue}
            on:change={(e)=>handlePercentChange(e)}/>
        </div>
    </div>

    </RangeSlider>
    
    <br>
    
  </div>


</main>
