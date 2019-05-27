<template>
    <div>
        <h1>Game Board</h1>
        <div id="board">
            <MiniGame
                v-for="miniGame in this.miniGames" :key="miniGame.id"
                >
            </MiniGame>
        </div>
    </div>
</template>

<script>
import MiniGame from './MiniGame'
export default {
    components: {
        MiniGame
    },
    data () {
        return {
            miniGames: [
                {id: 11, winner: '', isEligible: true},
                {id: 12, winner: '', isEligible: true},
                {id: 13, winner: '', isEligible: true},
                {id: 21, winner: '', isEligible: true},
                {id: 22, winner: '', isEligible: true},
                {id: 23, winner: '', isEligible: true},
                {id: 31, winner: '', isEligible: true},
                {id: 32, winner: '', isEligible: true},
                {id: 33, winner: '', isEligible: true}
            ]
        }
    }
}
</script>

<style>
#board {
    display: grid;
    max-width: 343px;
    grid-template-columns: auto auto auto;
    grid-row-gap: 2px;
    margin: auto;
}
</style>



