<template>
  <div id="app">
    <LoadingScreen v-if="isLoading"/>
    <div class="buttons-container">
      <input v-model="columns" type="number" placeholder="Set column quantity">
      <input v-model="lines" type="number"   placeholder="Set row quantity">
      <QuantityButton msg="Generate"/>     
    </div>
    <ApiCanvas :columns="columns" :lines="lines" />
  </div>
</template>

<script>
import QuantityButton from './components/QuantityButton.vue'
import ApiCanvas from './components/ApiCanvas.vue'
import LoadingScreen from './components/LoadingScreen.vue'

export default {
  name: 'App',
  components: {
    LoadingScreen,
    ApiCanvas,
    QuantityButton
  },
   data: function () {
    return {
      isLoading: true,
      lines: null,
      columns: null
    }
  },
  mounted() {
    this.apiMock()
  },
  methods: {
      apiMock() {
        let delay = new Promise((resolve) => {
          setTimeout(() => {           
            resolve(false)
          }, 2000);
        });
        delay.then(result => {
          this.isLoading = result;
        })  
      }
    }
}
</script>