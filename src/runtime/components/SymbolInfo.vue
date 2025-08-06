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
import { symbolInfoOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type SymbolInfoOptions = typeof symbolInfoOptions

const props = withDefaults(defineProps<{
  options?: Partial<SymbolInfoOptions> & { [key: string]: unknown }
  class?: string
}>(), {
  class: 'symbol-info',
  options: () => ({})
})

const mergedOptions: SymbolInfoOptions = {
  ...symbolInfoOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-symbol-info.js'
);
</script>
