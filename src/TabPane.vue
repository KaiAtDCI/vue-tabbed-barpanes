<template>
  <div id="app">
    <keep-alive>
      <component :is="currentTab" class="tab"/>
    </keep-alive>

    <button v-for="tab in tabs"
            :key="tab"
            :class="{ active: currentTab === tab }"
            @click="switchTab(tab)"
    >
      {{ tab }}
    </button>
  </div>

</template>

<script>
  import Tab1 from './components/Tab1.vue'
  import Tab2 from './components/Tab2.vue'

  export default {
    name: 'TabPane',
    components: {
      Tab1, Tab2
    },

    data() {
      return {
        tabs: ["Tab1", "Tab2"],
        currentTab: "Tab1",
      }
    },

    methods: {
      switchTab(id) {
        // console.log(`App.vue: switchTab(${id})`);
        this.currentTab = id;
      }
    },

    watch: {
      currentTab() {
        console.log(`App.vue: currentTab=${this.currentTab}`);
      }
    }

  }
</script>

<style scoped>

  * {
    box-sizing: content-box;
    padding: 0;
    margin: 0;
  }

  body {
    padding: 1em;
  }

  button {
    border: solid lightsteelblue;
    border-width: 0 1px 1px 1px;
    /*border-radius: 0 0 .25em .25em;*/
    padding: 0.25em;
  }
  .active {
    background-color: lightsteelblue;
  }

  .tab {
    border: 1px solid lightsteelblue;
  }
</style>
