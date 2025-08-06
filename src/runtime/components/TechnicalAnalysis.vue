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
import { technicalAnalysisOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type TechnicalAnalysisOptions = typeof technicalAnalysisOptions

const props = withDefaults(defineProps<{
  options?: Partial<TechnicalAnalysisOptions> & { [key: string]: unknown }
  class?: string
}>(), {
  class: 'technical-analysis',
  options: () => ({})
})

const mergedOptions: TechnicalAnalysisOptions = {
  ...technicalAnalysisOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-technical-analysis.js'
);
</script>
