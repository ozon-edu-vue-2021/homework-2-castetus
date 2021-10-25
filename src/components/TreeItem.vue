<template>
  <li
    :class="`tree__item tree__item_${item.type}`"
    @click.stop="select()">
    <span
      class="tree__toggler"
      @click="isOpen = !isOpen"
      v-if="item.contents && item.type === 'directory'">
      [ {{isOpen ? '-' : '+'}} ]
    </span>
    <folder-open-icon/>
    {{item.name}}
    <ul
      v-if="item.contents && item.type === 'directory'"
      v-show="isOpen">
      <tree-item
        v-for="item in item.contents"
        :key="item.name"
        :item="item">
      </tree-item>
    </ul>
  </li>
</template>

<script>
import FolderOpenIcon from 'vue-material-design-icons/FolderOpen.vue';

export default {
  name: 'TreeItem',
  props: {
    item: {
      type: [Object, Array],
      // required: true,
    },
  },
  components: {
    FolderOpenIcon,
  },
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    select() {
      console.log('select');
    },
  },
}
</script>

<style lang="scss">

</style>