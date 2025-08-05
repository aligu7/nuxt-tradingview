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
import { marketDataOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type MarketDataOptions = typeof marketDataOptions

const props = withDefaults(defineProps<{
  options?: Partial<MarketDataOptions>
  class?: string
}>(), {
  class: 'market-data',
  options: () => ({})
})

const mergedOptions: MarketDataOptions = {
  ...marketDataOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-market-quotes.js'
);
</script>
