<template>
    <div class="filter">
        <div class="filter__content">
            <CustomSelect
                :options="options"
            />
        </div>
    </div>
</template>

<script>
import CustomSelect from "@/components/CustomSelect.vue";

export default {
  components: {
    'CustomSelect': CustomSelect
  },
  data() {
      return {
          options: [
              {name: "Option 1", value: 1},
              {name: "Option 2", value: 2},
              {name: "Option 3", value: 3},
              {name: "Option 4", value: 4},
              {name: "Option 5", value: 5},
          ]
      }
  }
};
</script>

<style lang="scss" scoped>
.filter {
    background-color: $post-list_background-color;
}

.filter__content {
    height: 132px;
    width: $content-width;
    margin: auto;
    display: flex;
    align-items: center;  
}
</style>