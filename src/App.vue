<template>
  <SideBar 
  @LengthCh="Length=$event"
  @XPosDestCh="XPosDest=$event"
  @USpeedCh="USpeed=$event"
  @WSpeedCh="WSpeed=$event"
  @AlphaCh="Alpha=$event"
  @StartCh="Started=$event"
  />
  <RiverBlock     
    :Length="Length"
    :XPosDest="XPosDest"
    :USpeed="USpeed"
    :WSpeed="WSpeed"
    :Alpha="Alpha"
    :Started="Started" />
</template>

<script>
import SideBar from './components/SideBar.vue'
import RiverBlock from './components/RiverBlock.vue';
export default {
  name: 'App',
  components: {
    SideBar,
    RiverBlock,
    RiverBlock,
  },
  data()
  {
    return{
      Length:30,
      XPosDest:0,
      USpeed:12,
      WSpeed:10,
      Alpha:90,
      Started:0,
    }
  }
}
</script>

<style>

</style>
