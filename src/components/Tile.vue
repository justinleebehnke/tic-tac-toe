<template>
    <div v-bind:class="tileObject" :style="tileStyle" v-on:click="select()">
        {{this.type}}
    </div>
</template>

<script>
export default {
  name: 'Tile',
  props: {
      cardID: {
        type: Number,
        required: true
      },
      type: {
        type: String,
        required: true,
        validator: function (value) {
            return ['O', 'X', ''].indexOf(value) !== -1
        }
      },
      miniGameID: {
        type: Number,
        required: true
      },
      currentTurn: {
          type: String,
          required: true,
          validator: function (value) {
            return ['O', 'X'].indexOf(value) !== -1
          }
      },
      isEligible: {
          type: Boolean,
          required: true
      }
      
  },
  data () {
      return {
          tileStyle: {
            borderBottom: (this.cardID < 30) ? (this.isEligible) ? '1px solid white' : '1px solid #292929' : '1px solid black',
            borderTop: (this.cardID >= 20) ? (this.isEligible) ? '1px solid white' : '1px solid #292929' : '1px solid black',
            borderRight: (this.cardID % 10 === 1 || this.cardID % 10 === 2) ? (this.isEligible) ? '1px solid white' : '1px solid #292929' : '1px solid black',
            borderLeft: (this.cardID % 10 === 2 || this.cardID % 10 === 3) ? (this.isEligible) ? '1px solid white' : '1px solid #292929' : '1px solid black',
            color: (this.isEligible) ? 'white' : '#292929'
          }
      }
  },
  computed: {
      tileObject () {
          return {
              tile: true,
              selected: this.type !== ''
          }
      }
  },
  methods: {
      select () {
          if (this.isEligible) {
              this.$emit('tileSelected')
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tile {
    border: 1px solid black;
    background-color: black;
    width: 35px;
    height: 35px;
}
.selected {
    font-size: 33px;    
}
</style>