<template>

  <nav>
    <p>Tic - Tac - Toe</p>
  </nav>

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

    </div>

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
    }

    nextTurn.value = nextTurn.value == 'O' ? 'X' : 'O'
  }

</script>

<style>

  html * {
    font-family: Arial, Helvetica, sans-serif;
    box-sizing: border-box;
    margin: 0%;
    padding: 0%;
  }

  nav {
    background: lightcyan;
    padding: .3em;
    font-size: 2rem;
    text-align: center;
  }

  main {
    width: 100%;
    height: 80vh;
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
    width: 340px;
    aspect-ratio: 1/1;
    background: lightcoral;
    display: flex;
    flex-wrap: wrap;
    padding: 10px;
    gap: 10px;
    border-radius: 20px;
  }

    .gameGrid button {
      cursor: pointer;
      width: 100px;
      aspect-ratio: 1/1;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2rem;
      border-radius: 20px;
      border: 1px solid gray;
      box-shadow: 0px 0px 5.3px rgba(0, 0, 0, 0.028);
    }

</style>
