<!--
  dependencies:
  $ npm install maska
  
  to use error messages, should combine with Vuelidate ($ npm install @vuelidate/core @vuelidate/validators), but not required
-->

<template>
  <!-- prettier-ignore -->
  <input
      v-if="mask" v-maska :data-maska="mask"
      :type="type"
      :class="className + renderIsInvalid"
      :placeholder="placeholder"
      :value="modelValue"
      @input="$emit('update:modelValue', handleInputChange($event))"
      :id="id"
    />
  <input
    v-if="!mask"
    :type="type"
    :class="className + renderIsInvalid"
    :placeholder="placeholder"
    :value="modelValue"
    @input="$emit('update:modelValue', handleInputChange($event))"
    :id="id"
  />
  <span v-for="error in errors" :key="String(error.$uid)">
    <span class="text-danger">{{ error.$message }}</span>
  </span>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { vMaska } from "maska";

export default defineComponent({
  name: "InputField",
  directives: { maska: vMaska },
  setup(props) {
    const handleInputChange = (event: Event) => {
      if (props.type == "checkbox") {
        return (event.target as HTMLInputElement).checked;
      }
      return (event.target as HTMLInputElement).value;
    };
    return {
      handleInputChange,
    };
  },
  props: {
    modelValue: {
      type: [String, Boolean],
    },
    errors: {
      type: Array as PropType<Array<any>>,
      default: () => [],
    },
    type: {
      type: String,
      default: "text",
    },
    className: {
      type: String,
      default: "",
    },
    placeholder: {
      type: String,
      default: "",
    },
    mask: {
      type: String,
      default: "",
    },
    id: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      showNickname: false,
    };
  },
  computed: {
    renderIsInvalid() {
      return this.errors?.length > 0 ? " is-invalid" : "";
    },
  },
});
</script>

<style scoped>
.alias {
  display: flex;
  justify-content: flex-start;
}

.submit {
  display: flex;
  justify-content: flex-end;
}
</style>
