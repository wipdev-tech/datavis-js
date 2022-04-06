<script>
  export let xScale;
  export let innerWidth;
</script>

<g>
  <line x2={innerWidth} stroke="black" />
  {#each xScale.ticks() as tick}
    <text x={xScale(tick)} y="-10">{tick}</text>
    <line transform="translate({xScale(tick)}, 0)" y1="-4" stroke="black" />
  {/each}
</g>

<style>
  text {
    text-anchor: middle;
  }
</style>
