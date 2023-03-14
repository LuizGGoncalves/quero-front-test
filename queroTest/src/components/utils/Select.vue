<template>
  <div class="select-container">
    <label class="select-label">{{ label }}</label>
    <select class="select" :class="{'active': this.isOrderSelect }">
      <option value="">Selecione uma opção</option>
      <option class="select-option" v-for="(option, index) in options" :key="index" :value="option.value">
        {{ option.label }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
    },
    options: {
      type: Array,
      required: true
    },
    isOrderSelect: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      selectedValue: null
    }
  },
  watch: {
    selectedValue(newVal) {
      this.$emit('input', newVal)
    },
  },
}
</script>
<style>
.select-container {
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
}

.select {
  border: 1px solid #b9bfc7;
  background-color: transparent;
  box-shadow: none;
  padding: 10px;

}

.active {
  border: none;
  color:#18ACC4;
  font-weight: bold;
  padding: 0px 0px ;
}

.active option {
  font-weight: bold;
  border: none;
}


label {
  width: 100%;
  font-weight: bold;
}
</style>
