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
import { tickerOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type TickerOptions = typeof tickerOptions

const props = withDefaults(defineProps<{
  options?: Partial<TickerOptions>
  class?: string
}>(), {
  class: 'ticker',
  options: () => ({})
})

const mergedOptions: TickerOptions = {
  ...tickerOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-tickers.js'
);
</script>
