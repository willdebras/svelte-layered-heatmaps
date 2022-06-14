<script>
  import Heatmap from "./heatmap.svelte";

  const data = [
    {
      id: 0,
      categoryTitle: "January",
      boxes: [
        null,
        8,
        12,
        15,
        5,
        7,
        11,
        8,
        12,
        15,
        9,
        8,
        12,
        15,
        21,
        8,
        10,
        7,
        7,
        12,
        22,
        13,
        12,
        15,
        17,
        4,
        6,
        11,
        14,
        23,
        16,
        19
      ]
    },
    {
      id: 1,
      categoryTitle: "February",
      boxes: [
        null,
        null,
        null,
        null,
        14,
        17,
        6,
        9,
        13,
        21,
        16,
        29,
        3,
        4,
        7,
        2,
        11,
        19,
        11,
        14,
        24,
        21,
        17,
        30,
        26,
        16,
        24,
        21,
        11,
        16,
        7,
        9,
        12,
        13,
        15
      ]
    },
    {
      id: 2,
      categoryTitle: "March",
      boxes: [
        11,
        13,
        9,
        16,
        26,
        14,
        19,
        23,
        11,
        7,
        6,
        6,
        15,
        13,
        18,
        9,
        12,
        10,
        15,
        22,
        25,
        17,
        13,
        17,
        12,
        13,
        11,
        9,
        6,
        7,
        10
      ]
    }
  ];
</script>

<style>
  main {
    font-family: sans-serif;
    text-align: center;
    height: 100vh;
    width: 100vw;
  }

  :root {
    --bg-color: #f4f5f2;
    background-color: var(--bg-color);
    font-family: "Roboto";
  }
</style>

<main>
	<Heatmap title = 'Monthly Contributions' containerColor = 'PapayaWhip' borderColor = 'LightCoral'
  boxdata = {data} boxSize = '32px' 
  interpolation='interpolateOranges'/>
</main>