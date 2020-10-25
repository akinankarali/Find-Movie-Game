<template>
  <div class="card">
    <img :src="card.image" alt="">
  </div>
</template>
<script>
export default {
  props : ['card']
}
</script>
<style scoped>
.card{
  width: 200px;
  height: 232px;
  border-radius: 4px;
  border: 1px solid #666;
  transition: box-shadow .5s;
  margin-left: 16px;
}
.card:first-child{
  margin-left: 0;
}
.card:hover{
  box-shadow: 0 5px 48px #666666;
  transition: box-shadow .5s;
}
.card img{
  width: 100%;
  height: 100%;
}
</style>