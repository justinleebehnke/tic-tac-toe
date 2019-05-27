<template>
    <div v-bind:class="tileObject" v-on:click="select()">
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
  computed: {
      tileObject () {
          return {
              tile: true,
              eligible: this.isEligible,
              selected: this.type !== '',
              x: this.type === 'X',
              o: this.type === 'O'
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
    border: 2px solid lightgray;
    width: 35px;
    height: 35px;
}
.eligible {
    border: 2px solid green;
}
.selected {
    font-size: 33px;    
}
.x {
    color: red;
}
.o {
    color: black;
}

</style>