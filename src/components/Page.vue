<template>
  <div>
    <header>
      <h1>Border Radius Previewer</h1>
    </header>
    <div class="layout-box">
      <div class="box" :style="styledBorderRadius"></div>
    </div>
    <form novalidate>
      <label for="border-radius">border-radius: </label>
      <input type="text" id="border-radius" v-model="borderRadius" />
      <div class="tooltip">
        <button @click.prevent="copyText" @mouseout="undoTooltipText">
          <span class="tooltip-text">{{ tooltipText }}</span>
          Copy
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      borderRadius: "0% 0% 0% 0%",
      tooltipText: "Copy to clipboard"
    }
  },
  computed: {
    styledBorderRadius () {
      return {
        "border-radius": this.borderRadius
      }
    }
  },
  methods: {
    copyText () {
      let copyText = document.getElementById("border-radius")
      copyText.select();
      copyText.setSelectionRange(0, 99999);

      document.execCommand("copy");
      window.getSelection().removeAllRanges();

      this.tooltipText = "Copied!"
    },

    undoTooltipText () {
      this.tooltipText = "Copy to clipboard"
    }
  }
}
</script>

<style scoped>
header {
  height: 20%;
}

.layout-box {
  margin-left: auto;
  margin-right: auto;
  border: 3px dashed rgba(0, 0, 0, 0.4);
  width: 55vmin;
  height: 55vmin;
}

.box {
  background: linear-gradient(45deg, #3023AE, #3f69e8);
  width: 100%;
  height: 100%;
  border-radius: 50%;
}

form {
  margin: 3% 3% auto;
}

label {
  text-align: left;
  font-size: 1.35em;
  margin: 5px;
}

input {
  text-align: center;
  font-size: 1.25em;
  padding: 10px 12.5px;
  background: #F8F8F8;
  box-shadow: none;
  outline: none;
  border: none;
}

input:focus {
  background: #e9f5fb;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltip-text {
  visibility: hidden;
  text-align: center;
  position: absolute;
  /* left: 50%; */
  bottom: 150%;
  background: #555;
  width: 200%;
  border-radius: 6px;
  padding: 5px;
  margin-left: -90%;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip .tooltip-text::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: 5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}

.tooltip:hover .tooltip-text {
  visibility: visible;
  opacity: 1;
}

button {
  font-size: 1.25em;
  padding: 10px 30px;
  background: blue;
  font-weight: bold;
  color: white;
  outline: none;
  text-decoration: none;
  position: relative;
  z-index: 2;
}

button::before,
button::after {
  position: absolute;
  z-index: -1;
  display: block;
  content: '';
}

button,
button::before,
button::after {
  -webkit-transition: all .3s;
  transition: all .3s;
}

button:hover {
  background-color: red;
  cursor: pointer;
}

button::after {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  -webkit-transform: scale(.5);
  transform: scale(.5);
  display: block;
  content: '';
  z-index: -1;
}

button:hover::after {
  background: red;
  -webkit-transform: scale(1);
  transform: scale(1);
}
</style>
