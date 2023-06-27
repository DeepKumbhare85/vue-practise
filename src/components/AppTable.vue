<script setup>
import { computed, ref } from 'vue';
const props = defineProps(['items', 'cols', 'search', 'noDataText']);
const searchQuery = ref('')
const itemsPerPage = ref(5)
const currentPage = ref(1)
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
    }).slice((currentPage.value - 1) * itemsPerPage.value, currentPage.value * itemsPerPage.value)

})
console.log(filteredItems.value.length / itemsPerPage.value);

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
            <tr v-if="!props.items.length">
                <td class="text-center" :colspan="headers.length">
                    {{ props.noDataText }}
                </td>
            </tr>
            <tr v-else v-for="item in filteredItems">
                <td v-for="[key, value] in Object.entries(item)">
                    <slot :name="'col-' + key" :item="item">
                        {{ value }}
                    </slot>
                </td>
            </tr>
        </tbody>
        <tfoot v-if="props.items.length">
            <div class="d-flex justify-content-end align-content-center">
                <div>
                    <select name="itemsPerPage" class="form-select" v-model="itemsPerPage">
                        <option value="5">5</option>
                        <option value="10">10</option>
                        <option value="15">15</option>
                    </select>
                </div>

                <div class="d-flex gap-2">
                    <button v-for="index in Math.ceil(props.items.length / itemsPerPage)"
                        :class="currentPage === index ? 'btn btn-primary' : 'btn btn-outline-dark'"
                        @click="currentPage = index">{{ index
                        }}</button>
                </div>
            </div>
        </tfoot>
    </table>
</template>
