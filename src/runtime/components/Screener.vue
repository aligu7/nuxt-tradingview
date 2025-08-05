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
import { screenerOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type ScreenerOptions = typeof screenerOptions

const props = withDefaults(defineProps<{
  options?: Partial<ScreenerOptions>
  class?: string
}>(), {
  class: 'screener',
  options: () => ({})
})

const mergedOptions: ScreenerOptions = {
  ...screenerOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-screener.js'
);
</script>
