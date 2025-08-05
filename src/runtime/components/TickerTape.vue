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
import { tickerTapeOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type TickerTapeOptions = typeof tickerTapeOptions

const props = withDefaults(defineProps<{
  options?: Partial<TickerTapeOptions>
  class?: string
}>(), {
  class: 'ticker',
  options: () => ({})
})

const mergedOptions: TickerTapeOptions = {
  ...tickerTapeOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-ticker-tape.js'
);
</script>
