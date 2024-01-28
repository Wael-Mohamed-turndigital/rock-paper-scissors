<script setup>
import { ref } from 'vue';
import iconPaper from '../assets/image/icon-paper.svg'
import iconRock from '../assets/image/icon-rock.svg'
import iconScissors from '../assets/image/icon-scissors.svg'
const playerSelection = ref(null)
const houseSelection = ref(null)
const emit = defineEmits(['gameResult'])
const result = ref('')
const options = [
    {
        id: 1,
        name:"paper",
        // link: "src/assets/image/icon-paper.svg",
        link: iconPaper,
        color: "yellow"
    },
    {
        id: 2,
        name:"rock",
        // link: "src/assets/image/icon-rock.svg",
        link: iconRock,
        color: "red"
    },
    {
        id: 3,
        name:"scissors",
        // link: "src/assets/image/icon-scissors.svg",
        link: iconScissors,
        color: "blue"
    }
]
function iconSelect(id) {

    playerSelection.value = options?.find(item => item.id == id)
    setTimeout(() => {
        const randomOptions = options.filter(item => item.id != id)
        const randomId = Math.floor(Math.random() * 2)
        houseSelection.value = randomOptions[randomId]
        setTimeout(() => {
            
            const playerResult = ( playerSelection.value.id + 1 ) == 3 ? ( playerSelection.value.id + 1 ) : ( playerSelection.value.id + 1 ) % 3
            if(playerResult == houseSelection.value.id) {
                result.value = 'YOU WIN'
                emit('gameResult', 1)
            }
            else {
                result.value = "YOU LOSE"
                emit('gameResult', -1)
            }
        }, 1000);
    }, 1000);
}
function resetGame() {
    playerSelection.value = null
    houseSelection.value = null
    result.value = ''
}
</script>

<template>
  
  <div class="game-container">
    <div class="select-container" v-if="!playerSelection">
        <div  v-for="option in options" :key="option.id" class="iconWrapper">
            <div :class="['icon-base', option.color]" @click="iconSelect(option.id)">
                <img :src="option.link" width="50px" height="50px" />
            </div>    
        </div>
        
    </div>
    <div v-else>
        <div class="selected-section">
            <div class="selected">
                <span>
                    YOU PICKED
                </span>
                <div :class="['icon-base', playerSelection?.color]">
                    <img :src="playerSelection?.link" width="50px" height="50px"/>
                </div>
            </div>
            <div v-if="result != ''" class="resultReset">
                <span class="status">
                    {{ result }}
                </span>
                <button class="resetButton" @click="resetGame">PLAY AGAIN</button>
            </div>
            <div class="selected" v-if="!houseSelection">
                <span>
                    THE HOUSE PICKED
                </span>
                <div class="blank" />
            </div>
            <div class="selected" v-else>
                <span>
                    THE HOUSE PICKED
                </span>
                <div :class="['icon-base', houseSelection?.color]">
                    <img :src="houseSelection?.link" width="50px" height="50px"/>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<style lang="scss">
.select-container {
    background-image: url('../assets/image/bg-triangle.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-size:contain;
    height:max-content;
    display: flex;
    flex-wrap: wrap;
    margin: auto;
    align-items: center;
}
.iconWrapper {
    width: 50%;
    margin: auto;
}
.triangle-base {
    display: flex;
    justify-content: space-between;
    gap: 70px;
}
.icon-base {
    display: flex;
    justify-content: center;
    justify-items: center;
    border-style: solid;
    border-width: 15px;
    border-radius: 50%;
    margin: auto;
    width: 100px;
    height: 100px;
    background-color: white;
    box-shadow: 0px 10px, 0px 5px inset;
    img {
        margin: auto;
    }
}
.yellow {
    border-color: yellow;
}
.red {
    border-color: red;
}
.blue {
    border-color: blue;
}
.selected-section {
    display: flex;
    justify-content: space-between;
    width: 100%;
    flex-wrap: wrap;
}
.selected {
    display: flex;
    flex-direction: column;
    gap: 5px;
    justify-content: center;
    align-items: center;
    font-size: large;
    color: white;
    margin: 0px 20px;
}
.status {
    font-size: large;
    margin: 10px auto;
}
.blank {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background-color: #16213d;
}
.resultReset {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    justify-items: center;
    color: white;
}
@media (max-width: 767.98px) {
    .selected {
        width: 50%;
    }
    .resultReset {
        // width: 100%;
        justify-content: center;
        padding-top: 40px;
        margin: auto;
        order: 3;
    }
}
.resetButton {
    padding: 10px 30px;
    border-radius: 5px;
}
</style>