<template>
  <div class="background-header-container">
    <img  class="header-desktop" src="./assets/bg-header-desktop.svg" alt="bg-header-desktop">
  </div>
  <FiltterBox v-if="selectedFillters.length > 0" :selectedFillters="selectedFillters" @un-select-filter="unSelectFilter" @un-select-all="unSelectAll"/>
  <JopList :jopData="[...filteredJopData]" @select-filter="selectFilter"/>
</template>

<script>
import { ref, watch } from "vue"
import JopList from "./components/Jop/JopList"
import FiltterBox from "./components/Ui/FilterBox"
export default {
  name: 'App',
  components: {
    JopList,
    FiltterBox
  },
  setup(){
    const jopData = ref(require("./data.json"))
    const filteredJopData = ref(jopData.value)
    const filterData = () => {
      if(!selectedFillters.value.length) { 
        filteredJopData.value = jopData.value
        return
      }
      filteredJopData.value =  jopData.value.filter(data => {
        let filters = [data.role,data.level,...data.languages,...data.tools]
        let fitsAllFilters = false
        for( let i = 0; i < selectedFillters.value.length; i++ ) {
          if(filters.includes(selectedFillters.value[i])) {
            fitsAllFilters = true
          } else {
            return false
          }
        }
        return fitsAllFilters
      })
    }

    const selectedFillters = ref([])
    watch(selectedFillters,() => {
      console.log("test",selectedFillters.value.length)
      filterData()
    },{ deep: true })
    const selectFilter = (filter) => {
      if(selectedFillters.value.includes(filter)) { return }
      selectedFillters.value.push(filter)
    }
    const unSelectFilter = (filter) => {
      let indexOf = selectedFillters.value.indexOf(filter)
      selectedFillters.value.splice(indexOf,1)
    }
    const unSelectAll = () => {
      selectedFillters.value = []
    }

    return { filteredJopData , selectedFillters , selectFilter , unSelectFilter , unSelectAll}
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Spartan:wght@500;700&display=swap');
@import "./shared";
html,body,#app {
  width: 100%;
  height: 100%;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Spartan', sans-serif;
}
html {
  min-width: $min-width * 1px;
}
#app {
  height: fit-content;
  box-sizing: content-box;
  padding-bottom: 1px;
}

.background-header-container {
  background: hsl(180, 29%, 50%);
  overflow: hidden;
  width: 100%;

  height: mathFromPcToTablet(208,180);
  @include media("<=phone",">min-width") {
    height: mathFromPhoneToMinWidth(180,170);
  }
  @include media("<=min-width") {
    height: 170px;
  }
  .header-desktop {
  width: 100%;
  height: 100%;
    @include media("<=pc",">tablet") {
      width: mathFromPcToTablet(1806,1160);
      transform: translateX(mathFromPcToTablet(0,-360));
    }
    @include media("<=tablet",">phone") {
      width: mathFromTabletToPhone(1160,950);
      transform: translateX(mathFromTabletToPhone(-360,-350));
    }
    @include media("<=phone",">min-width") {
      width: mathFromPhoneToMinWidth(1050,1125);
      transform: translateX(mathFromPhoneToMinWidth(-450,-800));
    }
    @include media("<=min-width") {
      width: 1125px;
      transform: translateX(-800px);
    }
  }
}
.JopList-comp {
  margin: 30px auto;
}
</style>
