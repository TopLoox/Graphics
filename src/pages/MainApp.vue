<template>
  <q-page class="flex flex-center column bg-dark">
    <q-intersection
      transition="scale"
      transition-duration="800"
    >
      <q-card class="br-em flex flex-center q-mb-xl shadow-15">
        <q-card-section class="flex flex-center row q-px-sm">
          <q-input
            class="q-mx-sm"
            v-for="input in inputs"
            :key="input.label"
            :label='input.label'
            v-model="input.model"
            filled
          >
            <template v-slot:prepend>
              <q-icon :name="input.icon" :color='input.color'/>
            </template>
          </q-input>
        </q-card-section>
        <q-card-section class="q-pl-none">
          <q-btn
            size="md"
            round
            color="primary"
            icon="send"
            @click="setDataChart"
          />
        </q-card-section>
      </q-card>
    </q-intersection>

    <q-intersection
      transition="scale"
      transition-duration="900"
    >
      <q-list>
        <SimpleLineChart
          class="br-em"
          ref="SimpleLineChart"
          :x-data="xData"
          :y-data="yData"
          @click="initChart"/>
      </q-list>
    </q-intersection>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { useQuasar } from 'quasar';
import SimpleLineChart from "components/SimpleLineChart.vue";
// const $q = useQuasar()

export default defineComponent({
  name: 'MainApp',
  components: {
    SimpleLineChart
  },

  data() {
    return {
      inputXAxis: ref(''),
      inputYAxis: ref(''),

      yData: [30, 70, 40, 50, 10, 90, 20],
      xData: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],

      inputs: [
        {
          label: 'xAxis',
          model: this.inputXAxis,
          icon: 'fas fa-database',
          color: 'primary',
        },
        {
          label: 'yAxis',
          model: this.inputYAxis,
          icon: 'fas fa-calendar',
          color: 'primary',
        }
      ]
    }
  },

  methods: {
    setDataChart() {
      this.$refs.SimpleLineChart.init()

      this.$q.notify({
        color: 'positive',
        progress: true,
        position: 'top-right',
        message: "Oops.. Sorry it's doesn't work yet :p",
        caption: 'project by TopLoox',
        avatar: 'https://avatars.githubusercontent.com/u/61392421?v=4',
        actions: [
          { label: 'Cringe', color: 'white'}
        ]
      })
    },
  }
})
</script>

<style scoped lang="scss">
.br-em {
  border-radius: 1em;
}
</style>
