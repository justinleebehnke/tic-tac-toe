<template>
    <div class="gameWrapper">
        <div v-if="winner" class="gameOver">
            <div v-if="winner === 'X'" class="x">
                {{this.winner}}
            </div>
            <div v-else class="o">
                {{this.winner}}
            </div>
        </div>
        <div v-else v-bind:class="gameObject">
            <Tile 
                v-for="tile in this.tiles" :key="tile.id"
                :cardID="tile.id"
                :type="tile.type"
                :miniGameID="gameID"
                :currentTurn="currentTurn"
                :isEligible="isEligible"
                v-on:tileSelected="updateTile(tile.id)">
            </Tile>
        </div>
    </div>
</template>
<script>
import Tile from './Tile'
export default {
    props: {
        currentTurn: {
            type: String,
            required: true,
            validator: function (value) {
                return ['O', 'X'].indexOf(value) !== -1
            } 
        },
        gameID: {
            type: Number,
            required: true
        },
        winner: {
            type: String,
            required: true
        },
        isEligible: {
            type: Boolean,
            required: true
        }
    },
    components: {
        Tile
    },
    computed: {
        gameObject () {
            return {
                minigame: true,
                eligible: this.isEligible
            }
        }
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
            ]
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
                            this.$emit('advanceTurn')
                        } else {
                            this.$emit('winnerFound')
                            this.$emit('advanceTurn')
                            this.toggleEligibilityOnUnFilledTiles()
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
        },
        toggleEligibilityOnUnFilledTiles() {
            this.tiles.forEach(tile => {
                if (tile.type === '') {
                    tile.isEligible = !tile.isEligible
                }
            })
        }
    }
}
</script>

<style>
.gameWrapper {
    border: 1px solid black;
    display: block;
    text-align: center;
    max-width: 113px;
    border: 1px black;
}
.gameOver {
    width: 113px;
    height: 113px;
    font-size: 100px;
}
.x {
    color: white;
}
.o {
    color: white;
}
.minigame {
    border: 1px black;
    margin: auto;
    display: grid;
    grid-template-columns: auto auto auto;
    background: black;
}
.eligible {
    border: 1px solid black;
}
.inEligible {
    border: 1px solid black;
}
</style>
