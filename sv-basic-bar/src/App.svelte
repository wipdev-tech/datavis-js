<script>
  import { scaleLinear, scaleBand } from "d3-scale";
  import AxisTop from "./components/AxisTop.svelte";

  // data
  const data = [
    { cat: "Placebo", val: 0.35126 },
    { cat: "Low Dose", val: 0.68901 },
    { cat: "High Dose", val: 0.62023 },
  ];

  // width and height
  let width = 960;
  let height = 300;

  const margin = { top: 25, right: 10, bottom: 10, left: 10 };

  let innerWidth = width - margin.left - margin.right;
  let innerHeight = height - margin.top - margin.bottom;

  // scales
  const xScale = scaleLinear().domain([0, 1]).range([0, innerWidth]);
  const yScale = scaleBand()
    .domain(data.map((d) => d.cat))
    .range([0, innerHeight])
    .padding(0.3);
</script>

<svg {width} {height}>
  <g transform="translate({margin.left}, {margin.top})">
    <AxisTop {xScale} {innerWidth} />
    {#each data as { cat, val }}
      <rect
        class="bg"
        y={yScale(cat) - 8}
        width={innerWidth}
        height={yScale.bandwidth() + 16}
      />
      <rect y={yScale(cat)} width={xScale(val)} height={yScale.bandwidth()} />
    {/each}
  </g>
</svg>

<style>
  .bg {
    fill: lightgray;
  }
</style>
