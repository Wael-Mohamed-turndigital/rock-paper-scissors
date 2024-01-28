<script setup>
  import Score from './components/Score.vue'
  import Game from './components/Game.vue'
  import Rules from './components/Rules.vue'
  import { ref } from 'vue';
  const total = ref(0)
  function gameResult(n){
    total.value += n
  }
</script>

<template>
  <main>
    <div class="container">
      <Score :score="total"/>
      <Game @gameResult="gameResult"/>
      <Rules />

    </div>
  </main>
</template>

<style lang="scss">

</style>
