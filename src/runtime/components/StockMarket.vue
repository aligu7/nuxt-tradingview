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
import { stockMarketOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type StockMarketOptions = typeof stockMarketOptions

const props = withDefaults(defineProps<{
  options?: Partial<StockMarketOptions> & { [key: string]: unknown }
  class?: string
}>(), {
  class: 'stock-market',
  options: () => ({})
})

const mergedOptions: StockMarketOptions = {
  ...stockMarketOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-hotlists.js'
);
</script>
