<template>
  <div id="app">
         <div class="wrapper clearfix">
            <Players :scorePlayer="scorePlayer"
            :activePlayer="activePlayer"
            :currenScore="currenScore"/>
            
           <Controls
           @handleNewGame="handleNewGame"
           @handleRollDice="handleRollDice"
           @handleHoldDice="handleHoldDice"
           />
            <Dices :dice="dice"/>
       
        </div>
  </div>
</template>

<script>
import Players from "./components/Players"
import Controls from "./components/Controls"
import Dices from "./components/Dices"
import PopupRule from "./components/PopupRule"
export default {
  name: 'app',
  data () {
    return {
      activePlayer: 0,
      scorePlayer: [12,11],
      currenScore: 30,
      isPlaying: false,
      dice: [1,1],
    }
  },
  components:{
    Players,
    Controls,
    Dices,
    PopupRule,
  },
  methods:{
    nextPlayer(){
      this.activePlayer =this.activePlayer===0?1:0
      this.currenScore=0;
    },
    handleNewGame(){
       console.log('jejelfjla adfjal');
       this.isPlaying=true;
       this.activePlayer=0;
       this.scorePlayer=[0,0]
       this.currenScore=0
       this.dice=[1,1]
    },
    handleRollDice(){
      console.log("roll app");
      if(this.isPlaying){
        var dice1 = Math.floor(Math.random()*6)+1
        var dice2 = Math.floor(Math.random()*6)+1
        this.dice = [dice1,dice2]
        if(dice1===1||dice2==1){
          this.nextPlayer();
          setTimeout(() =>{alert(`người chơi ${this.activePlayer+1} đã quay trúng số 1 và mất lượt`)},20)
          
        }else{
          this.currenScore= this.currenScore+dice1+dice2
        }
      }else{
        alert('chua new game kia :v')
        //helloo
      }   
    },
    handleHoldDice(){
      if(this.isPlaying){
        let{scorePlayer, activePlayer, currenScore} =this
        let scoreOld = scorePlayer[activePlayer]
        let cloneScorePlayer =[...scorePlayer]
        cloneScorePlayer[activePlayer] =scoreOld + currenScore
        this.scorePlayer= cloneScorePlayer
        this.nextPlayer()
      }else{
         alert('chua new game kia :v')
      }
      
    }

  }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/dist/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}





</style>
