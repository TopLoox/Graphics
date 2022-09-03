<template>
  <q-card class="shadow-24">
    <q-card-section>
      <div id="chart-container" ref="SimpleLinechart"></div>
    </q-card-section>
    <q-resize-observer @resize="onResize"/>
  </q-card>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "SimpleLineChart",
  props: {
    xData: {
      type: Array,
      default: () => []
    },

    yData: {
      type: Array,
      default: () => []
    }
  },

  data() {
    return {
      options: {
        title: {
          text: 'Simple Line Chart',
        },

        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
          }
        },

        // legend: {
        //   data: ['Values']
        // },

        xAxis: {
          boundaryGap: false,
          type: 'category',
          data: this.yData,
        },

        yAxis: {
          type: 'value'
        },

        series: [
          {
            name: 'Values',
            type: 'line',
            smooth: true,
            data: this.xData,

            color: '#ff5757',
            lineStyle: {
              width: 5
            },
            showSymbol: true,
            areaStyle: {
              opacity: .7,
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                {
                  offset: 0,
                  color: '#ffc15f',
                },
                {
                  offset: 1,
                  color: '#ff8c8c',
                }
              ])
            },
          }
        ],

        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },

        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
      },

      simple_line_chart: null
    }
  },

  mounted() {
    this.init()
  },

  methods: {
    init() {
      let Chart = document.getElementById('chart-container')
      echarts.dispose(Chart)
      this.simple_line_chart = echarts.init(Chart)
      this.simple_line_chart.setOption(this.options)
      this.simple_line_chart.setOption(this.options)
      // console.log(this.xData, this.yData)
    },
    onResize() {
      if (this.simple_line_chart) {
        this.simple_line_chart.resize()
      }
    },
  }
};
</script>

<style scoped lang="scss">
#chart-container {
  position: relative;
  width: 100vh;
  height: 50vh;
  overflow: hidden;
}
</style>
