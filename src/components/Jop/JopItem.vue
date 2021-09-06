<template>
    <div :class="['JopItem-comp',data.featured == true ? 'featured': '']">
        <img class="logo" :src="require(`../../assets/${data.logo}.svg`)" alt="logo">
        <div class="details">
            <div class="info">
                <p class="company">{{ data.company }}</p>
                <FilledDiv v-if="data.new" text="NEW!"/>
                <FilledDiv v-if="data.featured" text="FEATURED" bgColor="hsl(180, 14%, 20%)"/>
            </div>
            <p class="position">{{ data.position }}</p>
            <div class="contract-details">
                <p class="posted-at">{{ data.postedAt }}</p>
                <p class="contract">{{ data.contract }}</p>
                <p class="location">{{ data.location }}</p>
            </div>
        </div>
        <hr class="phone-hr">
        <div class="langs">
            <FilledDiv v-for="filter , index in [data.role,data.level,...data.languages,...data.tools]" :key="index"
            @click="$emit('select-filter',filter)" 
            :text="filter" bgColor="transparent" bgColorHover="hsl(180, 29%, 50%)"  textColor="hsl(180, 29%, 50%)" textColorHover="white" borderRadius="5px" />
        </div>
    </div>
</template>

<script>
import FilledDiv from "../Ui/FilledDiv"
export default {
    name: "JopItem",
    components:{
        FilledDiv,
    },
    props: { data:Object },
    setup(props,{emit}) {
        const selectFilter = (filter) => {
            console.log("1",filter)
            
        }
        return { selectFilter }
    },
}
</script>

<style lang="scss" scoped>
@import "../../shared";
.JopItem-comp {
    width: 100%;
    display: flex;
    column-gap: 15px;
    align-items: center;
    box-shadow: #5ba4a45c 2px 5px 25px 0px;
    border-radius: 5px;
    position: relative;
    &.featured { border-left: hsl(180, 29%, 50%) solid 5px; }    

    padding: mathFromPcToTablet(30,20) mathFromPcToTablet(30,15);
    @include media("<=tablet",">phone") {
        column-gap: mathFromTabletToPhone(15,10);
    }
    @include media("<=phone") {
        flex-direction: column;
        align-items: self-start;
        padding: mathFromPhoneToMinWidth(50,40) mathFromPhoneToMinWidth(20,10) mathFromPhoneToMinWidth(40,20);
        row-gap: mathFromPhoneToMinWidth(15,10);
    }
    @include media("<=min-width") {
        padding: 40px 10px 20px;
        row-gap: 10px;
    }
    .logo {
        flex: 0;
        width: mathFromPcToTablet(88,60);
        @include media("<=tablet",">phone") {
            width: 60px;
        }
        @include media("<=phone") {
            width: 60px;
            position: absolute;
            top: -25px;
            left: 15px;
        }
    }
    .details {
        display: flex;
        flex-direction: column;
        row-gap: 10px;
        flex: 3;
        
        @include media("<=phone") {
            row-gap: 15px;
        }
        .info {
            display: flex;
            align-items: center;
            column-gap: 10px;
            .company {
                font-weight: 700;
                color: hsl(180, 29%, 50%);
                cursor: pointer;

                font-size: mathFromPcToTablet(13,10);
                @include media("<=phone",">min-width") {
                    font-size: mathFromPhoneToMinWidth(14,11);
                }
                @include media("<=min-width") {
                    font-size: 11px;
                }
            }
        }
        .position {
            font-weight: 700;
            color: hsl(180, 29%, 50%);
            cursor: pointer;
            width: fit-content;

            font-size: mathFromPcToTablet(16,13);
            @include media("<=tablet",">phone") {
                font-size: mathFromTabletToPhone(13,12);
            }
            @include media("<=phone") {
                color: rgb(44, 58, 58);
                font-size: mathFromPhoneToMinWidth(17,13);           
            }
            @include media("<=min-width") {
                font-size: 13px;           
            }
        }
        .contract-details {
            display: flex;
            column-gap: 25px;
            P {
                color: hsl(180, 8%, 52%);
                font-size: mathFromPcToTablet(14,11);
                @include media("<=tablet",">phone") {
                    font-size: mathFromTabletToPhone(11,10);
                }
                @include media("<=phone",">min-width") {
                    font-size: mathFromPhoneToMinWidth(14,10);           
                }
                @include media("<=min-width") {
                    font-size: 10px;           
                }
            }
            .contract, .location {
                display: list-item;
            }
        }
    }
    .phone-hr {
        display: none;
        @include media("<=phone") {
            display: inline-block;
            width: 100%;
        }
    }
}
</style>
<style lang="scss">
@import "../../shared";
.langs {
    display: flex;
    flex: 0;
    column-gap: mathFromPcToTablet(10,0);

    @include media("<=phone") {
        column-gap: mathFromTabletToPhone(15,10);
        flex-wrap: wrap;
        width: 100%;
    }
    @include media("<=min-width") {
        column-gap: 10px;
    }

    .FilledDiv {
        padding: 16px 10px;
        border-radius: 5px;
        cursor: pointer;
        p {
            font-weight: 700;
            font-size: mathFromPcToTablet(14,11);
            @include media("<=tablet",">phone") {
                font-size: mathFromTabletToPhone(11,9);
            }
            @include media("<=phone",">min-width") {
                font-size: mathFromPhoneToMinWidth(13,10);
            }
            @include media("<=min-width") { 
                font-size: 10px;
            }
        }    
    }
    
}
</style>