<template>
  <div class="tree">
    <menu-icon />
    <tree-item
      :item="treeData"></tree-item>
  </div>
</template>

<script>
import TreeItem from './TreeItem.vue';
import treeData from '../../public/static/node_modules.json';
import MenuIcon from 'vue-material-design-icons/Menu.vue';

export default {
  name: 'Tree',
  components: {
    TreeItem,
    MenuIcon,
  },
  data() {
    return {
      treeData: [],
    };
  },
  created() {
    this.treeData = treeData;
  },
}
</script>

<style lang="scss">
  .tree{
    &__item{
      &_directory{
        font-weight: bold;
      }
      &_file{
        font-weight: normal;
      }
      &_link{
        font-weight: normal;
        color: blue;
        text-decoration: underline;
      }
    }
    &__toggler{
      cursor: pointer;
    }
  }
</style>