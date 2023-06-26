<script setup>
const props = defineProps(['items', 'modelValue']);
const emit = defineEmits(['update:modelValue']);
</script>

<template>
    <ul>
        <div class="my-2">
            <slot name="before"></slot>
        </div>
        <li v-for="(item, index) in props.items" :key="index" @click="$emit('update:modelValue', item)">
            <span>{{ item }}</span>
        </li>
        <div class="my-2">
            <slot name="after"></slot>
        </div>
    </ul>
</template>