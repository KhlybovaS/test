<template>
  <div class="custom_select__content">
    <img alt="user" src="@/assets/images/user.png" class="custom_select_icon"/>
    <select 
        v-model="modelValue" 
        @change="changeOption"
        class="custom_select"
    >
        <option value="" class="custom_select_option" >
            Выбор автора
        </option>
        <option
          v-for="option in options"
          :key="option.value"
          :value="option.value"
          class="custom_select_option"
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
    border: none;
    padding: 16px 16px 16px 0;
    border-top-right-radius: $border-radius;
    border-bottom-right-radius: $border-radius;
    width: 280px;
    color: #888888;
    font-size: 1.2rem;
    font-weight: 600;
    cursor: pointer;
    background-color: white;

    @media(max-width: $breakpoint_tablet) {
      font-size: 1rem;
      width: $content-width;
    }
}

.custom_select_icon {
  background-color: white;
  border-top-left-radius: $border-radius;
  border-bottom-left-radius: $border-radius;
  padding: 16px;

  @media( max-width: $breakpoint_tablet){
    width: 18px;
    height: 18px;
    padding: 18px;
  }
}

.custom_select__content {
  display: flex;
  justify-content: center;
  
  @media( max-width: $breakpoint_tablet){
    margin-bottom: 20px;
  }
}
</style>