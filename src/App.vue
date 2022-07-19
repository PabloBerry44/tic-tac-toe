<template>

  <nav>
    <p>Tic - Tac - Toe</p>
  </nav>

  <main>
    <div class="gameGrid">
      <input 
        type="button" 
        value=""
        v-for="button in buttons">
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
        value: ''
      }
    )

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
  }

  .gameGrid {
    width: 330px;
    aspect-ratio: 1/1;
    background: lightcoral;
  }

    .gameGrid input {
      width: 100px;
      aspect-ratio: 1/1;
      margin: 5px;
    }

</style>
