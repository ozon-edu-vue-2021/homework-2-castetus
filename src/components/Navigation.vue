<template>
  <div class="navigation">
    <h3>Keyboard Navigation:</h3>
    <p class="navigation__point"><keyboard-return></keyboard-return> - open/close folder</p>
    <p class="navigation__point"><arrow-up></arrow-up> - previous sibling</p>
    <p class="navigation__point"><arrow-down></arrow-down> - next sibling</p>
    <p class="navigation__point"><arrow-left></arrow-left> - level up</p>
    <p class="navigation__point"><arrow-right></arrow-right> - level down</p>
  </div>
</template>

<script>
import KeyboardReturn from 'vue-material-design-icons/KeyboardReturn.vue';
import ArrowUp from 'vue-material-design-icons/ArrowUp.vue';
import ArrowDown from 'vue-material-design-icons/ArrowDown.vue';
import ArrowLeft from 'vue-material-design-icons/ArrowLeft.vue';
import ArrowRight from 'vue-material-design-icons/ArrowRight.vue';

export default {
  name: 'Navigation',
  components: {
    KeyboardReturn,
    ArrowUp,
    ArrowDown,
    ArrowLeft,
    ArrowRight,
  }
};
</script>

<style lang="scss">
  .navigation{
    &__point{
      display: flex;
      align-items: center;
    }
  }
</style>