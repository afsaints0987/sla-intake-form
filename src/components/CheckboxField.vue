<template>
    <div class="form-check-inline form-group">
        <input class="form-check-input mx-2" type="checkbox" :checked="checked" :id="fieldId" :disabled="disabled" :value="value" @change="checkBox">
        <label class="form-check-label" :for="fieldId">{{label}}</label> 
    </div>
</template>
<script>
export default {
    name: 'CheckboxField',
    props: {
        label: String,
        fieldId: {
            type: String,
            required: true,
        },
        checked: {
            type: Boolean,
        },
        disabled: {
            type: Boolean,
            default: false
        },
        value: String
    },
    methods: {
        checkBox(e){
            this.$emit('checkValue', e.target.value)
        }
    }
}
</script>
<style scoped lang="scss">
    .form-check-label {
        font-size: 12px;
    }
</style>