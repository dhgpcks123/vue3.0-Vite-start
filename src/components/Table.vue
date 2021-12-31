<template>
    <table>
        <tr>
            <th v-for="(head, index) in header" :key="'head'+index">
                {{ head }}
            </th>
        </tr>
        <tr v-for="(row, index) in rows" :key="'row-'+index">
            <td
                v-for="(data, index) in row"
                :key="'data-'+index"
                :colspan="data.colspan || 1"
                :rowspan="data.rowspan || 1"
            >
                {{ data.data }}
            </td>
        </tr>
    </table>
</template>

<script>
// 안쓸꺼여서 그냥 import안하나봐 import { ref, onMounted } from 'vue'
export default {
    props: ['header', 'rows'],
}
</script>


<style scoped>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 5px;
}
</style>