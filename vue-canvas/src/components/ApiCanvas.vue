<template>
  <canvas @click="draw(column, line)" id="canv" width="1000" height="500"></canvas>
</template>

<script>
export default {
  name: 'ApiCanvas',
  mounted() {
    this.draw(this.column, this.line)
    this.$root.$on('render', () => {
      this.draw(this.column, this.line)
    });
  },
  props: {
      lines: {
        type: String
      },
      columns: {
        type: String
      }
    },
  created: function () {
    
  },
  methods: {
    draw(lineQuantity, rowQuantity) {
      const canvas = document.getElementById('canv');
      let rectH = this.calcHW(canvas.height, rowQuantity) 
      let rectW = this.calcHW(canvas.width, lineQuantity) 
      if (canvas.getContext) {
        const ctx = canvas.getContext('2d');
        for (let i = 0; i < rowQuantity; i++) { // row loop
          for (let j = 0; j < lineQuantity; j++) {  // line loop
            ctx.fillStyle = this.fillColor()
            ctx.fillRect(j * rectW - 0.5, i * rectH - 0.5, rectW + 0.5, rectH + 0.5);
          }
        }
      }
    },
    calcHW(width, parts){
      return  width/parts;
    },
    fillColor(){
      let colorV = () => Math.round(Math.random() * 255);
      return 'rgba(' + colorV() + ',' + colorV() + ',' + colorV() + ')';
    }
  },
  computed: {
    line() {
      return this.lines || 2;
    },
    column() {
      return this.columns || 4;
    }
  }
}
</script>
