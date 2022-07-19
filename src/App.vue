<template>

  <main>

    <p class="nextTurn">
      <span :="nextTurn.value">{{nextTurn}}</span> turn
    </p>
    

    <div class="gameGrid">
      <button        
        v-for="button in buttons"
        type="button" 
        @click="handleClick(button.id)">
        {{button.text}}
      </button>

      <div class="winView" v-if="winner" :="winner.value">
        <div class="normal">
          <p>{{winner}}</p>
        </div>
        <button @click="resetGrid"><ion-icon name="refresh-outline"></ion-icon></button>
        <div class="flipped">
          <p>{{winner}}</p>
        </div>

      </div>

    </div>

    <p class="nextTurn flipped">
      <span :="nextTurn.value">{{nextTurn}}</span> turn
    </p>

  </main>

</template>

<script setup>
  import { ref } from 'vue'
 
  const buttons = ref([])

  for (let i = 0; i < 9; i++) {

    buttons.value.push(
      {
        id: i,
        text: ''
      }
    )

  }

  const nextTurn = ref('O')
  const handleClick = (buttonId) => {

    if( buttons.value[buttonId].text == '' ) {
      buttons.value[buttonId].text = nextTurn.value
      nextTurn.value = nextTurn.value == 'O' ? 'X' : 'O'
    }
    checkWin()

  }

  const winner = ref('')
  const checkWin = () => {

    if(
      (buttons.value[0].text + buttons.value[1].text + buttons.value[2].text == 'OOO') || 
      (buttons.value[3].text + buttons.value[4].text + buttons.value[5].text == 'OOO') ||
      (buttons.value[6].text + buttons.value[7].text + buttons.value[8].text == 'OOO') ||
      (buttons.value[0].text + buttons.value[3].text + buttons.value[6].text == 'OOO') ||
      (buttons.value[1].text + buttons.value[4].text + buttons.value[7].text == 'OOO') ||
      (buttons.value[2].text + buttons.value[5].text + buttons.value[8].text == 'OOO') ||
      (buttons.value[0].text + buttons.value[4].text + buttons.value[8].text == 'OOO') ||
      (buttons.value[2].text + buttons.value[4].text + buttons.value[6].text == 'OOO')
      ){
        winner.value = 'The winner is O!'
        return
      }

    if(
      (buttons.value[0].text + buttons.value[1].text + buttons.value[2].text == 'XXX') || 
      (buttons.value[3].text + buttons.value[4].text + buttons.value[5].text == 'XXX') ||
      (buttons.value[6].text + buttons.value[7].text + buttons.value[8].text == 'XXX') ||
      (buttons.value[0].text + buttons.value[3].text + buttons.value[6].text == 'XXX') ||
      (buttons.value[1].text + buttons.value[4].text + buttons.value[7].text == 'XXX') ||
      (buttons.value[2].text + buttons.value[5].text + buttons.value[8].text == 'XXX') ||
      (buttons.value[0].text + buttons.value[4].text + buttons.value[8].text == 'XXX') ||
      (buttons.value[2].text + buttons.value[4].text + buttons.value[6].text == 'XXX')
      ){
        winner.value = 'The winner is X!'
        return
      }

      let allChecked = true

      for (const button of buttons.value) {
        if(button.text == ''){
          allChecked = false
        }
      }

      if(allChecked){
        winner.value = "It's  a draw!"
      }

  }

  const resetGrid = () => {
    for (let i = 0; i < 9; i++) {
      buttons.value[i].text = ''
    }
    winner.value = ''
  }
</script>

<style>

  html * {
    font-family: Arial, Helvetica, sans-serif;
    box-sizing: border-box;
    margin: 0%;
    padding: 0%;
  }

  main {
    width: 100%;
    height: 90vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .nextTurn {
    font-size: 2rem;
  }
    .nextTurn span {
      font-size: 3rem;
    }

  .gameGrid {
    position: relative;
    width: 340px;
    aspect-ratio: 1/1;
    background: #BCD9BA;
    display: flex;
    flex-wrap: wrap;
    padding: 10px;
    gap: 10px;
    border-radius: 20px;
    overflow: hidden;
    box-shadow:
      0px 0px 5.3px rgba(0, 0, 0, 0.028),
      0px 0px 17.9px rgba(0, 0, 0, 0.042),
      0px 0px 80px rgba(0, 0, 0, 0.07);
  }

    .gameGrid button {
      background: #C5E3C3;
      cursor: pointer;
      width: 100px;
      aspect-ratio: 1/1;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2rem;
      border-radius: 20px;
      border: 1px solid gray;
      color: black;
      box-shadow: 0px 0px 5.3px rgba(0, 0, 0, 0.028);
    }

  .winView {
    position: absolute;
    top: 0;
    left: 0;
    width: 340px;
    aspect-ratio: 1/1;
    background: #c5dac4;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 3em;
  }
    .winView div {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    .winView p {
      font-size: 2rem;
    }

    .winView button {
      width: max-content;
      border-radius: 50%;
      padding: .3em;
      background: #abbbaa;
      border: none;
      box-shadow:
        0px 0px 5.3px rgba(0, 0, 0, 0.028),
        0px 0px 17.9px rgba(0, 0, 0, 0.042),
        0px 0px 80px rgba(0, 0, 0, 0.07);
    }

  .flipped {
    transform: rotateZ(180deg);
  }

</style>