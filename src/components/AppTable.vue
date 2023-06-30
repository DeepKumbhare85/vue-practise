<script setup>
import { computed, ref, watch } from 'vue';
const props = defineProps(['items', 'cols', 'search', 'noDataText']);
const searchQuery = ref('')
const itemsPerPage = ref(5)
const currentPage = ref(1)
const sortOrder = ref('')
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

const sortBy = ref()


const sortedItems = computed(() => {
    if (sortOrder.value === 'asc') {
        return props.items.sort((a, b) => {
            return a[sortBy.value] > b[sortBy.value] ? 1 : -1
        })
    }
    else if (sortOrder.value === 'desc') {
        return props.items.sort((a, b) => {
            return a[sortBy.value] > b[sortBy.value] ? -1 : 1
        })
    }
    else {
        return props.items
    }
})

const filteredItems = computed(() => {
    return sortedItems.value.filter((item) => {
        return item.name.toLowerCase().includes(query.value.toLowerCase())
    })
});

const paginatedItems = computed(() => {
    return filteredItems.value.slice((currentPage.value - 1) * itemsPerPage.value, currentPage.value * itemsPerPage.value)
});

watch(itemsPerPage, () => {
    currentPage.value = 1
});

</script>

<template>
    <input type="text" v-model="searchQuery" v-if="props.search === true">
    <table class="table">
        <thead>
            <tr>
                <th v-for="col in headers">
                    <div class="d-flex align-items-center">
                        <div class="text-capitalize" style="cursor: pointer;"
                            @click="sortBy = col.key; sortOrder === '' ? sortOrder = 'asc' : sortOrder === 'asc' ? sortOrder = 'desc' : sortOrder = 'asc'">
                            {{ col.key }}
                            <i
                                :class="[sortOrder === '' ? 'bi bi-sort-up' : sortOrder === 'asc' ? 'bi bi-sort-down' : 'bi bi-sort-up', sortBy === col.key || '' ? '' : 'd-none']"></i>
                        </div>

                    </div>
                </th>
            </tr>
        </thead>

        <tbody>
            <tr v-if="!props.items.length">
                <td class="text-center" :colspan="headers.length">
                    {{ props.noDataText }}
                </td>
            </tr>
            <tr v-else v-for="item in paginatedItems">
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
                    <button v-for="index in Math.ceil(filteredItems.length / itemsPerPage)   "
                        :class="currentPage === index ? 'btn btn-primary' : 'btn btn-outline-dark'"
                        @click="currentPage = index">{{ index }}</button>
                </div>
            </div>
        </tfoot>
    </table>
</template>
