<template>
  <div id="BarPane">
    <Bar v-for="barNumber in numberOfBars"
         :key="barNumber"
         :initial-value="1"
         @onchange="onBarChange($event, barNumber)"/>
  </div>
</template>

<script>

  import Bar from './Bar.vue';

  export default {
    name: 'BarPane',

    components: {
      Bar,
    },

    props: {
      numberOfBars: {
        type: Number,
        default: 10,
      }
    },

    data() {
      return {
        value: new Array(this.numberOfBars),
      }
    },

    methods: {
      onBarChange(event, barNumber) {
        const newValue = event.toFixed(2);
        this.value.splice(barNumber - 1, 1, newValue);
        this.emitValue();
      },
      emitValue() {
        this.$emit('onchange', this.value);
        console.log(this.value);
      },
    },
  }
</script>

<style>

  #BarPane {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    align-items: center;
    width: 100%;
    height: 100%;
  }

</style>