<script setup>
const props = defineProps(['score'])
</script>

<template>
  
  <div class="score-container">
    <div class="title">
        <span>ROCK</span>
        <span>PAPER</span>
        <span>SCISSORS</span>
          
    </div>
    <div class="score">
        <span>SCORE</span>
        <h1>{{ score }}</h1>
    </div>
  </div>
</template>

<style lang="scss">
.title {
    display: flex;
    flex-direction: column;
    span {
        font-size: large;
        color: white;
    }
}
.score {
    display: flex;
    flex-direction: column;
    background-color: white;
    color: #535061;
    padding: 5px 20px;
    border-radius: 5px;
    justify-content: center;
    align-items: center;
}
</style>