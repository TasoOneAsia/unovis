<script setup lang="ts" generic="Datum">
// !!! This code was automatically generated. You should not change it !!!
import { GroupedBar, GroupedBarConfigInterface, NumericAccessor } from '@unovis/ts'
import { onMounted, onUnmounted, computed, ref, watch, nextTick, inject } from 'vue'
import { arePropsEqual, useForwardProps } from '../../utils/props'
import { componentAccessorKey } from '../../utils/context'

const accessor = inject(componentAccessorKey)

// data and required props 
type Props = GroupedBarConfigInterface<Datum>
const props = defineProps<Props & { data?: Datum[] }>()

const data = computed(() => accessor.data.value ?? props.data)
// config
const config = useForwardProps(props)

// component declaration
const component = ref<GroupedBar<Datum>>()


onMounted(() => {
  nextTick(() => {
    component.value = new GroupedBar<Datum>(config.value)
    component.value?.setData(data.value)
    accessor.update(component.value)
  })
})

onUnmounted(() => {
  component.value?.destroy()
  accessor.destroy()
})

watch(config, (curr, prev) => {
  if (!arePropsEqual(curr, prev)) {
    component.value?.setConfig(config.value)
  }
})

watch(data, () => {
  component.value?.setData(data.value)
})

defineExpose({
  component
})
</script>

<script lang="ts">
export const VisGroupedBarSelectors = GroupedBar.selectors
</script>

<template>
  <div data-vis-component />
</template>


