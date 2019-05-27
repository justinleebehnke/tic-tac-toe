<template>
    <div class="gameWrapper">
        <div v-if="!winner" class="gameHeader">
            <h1>Current Turn: {{currentTurn}}</h1>
        </div>
        <div v-else class="gameHeader">
            <h1>Winner {{currentTurn}}</h1>
        </div> 
        <div class="minigame">
            <Tile 
                v-for="tile in this.tiles" :key="tile.id"
                :cardID="tile.id"
                :type="tile.type"
                :miniGameID="gameID"
                :currentTurn="currentTurn"
                :isEligible="tile.isEligible"
                v-on:tileSelected="updateTile(tile.id)">
            </Tile>
        </div>
    </div>
</template>
<script>
import Tile from './Tile'
export default {
    components: {
        Tile
    },
    data() {
        return {
            gameID: 11,
            tiles: [
                {id: 11, type: '', isEligible: true},
                {id: 12, type: '', isEligible: true},
                {id: 13, type: '', isEligible: true},
                {id: 21, type: '', isEligible: true},
                {id: 22, type: '', isEligible: true},
                {id: 23, type: '', isEligible: true},
                {id: 31, type: '', isEligible: true},
                {id: 32, type: '', isEligible: true},
                {id: 33, type: '', isEligible: true}
            ],
            currentTurn: 'O',
            winner: ''
        }
    },
    methods: {
        updateTile (tileID) {
            if (!this.winner) {
                for (let tile of this.tiles) {
                    if (tile.id === tileID) {
                        tile.type = this.currentTurn
                        tile.isEligible = false
                        if (!this.getVictor()) {
                            this.currentTurn = (this.currentTurn === 'O')? 'X' : 'O'
                        } else {
                            this.winner = this.currentTurn
                            this.tiles.forEach(tile => {
                                tile.isEligible = false
                            })
                        }
                    }
                }

            }
        },
        getVictor () {
            if (this.tilesMatch(0, 1, 2)) {
                return this.tiles[0].type
            }
            if (this.tilesMatch(3, 4, 5)) {
                return this.tiles[3].type
            }
            if (this.tilesMatch(6, 7, 8)) {
                return this.tiles[6].type
            }
            if (this.tilesMatch(0, 3, 6)) {
                return this.tiles[0].type
            }
            if (this.tilesMatch(1, 4, 7)) {
                return this.tiles[1].type
            }
            if (this.tilesMatch(2, 5, 8)) {
                return this.tiles[2].type
            }
            if (this.tilesMatch(0, 4, 8)) {
                return this.tiles[0].type
            }
            if (this.tilesMatch(2, 4, 6)) {
                return this.tiles[2].type
            }
            return ''
        },
        tilesMatch(index1, index2, index3) {
            return this.tiles[index1].type && 
            this.tiles[index1].type === this.tiles[index2].type && 
            this.tiles[index2].type === this.tiles[index3].type
        }
    }
}
</script>

<style>
.gameWrapper {
    display: block;
    text-align: center;
}
.minigame {
    max-width: 9px;
    display: grid;
    grid-template-columns: auto auto auto;
}
</style>
