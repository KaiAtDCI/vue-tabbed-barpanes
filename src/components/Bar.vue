<template>
  <div id="bar" ref="bar" @click.stop="onClick($event)">
    <div id="upper" :style="{ height: upperHeight + 'px' }"/>
    <div id="lower" :style="{ height: lowerHeight + 'px' }">
      <div id="value">{{ value.toFixed(2) }}</div>
    </div>
  </div>
</template>

<script>
  export default {

    name: 'Bar',

    props: {
      initialValue: Number,
    },

    emits: {
      onchange: () => true,     // ToDo: change to real validator or delete !?
    },

    data() {
      return {
        value: this.initialValue,
        elementHeight: 100,
        elementTop: 100,
      }
    },

    computed: {
      lowerHeight() { return this.elementHeight * this.value; },
      upperHeight() { return this.elementHeight * (1 - this.value); }
    },

    created() {
      this.emitValue();
    },

    mounted() {
      window.addEventListener("resize", this.onResize);
      this.onResize();
    },

    methods: {
      onClick(event) {
        this.value =  1 - (event.clientY - this.elementTop) / this.elementHeight;
        this.emitValue();
      },
      onResize() {
        const element = this.$refs.bar;
        this.elementTop = element.getBoundingClientRect().top;
        this.elementHeight = element.getBoundingClientRect().height;
      },
      emitValue() {
        this.$emit('onchange', this.value);
      }
    },
  }
</script>

<style scoped>

  #bar {
    display: flex;
    flex-direction: column;
    min-width: 3rem;
    height: 100%;
    padding: 0;
    border: 0;
    margin: 0;
    cursor: crosshair;
  }

  #upper {
    /* height: set via template style binding */
  }

  #lower {
    /* height: set via template style binding */
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    user-select: none;
    background-color: lightsteelblue;
    font-family: "Courier 10 Pitch",serif;
    color: black;
  }
</style>