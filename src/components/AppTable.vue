<script setup>
import { computed, ref } from 'vue';
const props = defineProps(['items', 'cols', 'search']);
const searchQuery = ref('')

console.log(typeof props.search);
const query = computed(() => {
    if (typeof props.search === 'boolean')
        if (props.search)
            return searchQuery.value
        else
            return ''
    else if (typeof props.search === 'string')
        return props.search
})

const headers = computed(() => {
    if (props.cols?.length) {
        console.warn('get from props');
        return props.cols
    }
    else {
        console.warn('lets calculate');

        return Object.keys[0].map((item) => {
            return { key: item }
        })


    }
})


const filteredItems = computed(() => {

    return props.items.filter((item) => {
        return item.name.toLowerCase().includes(query.value.toLowerCase())
    })

})
console.log('loaded!');
console.log(props.search && !(typeof (props.search) === 'string'));


</script>

<template>
    <input type="text" v-model="searchQuery" v-if="props.search === true">
    <table class="table">
        <thead>
            <tr>
                <th v-for="col in headers">
                    <span class="text-capitalize">
                        {{ col.key }}
                    </span>
                </th>
            </tr>
        </thead>
        <tbody>

            <!-- <td v-for="value in Object.values(item)">
                    <slot name="item" :item="item">
                        {{ value }}
                    </slot>
                </td> -->
            <tr v-for="item in filteredItems">
                <td v-for="[key, value] in Object.entries(item)">
                    <slot :name="'col-' + key" :item="item">
                        {{ value }}
                    </slot>
                </td>
            </tr>

        </tbody>
    </table>
</template>
