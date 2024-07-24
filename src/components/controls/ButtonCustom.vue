<template>
    <button
        class="button"
        :class="[setColor, { disabled: disabled }]"
        :autofocus="autofocus"
        :disabled="disabled"
        :form="form"
        :name="name"
        :type="type"
        @click="handleClick"
    >
        <slot>
            {{ value }}
        </slot>
        <svg-icon
            v-if="bIcon" 
            :icon="bIcon"
            class="button__icon"
            :stroke="bIconColor"
            :width="bIconSize"
            :height="bIconSize"
        />
    </button>
</template>

<script>
import "@/assets/css/controls/button-custom.scss";

export default {
  provide() {
    return {
      click: this.handleClick,
    };
  },
  props: {
    autofocus: { type: Boolean, default: false },
    disabled: { type: Boolean, default: false },
    form: { type: String, default: null },
    name: { type: String, default: null },
    type: { type: String, default: "button" },
    value: { type: [String, Number], default: null },
    bError: { type: Boolean, default: false },
    bErrorName: { type: String, default: null },
    bIcon: { type: String, default: null },
    bIconSize: { type: [String, Number], default: "24" },
    bIconColor: { type: String, default: "#FFFFFF" },
    bForm: { type: String, default: "default" },
  },
  computed: {
    setColor() {
      if (this.bForm) {
        return "button_" + this.bForm;
      }
      return null;
    },
  },
  methods: {
    handleClick(e) {
      return e;
    },
  },
};
</script>
