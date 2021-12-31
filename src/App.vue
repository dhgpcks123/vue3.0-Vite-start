<template>
  <MyTable :header="header" :rows="rows"/>  
</template>

<script>
import MyTable from './components/Table.vue'

export default {
  name: 'App',
  data() {
    return {
      header: ['first title', 'second title', 'third title'],
      rows: [
        [{data: 'first content'}, {data: 'second content'}, {data: 'second content'}],
        [{data: 'first content2', colspan: 2}],
        [{data: 'first content2'}],
        [{data: 'rowspan', rowspan: 3}, {data: 'ge'}],
        [{data: 'first content2'}],
        [{data: 'first content2'}],
      ],
    }
  },
  components: {
    MyTable,
  },
}
</script>