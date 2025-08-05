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
import { fundamentalDataOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type FundamentalData = typeof fundamentalDataOptions

const props = withDefaults(defineProps<{
  options?: Partial<FundamentalData>
  class?: string
}>(), {
  class: 'fundamental-data',
  options: () => ({})
})

const mergedOptions: FundamentalData = {
  ...fundamentalDataOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-financials.js'
);
</script>
