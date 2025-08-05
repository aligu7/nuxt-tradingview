<template>
  <div
    :id="container"
    ref="tradingview"
    :style="{
      width: options.autosize && '100%',
      height: options.autosize && '100%',
    }" />
</template>

<script lang="ts" setup>
import { chartOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type ChartOptions = typeof chartOptions

const props = withDefaults(defineProps<{
  options?: Partial<ChartOptions>
  class?: string
}>(), {
  class: 'chart',
  options: () => ({})
})

const mergedOptions: ChartOptions = {
  ...chartOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-advanced-chart.js'
);
</script>
