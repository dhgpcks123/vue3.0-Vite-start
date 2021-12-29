<template>
  <button
    v-bind="$attrs"
    :type="type"
    :class="classes"
    ref="button"
    v-on="type == 'switch' ? { click: onClick } : {}"
  >
    <slot></slot>
  </button>
</template>

<script>
import {ref, onMounted} from 'vue'
export default{
    props: {
        type: {
            default: 'button',
            validator: (value) => {
                // 실전 연습 - switch 추가
                const allowed = ['button', 'submit', 'reset', 'switch']
                return allowed.includes(value)
            },
        },
        active: {
            type: Boolean,
            default: true
        }
    },
    emits: ['update:active'],
    setup(props, context){
        const classes = ref([])
        // const classes = reactive([])
        // const button = ref(null)
        const active = ref(props.active)
        
        // swtich 를 위한 Props
        const changeBrightness = () => {
            if (props.type == 'switch') {
                if (!active.value) classes.value.push('deactive')
                else classes.value = classes.value.filter((i) => i != 'deactive')
            }
        }
        changeBrightness()
        const onClick = () => {
            active.value = !active.value
            changeBrightness()
            context.emit('update:active', active.value)
        }
        
        
        return {
            classes,
            onClick,
        }

    }
    
}
</script>

<style scoped>
.deactive{
    filter: brightness(50%)
}

</style>