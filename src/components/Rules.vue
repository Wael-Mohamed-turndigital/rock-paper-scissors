<script setup>
import RulesDetails from './RulesDetails.vue'
import { ref } from 'vue';
const isOpen = ref(false)
</script>

<template>
    <button class="rules-btn rules-container" @click="isOpen = true">
        RULES
    </button>
    <Teleport to="body">
        <div class="overlay" v-if="isOpen">
            <div  class="modal-details">
                <img src="../assets/image/icon-close.svg" width="20px" height="20px" class="close-btn" @click="isOpen = false" />
                <RulesDetails />
            </div>
        </div>
    </Teleport>
</template>

<style lang="scss">
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(128,128,128,0.5);
}
.rules-btn {
    padding: 5px 20px;
    border-radius: 5px;
    border: solid;
    border-width: 2px;
    background-color: transparent;
    color: white;
    border-color: white;
}
.modal-details {
    position: fixed;
    top: 20vh;
    left: 33vw;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-end;
    width: 30%;
    margin: auto;
    background-color: white;
    border-radius: 5px;
}
.close-btn {
    margin: 20px;
    cursor: pointer;
}
@media (max-width: 767.98px) {
    .modal-details {
        position: fixed;
        top: 0;
        left: 0;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-end;
        width: 100%;
        height: 100%;
        margin: auto;
        background-color: white;
    }
}
</style>