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
    default: 'forex-cross-rates',
  },
});

const defaultOptions = {
  width: '100%',
  height: 450,
  colorTheme: 'dark',
  currencies: ['EUR', 'USD', 'JPY', 'GBP', 'CHF', 'AUD', 'CAD', 'NZD'],
  isTransparent: false,
  locale: 'en',
}

const options = merge({}, defaultOptions, props.options);

const { container, tradingview } = useInitWidget(
  options,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-forex-cross-rates.js'
);
</script>
