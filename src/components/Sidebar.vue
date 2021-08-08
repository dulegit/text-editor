<template>
	<div class="sidebar">
    <div class="container pb-0">
      <div class="row row--max">
        <div class="col">
          <div class="sidebar__title">
            Text Layer
          </div>
        </div>
      </div>
    </div>
    <div class="sidebar__form">
      <form
        class="form"
        @submit.prevent
      >
        <div class="container">

          <!-- ROW -->
          <div class="row row--max-auto">
            <div class="col">
              <div class="form__field">
                <label class="form__label" for="form-text">Enter text</label>
                <input
                  v-model="textLayer.text"
                  @keydown.enter="emitUpdateTextbox"
                  @change="emitUpdateTextbox"
                  class="form__input"
                  type="text"
                  id="form-text"
                >
              </div>
            </div>
            <div class="col">
              <div class="form__field">
                <button
                  class="form__button"
                  @click="emitCreateCanvas"
                >+</button>
              </div>
            </div>
          </div>

          <!-- ROW -->
          <div class="row">
            <div class="col col-6">
              <div class="form__field">
                <label class="form__label" for="form-font-size">Font size</label>
                <input
                  v-model="textLayer.fontSize"
                  @keydown.enter="emitUpdateTextbox"
                  @change="emitUpdateTextbox"
                  class="form__input"
                  type="number"
                  id="form-font-size"
                >
              </div>
            </div>
            <div class="col col-6">
              <div class="form__field">
                <label class="form__label" for="form-line-height">Line height</label>
                <input
                  v-model="textLayer.lineHeight"
                  @keydown.enter="emitUpdateTextbox"
                  @change="emitUpdateTextbox"
                  class="form__input"
                  type="number"
                  id="form-line-height"
                >
              </div>
            </div>
          </div>

          <!-- ROW -->
          <div class="row row--max">
            <div class="col">
              <div class="form__field">
                <label class="form__label">Change font family</label>
                <select
                  v-model="textLayer.fontFamily"
                  @change="emitUpdateTextbox"
                  class="form__input"
                >
                  <option
                    v-for="font in fontFamilyList"
                    :key="font"
                  >
                    {{ font }}
                  </option>
                </select>
              </div>
            </div>
          </div>

        </div>
      </form>
    </div>
	</div>
</template>
<script>
export default {
	name: 'Sidebar',
  props: ['textLayer'],
  data() {
    return {
      fontFamilyList: [
        'Arial',
        'Times New Roman',
        'Helvetica',
        'Times',
        'Courier New',
        'Verdana',
        'Courier',
        'Arial Narrow',
        'Candara',
        'Geneva'
      ],
    }
  },
  methods: {
    emitCreateCanvas() {
      this.$emit('emitCreateCanvas')
    },
    emitUpdateTextbox(e) {
      e.preventDefault();
      if (e.type === 'keydown' && e.keyCode === 13) {
        e.target.blur()
      }
      this.$emit('emitUpdateTextbox')
    }
  }
}
</script>
<style scoped>
.sidebar {
  grid-column: 10/13;
  grid-row: 2;
  min-height: calc(100vh - 60px);
  background: #fff;
  box-shadow: -2px 4px 6px rgb(0 0 0 / 20%);
}
.sidebar__title {
  border-bottom: 1px solid var(--background);
  padding-bottom: 20px;
  font-weight: 700;
}

.container {
  display: grid;
  gap: 20px;
  padding: 20px;
}
.pb-0 {
  padding-bottom: 0!important;
}
.row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: end;
  gap: 20px;
}
.row--max {
  grid-template-columns: 1fr;
}
.row--max-auto {
  grid-template-columns: 1fr auto;
}
.form__field {
  display: grid;
}
.form__label {
  padding-bottom: 4px;
  font-size: 0.875rem;
}
.form__input {
  padding: 4px;
  border-radius: 4px;
  border: 1px solid var(--background);
  height: 24px;
}
.form__button {
  color: #fff;
  background: var(--primary);
  width: 22px;
  height: 22px;
  border: none;
  border-radius: 4px;
  font-weight: 700;
  cursor: pointer;
}
</style>