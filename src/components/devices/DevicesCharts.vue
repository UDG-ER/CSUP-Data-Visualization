<template>
  <div class="row row-equal">
    <div class="flex xs12">
      <p class="display-2">Analytics</p>
    </div>
    <div class="flex xs12">
      <div class="row row-equal">
        <div class="flex xs12 md4">
          <va-date-picker
            :label="$t('forms.dateTimePicker.rangeLabel')"
            :config="{mode: 'range', inline: false}"
            v-model="datepicker.range"
          />
        </div>
      </div>
      <div v-if="!measurements" class="row">
        <va-progress-bar 
          class="placeholder small"
          color="success"
          :indeterminate="true"
        />
      </div>
    </div>
    <div v-if="measurements" class="flex xs12 md12">
      <va-card :title="$t('dashboard.charts.trends')">
        <va-chart class="chart" :data="measurements" type="line"/>
      </va-card>
    </div>

    <!--
    <div v-if="measurements" class="flex xs12 md3">
      <va-card :title="$t('dashboard.charts.dummyText')">
        <va-button
          icon="fa fa-print"
          flat
          slot="actions"
          class="mr-0"
        />
        <va-chart class="chart" :data="donutChartData" type="donut"/>
      </va-card>
    </div>
    -->

    <!--
    <div class="flex xs12 md6 xl3">
      <va-card :title="$t('dashboard.charts.topContributors')">
        <va-button flat small slot="actions" class="mr-0">
          {{ $t('dashboard.charts.showAll') }}
        </va-button>

        <div
          class="mb-3"
          v-for="(progress, idx) in progressData"
          :key="idx"
        >
          <va-progress-bar
            :value="getPercent(progress.value)"
            :color="progress.color"
          >
            {{ progress.value }} {{ $t('dashboard.charts.commits') }}
          </va-progress-bar>
          <p class="mt-2">{{ progress.text }}</p>
        </div>
      </va-card>
    </div>
    -->
  </div>
</template>

<script>
import { getDonutChartData } from '../../data/charts/DonutChartData'

export default {
  name: 'devices-charts',
  props: ['measurements', 'changeRange'],
  data () {
    return {
      //donutChartData: getDonutChartData(this.$themes),
      datepicker: {
        range: '',
      },
    }
  },
  watch: {

    "datepicker.range" (val) {
      if(val.includes('to')){
        this.$props.changeRange(val)
      }
    }
  },
  methods: {
    getPercent (val) {
      return (val / this.progressMax) * 100
    },
  },
}
</script>

<style scoped>
  .chart {
    height: 400px;
  }
</style>
