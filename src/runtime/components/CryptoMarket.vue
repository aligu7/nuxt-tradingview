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
import { cryptoMarketOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type CryptoMarketOptions = typeof cryptoMarketOptions

const props = withDefaults(defineProps<{
  options?: Partial<CryptoMarketOptions>
  class?: string
}>(), {
  class: 'crypto-market',
  options: () => ({})
})

const mergedOptions: CryptoMarketOptions = {
  ...cryptoMarketOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-screener.js'
);
</script>
