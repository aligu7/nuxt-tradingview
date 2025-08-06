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
import { companyProfileOptions } from '../composables/defaultWidgetOptions';
import useInitWidget from '../composables/useInitWidget';

type CompanyProfileOptions = typeof companyProfileOptions

const props = withDefaults(defineProps<{
  options?: Partial<CompanyProfileOptions> & { [key: string]: unknown }
  class?: string
}>(), {
  class: 'company-profile',
  options: () => ({})
})

const mergedOptions: CompanyProfileOptions = {
  ...companyProfileOptions,
  ...props.options,
}

const { container, tradingview } = useInitWidget(
  mergedOptions,
  props.class,
  'https://s3.tradingview.com/external-embedding/embed-widget-symbol-profile.js'
);
</script>
