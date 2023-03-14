<template>
  <div class="slider-container">
    <div class="slider-label">{{ label }}</div>
    <div class="slider-value">R${{ parseInt(currentvalue).toLocaleString('pt-BR') }}</div>
    <input class="slider" type="range" :min="min" :max="max" :step="step" :value="currentvalue" @input="updateValue"/>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true,
    },
    min: {
      type: Number,
      default: 0
    },
    max: {
      type: Number,
      default: 100
    },
    step: {
      type: Number,
      default: 1
    },
    value: {
      type: Number,
      default: 10000
    }
  },
  methods: {
    updateValue(event) {
      this.selectedValue = event.target.value
    }
  },
  data() {
    return {
      selectedValue: 10000
    }
  },
  computed: {
    currentvalue() {
      return this.selectedValue;
    }
  }
}
</script>

<style scoped>


.slider {
  -webkit-appearance:none;
  width: 100%;
  background-color: #007A8D;
  height: 3px;
  border-radius: 10px;
  outline: none;
  opacity: 0.7;
  -webkit-transition: opacity .2s;
  transition: opacity .2s;
}

.slider-label{
  font-weight: bold;;
}

.slider-value {
  padding-bottom: 5%;
}

.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance:none;
  background: #fff;
   border: 2px solid #18ACC4;
   width:25px;
   height:25px;
   border-radius:50%;
   cursor:pointer;
}

input[type="range"]::-webkit-slider-runnable-track::after {
  background: #ccc;
}


.slider::-moz-range-thumb {
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: black;
  color: black;
  cursor: pointer;
}


</style>
