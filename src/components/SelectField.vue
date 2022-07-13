<template>
  <v-select class="select style-chooser" 
    :options="options" 
    :label="label" 
    :placeholder="placeholder"
    :required="required"
    :value="value"
    @change="checkValue"
    >
  </v-select>
</template>
<script>
import vSelect from 'vue-select'
import 'vue-select/dist/vue-select.css'

export default {
  name: "SelectField",
  props: {
      options: Array,
      placeholder: String,
      label: String,
      required: Boolean,
      value: String
  },
  components: {
    vSelect
  },
  methods: {
    checkValue(e){
      this.$emit("customCheck", e.target.selected)
    }
  }
};
</script>
<style scoped lang="scss">
 
</style>