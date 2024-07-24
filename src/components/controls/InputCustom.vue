<template>
    <div class="input-custom">
        <div v-if="title"
             class="input-label">
            {{ title }}
        </div>
        <input
            v-model="proxyValue"
            class="input"
            :class="[
                setType,
                {'error': iError },
                {'focused': focused },
                {'active': proxyValue },
            ]"
            :autocomplete="autocomplete"
            :disabled="disabled"
            :form="form"
            :min="min"
            :max="max"
            :maxlength="maxlength"
            :name="name"
            :pattern="pattern"
            :placeholder="placeholder"
            :readonly="readonly"
            :required="required"
            :size="size"
            :step="step"
            :type="type"
            @input="onInput"
            @change="onChange"
            @focus="focused = true"
            @blur="focused = false"
            @keydown="onKeydown"
        />
        <div v-if="iError"
             class="input-error">
            {{ iErrorName }}
        </div>
    </div>
</template>

<script>
import '@/assets/css/controls/input-custom.scss'

export default {
  props: {
    // Default Input Props
    autocomplete: { type: String, default: null },
    title: { type: String, default: null },
    disabled: { type: Boolean, default: null },
    form: { type: String, default: null },
    max: { type: Number, default: null },
    maxlength: { type: Number, default: null },
    min: { type: Number, default: null },
    minlength: { type: Number, default: null },
    name: { type: String, default: null },
    pattern: { type: String, default: null },
    placeholder: { type: String, default: null },
    readonly: { type: Boolean, default: null },
    required: { type: Boolean, default: null },
    size: { type: Number, default: null },
    step: { type: Number, default: null },
    type: { 
      type: String, 
      default: 'text' 
    },
    inputType: { 
      type: String, 
      default: null
    },
    modelValue: { type: [String, Number], default: null },

    // Custom Input Props
    bName: { type: String, default: null },
    iError: { type: Boolean, default: false },
    iErrorName: { type: String, default: null },
    bIcon: { type: String, default: null },
  },
  data() {
    return {
      proxyValue: this.modelValue,
      focused: false,
    }
  },
  computed: {
    setType() {
      if (this.inputType) {
        return "input_" + this.inputType;
      }
      return null;
    },
  },
  watch: {
    modelValue(newValue) {
      this.proxyValue = newValue
    }
  },
  mounted() {
    this.proxyValue = this.modelValue
  },
  methods: {
    onInput(event) {
      const newValue = event.target.value
      this.proxyValue = newValue
      this.$emit('input', newValue)
      this.$emit('update:modelValue', newValue)
    },
    onChange(event) {
      const newValue = event.target.value
      this.proxyValue = newValue
      this.$emit('change', newValue)
    },
    onKeydown(event) {
      if (['-', '+', '.'].includes(event.key) && this.type == 'number') {
        event.preventDefault();
      }
    }
  },
}
</script>