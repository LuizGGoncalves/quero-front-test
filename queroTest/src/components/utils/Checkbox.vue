<template>
<div class="control-group">
  <label class="control control-checkbox">
    <div class="checkbox-description">{{ description }}</div>
    <input type="checkbox" v-model="isChecked" />
    <div class="control_indicator"></div>
  </label>
</div>
</template>
<script>
export default {
  name: "Checkbox",
  props: {
    description: {
      type: String,
    },
  },
  data() {
    return {
      isChecked:false
    }
  }
}
</script>
<style>

.control {
    font-family: arial;
    display: block;
    position: relative;
    padding-left: 25px;
    padding-top: 3px;
    cursor: pointer;
    font-size: 16px;
}

.control input {
    position: absolute;
    z-index: -1;
    opacity: 0;
}

.checkbox-description{

  font-weight: lighter
}

.control_indicator {
    position: absolute;
    top: 2px;
    left: 0;
    height: 20px;
    width: 20px;
    background: white;
    border: 1px solid #000000;
    border-radius: 5px;
}

.control:hover input ~ .control_indicator,
.control input:focus ~ .control_indicator {
    background: #cccccc;
}

.control input:checked ~ .control_indicator {
    background: #18ACC4;
}

.control_indicator:after {
    box-sizing: unset;
    content: '';
    position: absolute;
    display: none;
}

.control input:checked ~ .control_indicator:after {
    display: block;
}

.control-checkbox .control_indicator:after {
    left: 8px;
    top: 4px;
    width: 3px;
    height: 8px;
    border: solid #ffffff;
    border-width: 0 2px 2px 0;
    transform: rotate(45deg);
}

</style>