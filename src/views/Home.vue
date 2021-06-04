<template>
  <div class="test-chart-container">
    <h2 class="chart-title">test</h2>
    <svg id="svg-test">
      <g
        v-if="domLoaded"
        :style="{
          transform: `translate(${this.margin.left}px,${this.margin.top}px)`
        }"
      >
        <rect
          x="0"
          y="0"
          :width="boxWidth"
          height="300"
          fill="white"
          stroke="blue"
          stroke-width="2"
        />
        <DynamicText
          text="This is the dynamic text. Unless I set a width, it will also run long lonfasfg over where I need it to go."
          :width="boxWidth"
          :x="0"
          :y="15"
          :textStyle="{
            fontWeight: 400
          }"
          align="baseline"
          :scaleToFit="true"
        />
      </g>
    </svg>
  </div>
</template>

<script>
import * as d3 from 'd3'
import DynamicText from '@/components/utils/text/Text'
export default {
  name: 'test',
  components: { DynamicText },
  data: function() {
    return {
      margin: { top: 15, right: 15, bottom: 0, left: 15 },
      boxWidth: 650,
      domLoaded: false
    }
  },
  computed: {
    width: function() {
      return (
        +d3
          .select('#svg-test')
          .style('width')
          .replace('px', '') -
        this.margin.left -
        this.margin.right
      )
    },
    height: function() {
      return (
        +d3
          .select('#svg-test')
          .style('height')
          .replace('px', '') -
        this.margin.top -
        this.margin.bottom
      )
    }
  },
  mounted() {
    this.domLoaded = true
  }
}
</script>

<style lang="scss" scoped>
.test-chart-container {
  width: 800px;
  height: 500px;
  display: flex;
  flex-flow: column;

  .chart-title {
    flex: 0 0 auto;
  }

  #svg-test {
    border: 1px solid rgb(207, 207, 207);
    width: 100%;
    flex: 1 1 auto;
  }
}
</style>
