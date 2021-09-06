<template>
    <div class="FiltterBox-comp">
        <div class="filters-container">
            <TagItem v-for="filter in selectedFillters" :key="filter" :text="filter" @un-select-filter="unSelectFilter"/>
        </div>
        <p @click="$emit('un-select-all')">Clear</p>
    </div>
    
</template>

<script>
import TagItem from "./TagItem"
export default {
    name: "FiltterBox",
    components: {
        TagItem,
    },
    props: {
        selectedFillters: Array,
    },
    setup(props,{emit}) {
        const unSelectFilter = (filter) => {
            emit("un-select-filter",filter)
        }
        return { unSelectFilter }
    },
}
</script>

<style lang="scss" scoped>
@import "../../shared";
.FiltterBox-comp {
    width: 80%;
    background: white;
    border-radius: 5px;
    box-shadow: #5ba4a45c 2px 5px 25px 0px;
    margin: auto;

    display: flex;
    justify-content: space-between;
    align-items: center;
    
    transform: translateY(mathFromPcToTablet(-40,-30));
    padding: mathFromPcToTablet(20,15)  mathFromPcToTablet(40,20);
    p {
        font-weight: 700;
        color: hsl(180, 8%, 52%);
        cursor: pointer;
        font-size: mathFromPcToTablet(16,14);
        &:hover {
            color: hsl(180, 29%, 50%);
            text-decoration: underline;
        }
    }
    .filters-container {
        display: flex;
        flex-wrap: wrap;
        gap: mathFromPcToTablet(20,10);
    }
}
</style>