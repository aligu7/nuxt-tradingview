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
import { miniChartOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type MiniChartOptions = typeof miniChartOptions

const props = withDefaults(defineProps<{
  options?: Partial<MiniChartOptions>
  class?: string
}>(), {
  class: 'mini-chart',
  options: () => ({})
})

const mergedOptions: MiniChartOptions = {
  ...miniChartOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-mini-symbol-overview.js'
);
</script>
