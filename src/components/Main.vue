<template>
  <div class="main">
    <div class="text-editor">
      <div class="text-editor__container">
        <canvas ref="textEditor" width="500" height="500" class="text-editor__content"></canvas>
      </div>
    </div>
    <Sidebar
      :textLayer="textLayer"
      v-on:emitCreateCanvas="createCanvas"
      v-on:emitUpdateTextbox="updateActiveTextbox"
    />
  </div>
</template>
<script>
import { fabric } from 'fabric';
import Sidebar from '@/components/Sidebar.vue'

export default {
  name: 'Main',
  components: {
    Sidebar
  },
  data(){
    return {
      canvas: null,
      textLayer: {
        text: '',
        fontSize: 32,
        lineHeight: 1,
        fontFamily: 'Arial'
      },
    }
  },
  mounted() {
    const ref = this.$refs.textEditor;
    this.canvas = new fabric.Canvas(ref);

    this.canvas.on('mouse:up', (e) => {
      if (e.target) {
        this.updateTextLayer(e.target)
      }
    })

    this.canvas.on('object:modified', (e) => {
      // reset scale before set font size and line height
      e.target.scaleX = 1;
      e.target.scaleY = 1;
      e.target.fontSize = this.textLayer.fontSize
      e.target.lineHeight = this.textLayer.lineHeight
    })

    this.canvas.on('object:scaling', (e) => {
      // calculate fontSize on resizing
      let fontSize = (e.target.fontSize * e.target.scaleX).toFixed();

      this.textLayer.fontSize = Number(fontSize);
    })

  },
  methods: {
    updateTextLayer(selected) {
      this.textLayer.text = selected.text;
      this.textLayer.fontSize = selected.fontSize;
      this.textLayer.lineHeight = selected.lineHeight;
      this.textLayer.fontFamily = selected.fontFamily;
    },
    createCanvas() {
      if (this.textLayer.text.length === 0) {
        return;
      }
      const text = new fabric.Textbox(this.textLayer.text, {
        fontFamily: this.textLayer.fontFamily,
        fontSize: this.textLayer.fontSize,
        lineHeight: this.textLayer.lineHeight,
        lockUniScaling: true
      })
      this.canvas.add(text);
      this.canvas.setActiveObject(text);
    },
    updateActiveTextbox() {
      let activeObject = this.canvas.getActiveObject();
      if (!activeObject) {
        return;
      }
      activeObject.set('text', this.textLayer.text);
      activeObject.set('fontSize', this.textLayer.fontSize);
      activeObject.set('lineHeight', this.textLayer.lineHeight);
      activeObject.set('fontFamily', this.textLayer.fontFamily);
      this.canvas.requestRenderAll();
    }
  }
}
</script>
<style scoped>
.main {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  background: var(--background);
}
.text-editor {
	grid-column: 1/10;
  grid-row: 2;
}
.text-editor__container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.text-editor__content {
  width: 100%;
  height: 100%;
  max-width: 500px;
  max-height: 500px;
  background: #fff;
  border: 1px solid var(--primaryText)
}
</style>