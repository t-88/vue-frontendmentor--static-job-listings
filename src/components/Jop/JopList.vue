<template>
    <div class="JopList-comp" >
        <JopItem v-for="data in jopData" :key="data.id" :data="data" @select-filter="selectFilter"/>
    </div> 
</template>

<script>
import JopItem from "./JopItem.vue"
export default {
    name: "JopList",
    components: { JopItem },
    props:{ jopData: Array },
    setup(props,{emit}) {
        const selectFilter = (filter) => {
            emit('select-filter',filter)
        }
        return { selectFilter }
    },
}
</script>

<style lang="scss" scoped>
@import "../../shared";
.JopList-comp {
    width: 80%;
    display: flex;
    flex-direction: column;
    row-gap: 25px;
    
    width: mathFromPcToTablet(1174,700);

    @include media("<=tablet",">phone") {
        width: mathFromTabletToPhone(700,570);
    }
    @include media("<=phone") {
        width: mathFromPhoneToMinWidth(450,260);
        row-gap: 50px;
    }
    @include media("<=min-width") {
        width: 260px;
    }
}
</style>