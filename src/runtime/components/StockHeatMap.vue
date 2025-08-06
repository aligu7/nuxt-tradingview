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
import { stockHeatMapOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type StockHeatMap = typeof stockHeatMapOptions

const props = withDefaults(defineProps<{
  options?: Partial<StockHeatMap> & { [key: string]: unknown }
  class?: string
}>(), {
  class: 'stock-heat-map',
  options: () => ({})
})

const mergedOptions: StockHeatMap = {
  ...stockHeatMapOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-stock-heatmap.js'
);
</script>
