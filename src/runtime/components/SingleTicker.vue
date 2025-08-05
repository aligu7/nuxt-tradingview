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
import { singleTickerOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type SingleTickerOptions = typeof singleTickerOptions

const props = withDefaults(defineProps<{
  options?: Partial<SingleTickerOptions>
  class?: string
}>(), {
  class: 'single-ticker',
  options: () => ({})
})

const mergedOptions: SingleTickerOptions = {
  ...singleTickerOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-single-quote.js'
);
</script>
