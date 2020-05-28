<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png"><br>
    <a href="javascript:;" @click="loadComponent">Click para carregar um componente dinamicamente</a>
    <div ref="container"></div>
  </div>
</template>

<script>
import Vue from 'vue';
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
  },
  methods: {
    loadComponent () {
      const ComponentClass = Vue.extend(HelloWorld);
      const instance = new ComponentClass({
        parent: this, // Important !
        propsData: {
          msg: 'Sou um componente instanciado dinamicamente!' // Props
        },
      })
      
      // Listener
      instance.$on('loaded', () => {
        console.log('Ready')
      });

      // Mount component (emit lifecycle mount event)
      instance.$mount();

      // Clear container
      this.$refs.container.innerHTML = null

      // Append DOM
      this.$refs.container.appendChild(instance.$el)
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
