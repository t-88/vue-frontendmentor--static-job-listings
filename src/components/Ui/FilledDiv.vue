<template>
    <div class="FilledDiv" :style="{ background: currBgColor , borderRadius: borderRadius }" @mouseenter="hover" @mouseleave="noHover" >
        <p  :style="{ color:currTextColor }" >
            {{ text }}
        </p>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity'
export default {
    name:"FilledDiv",
    props: {
        text: String,
        bgColor: {type:String, default:"hsl(180, 29%, 50%)"},
        bgColorHover: {type:String, default:null},
        textColor: {type:String, default:"white"},
        textColorHover: {type:String, default:null},
        borderRadius: {type:String, default:"20px"}

    },
    setup(props) {
        const hover = () => {
            currBgColor.value = props.bgColorHover == null ? props.bgColor : props.bgColorHover
            currTextColor.value = props.textColorHover == null ? props.textColor : props.textColorHover
        }
        const noHover = () => {
            currBgColor.value = props.bgColor
            currTextColor.value = props.textColor
        }
        const currBgColor = ref(props.bgColor)
        const currTextColor = ref(props.textColor)
        return { hover , noHover , currBgColor , currTextColor }
    },
}
</script>

<style lang="scss" scoped>
@import "../../shared";
.FilledDiv {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 23px;
    padding: 0 8px;
    cursor: context-menu;
    P {
        margin-top: 3px;
        line-height: 2;
        font-size: mathFromPcToTablet(10,8);

        @include media("<=phone",">min-width") {
            font-size: mathFromPhoneToMinWidth(10,7);
        }
    }
}
</style>