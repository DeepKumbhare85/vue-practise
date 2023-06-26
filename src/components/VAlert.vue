<script setup>
import { watch } from 'vue';

const props = defineProps({
    dismissible: Boolean,
    modelValue: Boolean,
});
const emits = defineEmits(['update:modelValue', 'close']);

watch(
    () => props.modelValue,
    (val) => {
        if (!val)
            emits('close');
    }
);
</script>
<template>
    <div class="alert alert-primary" v-if="props.modelValue">
        <slot></slot>
        <button v-if="props.dismissible" class="btn-close" aria-label="Close" @click="$emit('update:modelValue')"></button>
    </div>
</template>


<style lang="scss" scoped></style>