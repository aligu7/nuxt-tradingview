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
import { forexHeatMapOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type ForexHeatMapOptions = typeof forexHeatMapOptions

const props = withDefaults(defineProps<{
  options?: Partial<ForexHeatMapOptions>
  class?: string
}>(), {
  class: 'forex-heat-map',
  options: () => ({})
})

const mergedOptions: ForexHeatMapOptions = {
  ...forexHeatMapOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-forex-heat-map.js'
);
</script>
