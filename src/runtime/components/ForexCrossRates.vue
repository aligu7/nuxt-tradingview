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
import { forexCrossRatesOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type ForexCrossRatesOptions = typeof forexCrossRatesOptions

const props = withDefaults(defineProps<{
  options?: Partial<ForexCrossRatesOptions>
  class?: string
}>(), {
  class: 'forex-cross-rates',
  options: () => ({})
})

const mergedOptions: ForexCrossRatesOptions = {
  ...forexCrossRatesOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-forex-cross-rates.js'
);
</script>
