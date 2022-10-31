<template>
<div>
    
    <select 
        v-model="modelValue" 
        @change="changeOption"
        class="custom_select"
    >
        
        <option disabled value=""
            style="background-image:url(@/assets/images/user.png);">
            <img alt="user" src="@/assets/images/user.png" />
            Выбор автора
        </option>
        <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
        >
        {{ option.name }}
        </option>
  </select>
</div>
</template>

<script>
export default {
  name: 'custom-select',
  props: {
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>

<style lang="scss" scoped>
.custom_select {
    border: 1px solid white;
    padding: 16px 16px 16px 0;
    border-radius: 10px;
    width: 335px;
    color: #0050EF;
}
</style>