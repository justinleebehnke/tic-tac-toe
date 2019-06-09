<template>
    <div>
        <h1>Ultimate Tic Tac Toe</h1>
        <div id="board">
            <MiniGame
                v-for="miniGame in this.miniGames" :key="miniGame.id"
                :gameID="miniGame.id"
                :currentTurn="currentTurn"
                v-on:advanceTurn="advanceTurn()"
                v-on:winnerFound="setWinner(miniGame.id)"
                :winner="miniGame.winner"
                :isEligible="miniGame.isEligible">
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
    methods: {
        advanceTurn () {
            if (!this.getOverallVictor()) {
                this.currentTurn = (this.currentTurn === 'O')? 'X' : 'O'
            } else {
                this.overAllWinner = this.currentTurn
                this.$children.forEach(miniGame => {
                    miniGame.toggleEligibilityOnUnFilledTiles()
                });
                this.miniGames.forEach(miniGame => {
                    miniGame.isEligible = false
                })
            }
        },
        setWinner (gameID) {
            for (let i = 0; i < this.miniGames.length; i++) {
                if (gameID === this.miniGames[i].id) {
                    this.miniGames[i].winner = this.currentTurn
                    break
                }
            }
        },
        getOverallVictor () {
            if (this.winnersMatch(0, 1, 2)) {
                return this.miniGames[0].winner
            }
            if (this.winnersMatch(3, 4, 5)) {
                return this.miniGames[3].winner
            }
            if (this.winnersMatch(6, 7, 8)) {
                return this.miniGames[6].winner
            }
            if (this.winnersMatch(0, 3, 6)) {
                return this.miniGames[0].winner
            }
            if (this.winnersMatch(1, 4, 7)) {
                return this.miniGames[1].winner
            }
            if (this.winnersMatch(2, 5, 8)) {
                return this.miniGames[2].winner
            }
            if (this.winnersMatch(0, 4, 8)) {
                return this.miniGames[0].winner
            }
            if (this.winnersMatch(2, 4, 6)) {
                return this.miniGames[2].winner
            }
            return ''
        },
        winnersMatch (index1, index2, index3) {
            return this.miniGames[index1].winner && 
            this.miniGames[index1].winner === this.miniGames[index2].winner && 
            this.miniGames[index2].winner === this.miniGames[index3].winner
        },
    },
    data () {
        return {
            currentTurn: 'O',
            overAllWinner: '',
            miniGames: [
                {id: 11, winner: '', isEligible: false},
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
    max-width: 339px;
    grid-template-columns: auto auto auto;
    margin: auto;
}
</style>



