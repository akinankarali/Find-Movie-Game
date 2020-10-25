<template>
  <div class="container">
    <h1>You Lose. Try Again!</h1>
    <button @click="newGame">Start New Game</button>
  </div>
</template>
<script>
export default {
  methods: {
    newGame(){
      this.$emit('activeComponentEvent', 'GameCards')
    }
  }
}
</script>
<style scoped>
  .container{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: darkred;
  }
  .container h1{
    text-align: center;
    font-size: 48px;
    color: #fff;
  }
  .container button{
    cursor: pointer;
    width: 200px;
    background-color: #fff;
    color: darkred;
    border: 1px solid brown;
    height: 50px;
    font-size: 16px;
    border-radius: 4px;
    outline: none;
  }
  .container button:hover{
    background-color: lightgreen;
    color: #fff;
    transition: all 0.5s;
  }
</style>