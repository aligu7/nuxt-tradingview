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
import { marketOverviewOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type MarketOverviewOptions = typeof marketOverviewOptions

const props = withDefaults(defineProps<{
  options?: Partial<MarketOverviewOptions> & { [key: string]: unknown }
  class?: string
}>(), {
  class: 'market-overview',
  options: () => ({})
})

const mergedOptions: MarketOverviewOptions = {
  ...marketOverviewOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-market-overview.js'
);
</script>
