<script>
  import * as d3 from "d3";
  export let boxdata;
  export let boxSize;
  export let title;
  export let containerColor;
  export let interpolation;
  export let borderColor;

  // clicked state handling
  let expanded = false;

  function setExpanded() {
    if (expanded) {
      expanded = false;
    } else {
      expanded = true;
    }
  }

  let allValues = [];

  for (let i = 0; i < boxdata.length; i++) {
    allValues = allValues.concat(boxdata[i].boxes);
  }

  var scaleNorm = d3
    .scaleLinear()
    .domain([d3.min(allValues), d3.max(allValues)])
    .range([0, 1]);

  let colorFunc = function(value) {
    let color;
    let borderColor;
    if (value) {
      color = eval(`d3.${interpolation}(scaleNorm(value));`);
      borderColor = "white";
    } else {
      color = "transparent";
      borderColor = "transparent";
    }
    return { color, borderColor };
  };
</script>
<div class='vizBody {expanded ? 'noHover' : '' }'>
  {#each boxdata as cat (cat.id)}
    <div on:click={setExpanded} class='vizWrapper {expanded ? 'transformed' : null }'  style='--box-size: {boxSize}; --id-val: {cat.id}; --container-color: {containerColor}; --border-color: {borderColor};'>
      <h2>{expanded ? cat.categoryTitle : title}</h2>
      <div class='boxContainer'>
      {#each cat.boxes as box}
      <div class='box' style='--box-color: {colorFunc(box).color}; --border-color: {colorFunc(box).borderColor}; --opacity-value: {scaleNorm(box)}'></div>
      {/each}
      </div>
    </div>
  {/each}
</div>




<style>
  .vizWrapper {
    margin: auto;
    text-align: left;
    width: max-content;
    height: max-content;
    transition: 0.5s;
    transform-style: preserve-3d;
    position: absolute;
    top: 32px;
    left: 0;
    right: 0;
  }

  h2 {
    font-weight: 400;
  }

  .vizWrapper:not(:first-of-type) {
    opacity: 1;
    pointer-events: none;
  }

  .vizBody.noHover:hover .vizWrapper {
    pointer-events: none;
    box-shadow: revert !important;
  }

  .vizBody:hover .vizWrapper {
    transform: rotateX(40deg);
    box-shadow: var(--border-color) 0px 1px 0px, var(--bg-color) 0px 10px 0px,
      var(--container-color) 0px 20px, var(--border-color) 0px 21px 0px,
      var(--bg-color) 0px 30px, var(--container-color) 0px 40px,
      var(--border-color) 0px 41px 0px, var(--bg-color) 0px 50px;
    cursor: pointer;
  }

  .transformed {
    transform: translateY(calc(100% * var(--id-val))) !important;
    opacity: 1 !important;
    pointer-events: auto !important;
  }

  .transformed:hover {
    transform: translateY(calc(100% * var(--id-val))) !important;
    box-shadow: revert !important;
    cursor: pointer;
  }

  .boxContainer {
    border: 1px solid var(--border-color);
    display: flex;
    flex-wrap: wrap;

    padding: 16px;
    width: calc((var(--box-size) + 12px) * 7);
    height: max-content;
    justify-content: flex-start;
    align-content: flex-start;
    background-color: var(--container-color);
    background-color: transparent;
  }

  .vizWrapper:first-of-type > .boxContainer {
    background-color: var(--container-color);
  }

  .transformed > .boxContainer {
    background-color: var(--container-color);
  }

  /* the pink boxes we will transition */
  .box {
    width: var(--box-size);
    height: var(--box-size);
    margin: 1px;
    z-index: 0;
    background-color: var(--box-color);
    /* background-color: orange; */
    position: relative;
    -moz-border-radius: 2px;
    -webkit-border-radius: 2px;
    border-radius: 6%;
    padding: 4px;
    color: var(--box-color);
    /* opacity: clamp(0.8, var(--opacity-value), 1); */
    opacity: var(--opacity-value);
    border: 1px solid var(--border-color);
  }
</style>