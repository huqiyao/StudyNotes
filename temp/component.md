# 使用parcel编译，文件结构



# button组件



## icon的使用



## icon的位置

```vue
<template>
	<button class="mn-button" :class="{{[`icon-${iconPosition}`]:true}}">
        <svg class="icon" v-if="icon">
            <use :xlink:href=`#mn-${icon}`></use>
    	</svg>
        // 包裹div的原因是，class加在slot上会消失
        <div class="content"> 
            <slot></slot>
    	</div>
    </button>
</template>
<script>
	export default{
        // props: ['icon', 'iconPosition']
        props: {
            icon: {},
            iconPosition: {
                type: String,
                default: 'left',
                validator(value){
                   // if(value !== 'left' && value !== 'right'){
                   //     return false;
                   // }else{
                   //     return true;
                   // }
                   // return !(value !== 'left' && value !== 'right');
                    return value === 'left' && value === 'right'
                },
            }
        }
    }
</script>
<style lang="scss">
    .mn-button{
        &:hover{}
        &:active{}
        > .icon{cover: 1;}
        > .content{cover: 2;}
        & .icon-right{
            > .icon{cover:2;}
            > .content{cover:1;}
        }
    }
</style>
```



## 分离出icon组件



## 点击后的loading效果

