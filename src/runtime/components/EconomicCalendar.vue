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
import { economicCalendarOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type EconomicCalendarOptions = typeof economicCalendarOptions

const props = withDefaults(defineProps<{
  options?: Partial<EconomicCalendarOptions>
  class?: string
}>(), {
  class: 'economic-calendar',
  options: () => ({})
})

const mergedOptions: EconomicCalendarOptions = {
  ...economicCalendarOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-events.js'
);
</script>
