<script setup>
import { usePlugins } from '@/composables/usePlugins';

const props = defineProps({
  proposal: Object,
  space: Object,
  modelValue: Object
});

const { getPluginComponents } = usePlugins();
const components = getPluginComponents(
  'Create',
  Object.keys(props.space.plugins)
);

const emit = defineEmits(['update:modelValue']);
const update = data => {
  const allConfig = props.modelValue;
  allConfig[data.key] = data.form;
  emit('update:modelValue', allConfig);
};
</script>

<template>
  <component
    :is="component"
    v-for="(component, key) in components"
    :key="key"
    v-bind="props"
    @update="update"
  />
</template>
