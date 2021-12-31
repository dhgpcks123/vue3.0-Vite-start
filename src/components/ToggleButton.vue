// template 구간
<template>
    <button
        v-bind="$attrs"
        :type="type" 
        :class="classes" 
        ref="button"
        v-on="type == 'switch' ? { click: onClick} : {}"
    >
        <slot></slot>
        <!-- slot은 여기에 무언가가 들어갈 거란 의미.
            퍼스널 컴퓨터에서, 롬(ROM) 카세트나 확장 보드(board)를 끼워 넣는 구멍 -->
    </button>
</template>

// script 구간
<script>
import { ref, onMounted } from 'vue'
import { c } from '../../dist/assets/vendor.883f1844';
// 여기서 사용할 것들만  'vue'에서 import해옵니다. {ref, onMounted}

export default{
    
    // props는 상위 vue에서 무언가를 받아쓰겠다가 아닐까?
    props:{
        //타입에 대한 정보를 정의하겠다.
        type: {
            default: 'button',
            validator: (value) => {
                const allowd = ['button', 'submit', 'reset', 'switch']
                return allowd.includes(value);
            },
        },
        sm: Boolean, // default를 boolean(false)으로 주겠다는거겠지?
        md: {
            type: Boolean,
            default: true,
        },
        lg: Boolean,
        pill: Boolean,
        active: {
            type: Boolean,
            default: true,
        }
    },
    setup(props, context) {
        const classes = ref([])
        const button = ref(null)
        const active = ref(props.active)
        // 변화가 필요하니까 ref로 씌우는거겠지?

        console.log('props : ' + props)
        // props로 처리하려는 변수들. 위에서 정의해둔 props 사용하겠지.
        if(props.sm) classes.value.push('sm')
        else if(props.lg) classes.value.push('lg')
        else classes.value.push('md')

        if(props.pill) classes.value.push('pill')

        // switch를 위한 Props
        const changeBrightness = () => {
            if(props.type == 'switch'){
                if(!active.value) classes.value.push('deactive')
                else classes.value = classes.value.filter((i) => i != 'deactive')
            }
        }
        changeBrightness()

        const onClick = () => {
            active.value = !active.value
            changeBrightness()
            context.emit('update:active', active.value)
        }

        console.log('context : ' + context)
        // Non-props로 처리하려고 하는 변수들
        onMounted(()=>{
            // mount되고 난 후에 context.attrs forEach 돒려
            Object.keys(context.attrs).forEach((attr)=>{
                //text- 문장으로 시작된다?
                if(attr.startsWith('text-')){
                    button.value.style.color = attr.substring(5)
                }
                if(attr.startsWith('background-')){
                    button.value.style.backgroundColor = attr.substring(11)
                }
            })
        })

        return {
            classes,
            button,
            onClick
        }
    },
}

</script>

// css 구간
<style scope>
button {
    outline: none;
}

.sm {
    height: 20px;
    font-size: 13px;
}

.md {
    height: 30px;
    font-size: 22px;
}

.lg {
    height: 40px;
    font-size: 31px;
}

.pill {
    border-radius: 16px;
}
.deactive {
    filter: brightness(50%);
}
</style>