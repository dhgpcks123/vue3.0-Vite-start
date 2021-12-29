<template>
  <ToggleButton type="switch" v-model:active="active">MyButton1</ToggleButton>
  <!-- <ToggleButton lg background-white>MyButton2</ToggleButton>
  <ToggleButton sm pill text-red>MyButton3</ToggleButton>
  <ToggleButton md pill text-green background-pink>MyButton4</ToggleButton>
  <ToggleButton lg pill @click.prevent="onClick">MyButton5</ToggleButton>
  <ToggleButton >MyButton6</ToggleButton> -->
</template>

<script>
import ToggleButton from "./components/ToggleButton.vue"


export default {
  name: 'App',
  data(){
    return{
      active: false,
    }
  },
  watch: {
    active(new_val) {
      alert(new_val)
    }
  },
  methods: {
  },
  components: {
    ToggleButton,
  },
}
</script>