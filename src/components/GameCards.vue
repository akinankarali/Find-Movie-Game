<template>
  <div class="game-area">
    <h1 class='title'>Find <span>the correct</span> <strong>movie ?</strong> </h1>
    <h4 class="desc">Select one movie card and then click the closed card</h4>
    <div class="container">
      <transition-group name="rotate-all" appear class="card-container">
        <Card
            :class="{'shadow' : selectedCard == card.id}"
            @click.native="selectedCard = card.id"
            v-for="card in cards"
            :card="card"
            :key="card.id"
        ></Card>
      </transition-group>
    </div>
    <div class="container">
      <DefaultCard />
    </div>
  </div>
</template>
<script>
import Card from './Card'
import DefaultCard from './DefaultCard'
export default {
  components : {
    Card,
    DefaultCard
  },
  data(){
    return{
      selectedCard : null,
      answer : {},
      cards:[
        {id: 1, component:'cards', image:'/src/assets/Braveheart.jpg'},
        {id: 2, component:'cards', image:'/src/assets/captainFantastic.jpg'},
        {id: 3, component:'cards', image:'/src/assets/forrestGump.jpg'},
        {id: 4, component:'cards', image:'/src/assets/spiritedAway.jpg'},
        {id: 5, component:'cards', image:'/src/assets/wall_e.jpg'}
      ]
    }
  },
  created() {
    let answer = Math.ceil(Math.random() * this.cards.length);
    this.answer = this.cards[answer - 1]
  }
}
</script>
<style  scoped>
  .title{
    text-align: center;
    color: rosybrown;
  }
  .title span{
    color: mediumpurple;
  }
  .title strong {
    color: darkred;
  }
  .desc{
    color: grey;
    text-align: center;
  }
  .container, .card-container{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 48px;
  }
  .shadow{
    box-shadow: 0 5px 48px #30969f!important;
    transition: box-shadow .5s;
  }

  //for animation and transition
  .rotate-all-enter{}
  .rotate-all-enter-active{
    animation: rotate-all ease-in-out 2s forwards;
  }
  .rotate-all-leave{}
  .rotate-all-leave-active{}

  @keyframes rotate-all {
    from{
      transform: rotateY(0);
    }
    to{
      transform: rotateY(360deg);
    }
  }
</style>