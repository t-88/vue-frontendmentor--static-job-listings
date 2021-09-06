<template>
    <div class="TagItem">
        <p>{{ text }}</p>
        <div class="img-container" @click="$emit('un-select-filter',text)"> 
            <img src="../../assets/icon-remove.svg" alt="remove">
        </div>
    </div>
</template>

<script>
export default {
    name: "TagItem",
    props: {
        text: String,
    },
    setup() {
        
    },
}
</script>

<style lang="scss" scoped>
@import "../../shared";
.TagItem {
    box-shadow: inset #00000029 -2px 0 20px 0px;
    width: fit-content;
    height: fit-content;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 5px;
    overflow: hidden;
    p {
        color: #5ba4a4;
        font-weight: 700;
        width: fit-content;
        line-height: 1;
        cursor: context-menu;

        font-size: mathFromPcToTablet(15,12);
        padding: mathFromPcToTablet(12,9);
        @include media("<=tablet") {
            font-size: 12px;
            padding: 9px;
        }
    }
    .img-container {
        background: hsl(180, 29%, 50%);
        cursor: pointer;
        height: mathFromPcToTablet(37,31);
        padding: mathFromPcToTablet(11,9) mathFromPcToTablet(12,10);
        @include media("<=tablet") {
            height: 31px;
            padding: 9px 10px;
        }
        img {
            height: mathFromPcToTablet(16,14);
            @include media("<=tablet") {
                height: 14px;
            }
        }

        &:hover {
            background: hsl(180, 14%, 20%);
        }
    }

}
</style>