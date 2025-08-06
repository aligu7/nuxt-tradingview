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
import { topStoriesOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type TopStoriesOptions = typeof topStoriesOptions

const props = withDefaults(defineProps<{
  options?: Partial<TopStoriesOptions> & { [key: string]: unknown }
  class?: string
}>(), {
  class: 'ticker',
  options: () => ({})
})

const mergedOptions: TopStoriesOptions = {
  ...topStoriesOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-timeline.js'
);
</script>
