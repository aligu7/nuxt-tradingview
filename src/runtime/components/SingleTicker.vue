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
import useInitWidget from '../composables/useInitWidget';
import merge from 'lodash.merge'

const props = defineProps({
  options: {
    type: Object,
    default: () => {},
  },
  class: {
    type: String,
    default: 'single-ticker',
  },
});

const defaultOptions = {
  colorTheme: 'dark',
  symbol: 'FX:EURUSD',
  width: 350,
  isTransparent: false,
  locale: 'en',
}

const options = merge({}, defaultOptions, props.options);

const { container, tradingview } = useInitWidget(
  options,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-single-quote.js'
);
</script>
