<template>
  <div class="game-area">
    <p>{{answer}}</p>
    <h1 class='title'>Find <span>the correct</span> <strong>movie ?</strong> </h1>
    <h4 class="desc">Select one movie card and then click the question mark</h4>
    <div class="container">
      <transition-group name="rotate-all" appear class="card-container">
        <app-card
            :class="{'shadow' : selectedCard == card.id}"
            @click.native="selectedCard = card.id"
            v-for="card in cards"
            :card="card"
            :key="card.id"
        ></app-card>
      </transition-group>
    </div>
    <div class="container">
      <transition name="rotate" mode="out-in">
        <component
            @click.native="showCard(answer)"
            :is="activeCard"
            :card="answer"
        ></component>
      </transition>
    </div>
  </div>
</template>
<script>
import Card from './Card'
import DefaultCard from './DefaultCard'
export default {
  components : {
    appCard: Card,
    appDefaultCard: DefaultCard
  },
  data(){
    return{
      selectedCard : null,
      answer : {},
      activeCard: 'app-default-card',
      cards:[
        {id: 1, component:'app-card', image:'/src/assets/Braveheart.jpg'},
        {id: 2, component:'app-card', image:'/src/assets/captainFantastic.jpg'},
        {id: 3, component:'app-card', image:'/src/assets/forrestGump.jpg'},
        {id: 4, component:'app-card', image:'/src/assets/spiritedAway.jpg'},
        {id: 5, component:'app-card', image:'/src/assets/wall_e.jpg'}
      ]
    }
  },
  created() {
    let answer = Math.ceil(Math.random() * this.cards.length);
    this.answer = this.cards[answer - 1]
  },
  methods : {
    showCard(answer){
      if (this.selectedCard == null){
        alert('First, you should select a card');
      }else{
        this.activeCard = answer.component;
        setTimeout(()=>{
          if (answer.id == this.selectedCard){
            this.$emit('isCorrectEvent', 'Celebrate')
          }else{
            this.$emit('isCorrectEvent', 'Failure')
          }
        },2000)
      }
    }
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

  .rotate-enter{}
  .rotate-enter-active{
    animation: rotate-in ease-in-out 0.7s forwards;
  }
  .rotate-leave{}
  .rotate-leave-active{
    animation: rotate-out ease-in-out 0.7s forwards;
  }

  @keyframes rotate-in {
    from{
      transform: rotateY(90deg);
    }
    to{
      transform: rotateY(0deg);
    }
  }
  @keyframes rotate-out {
    from{
      transform: rotateY(0deg);
    }
    to{
      transform: rotateY(90deg);
    }
  }

</style>