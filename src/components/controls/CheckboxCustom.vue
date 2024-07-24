<template>
    <div
        class="checkbox" 
    >
        <input
            :id="id || name"
            :name="name"
            :checked="internalValue"
            type="checkbox"
            class="custom-checkbox"
            @click="handleClick"
        >
        <label
            :for="id || name"
            class="checkbox__label"
        >
            <slot>
                {{ text }}
            </slot>
        </label>
    </div>
</template>

<script>
import "@/assets/css/controls/checkbox-custom.scss";

export default {
props: {
  id: { type: String, default: null },
  name: { type: String, default: 'checkbox' },
  value: { type: Boolean, default: false },
  checked: { type: Boolean, default: false },
  text: { type: String, default: '' },

  // Checkbox types
  default: { type: Boolean, default: false },
},
data: () => ({
  internalValue: false
}),
watch: {
  value (val) {
    this.internalValue = val
  },
  checked (val) {
    this.internalValue = val
  },
  internalValue (val, oldVal) {
    if (val !== oldVal) {
      this.$emit('input', val)
    }
  }
},
created () {
  this.internalValue = this.value
  if (this.$options.propsData && 'checked' in this.$options.propsData) {
    this.internalValue = this.$options.propsData.checked;
  }
},
methods: {
  handleClick (e) {
    this.$emit('click', e)
    if (!e.isPropagationStopped) {
      this.internalValue = e.target.checked
    }
  }
}
}
</script>