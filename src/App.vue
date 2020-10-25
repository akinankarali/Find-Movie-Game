<template>
  <div class="">
    <component :is="activeComponent"></component>
  </div>
</template>
<script>
import  GameCards from './components/GameCards'
import  Failure from './components/Failure'
import  Celebrate from './components/Celebrate'
export default {
  data(){
    return{
      activeComponent : 'GameCards'
    }
  },
  components: {
    GameCards,
    Celebrate,
    Failure
  }

}
</script>
<style>
  body{
    font-family: sans-serif;
  }
</style>
