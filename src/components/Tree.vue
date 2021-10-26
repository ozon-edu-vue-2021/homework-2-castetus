<template>
  <div class="tree" @keyup.prevent="keyboardHandler" tabindex="0">
    <div class="tree__full-path">Fullpath: {{fullPath}}</div>
    <tree-item
      :root="true"
      :item="treeData">
    </tree-item>
  </div>
</template>

<script>
import TreeItem from './TreeItem.vue';
import treeData from '../../public/static/node_modules.json';
import { eventBus } from '../main';

export default {
  name: 'Tree',
  components: {
    TreeItem,
  },
  data() {
    return {
      treeData: [],
      fullPath: '',
      controlKeys: [
        'Enter',
        'ArrowUp',
        'ArrowDown',
        'ArrowLeft',
        'ArrowRight',
      ],
    };
  },
  created() {
    this.treeData = treeData;
    eventBus.$on('setFullPath', (path) => this.fullPath = path);
  },
  mounted() {
    this.$el.focus();
  },
  methods: {
    keyboardHandler(ev) {
      if (!this.controlKeys.includes(ev.code)) {
        return;
      }
      eventBus.$emit('keyEvent', ev.code);
    },
  },
}
</script>

<style lang="scss">
  .tree{
    outline: none;
    &__item{
      margin: 8px 0;
      width: fit-content;
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
    &__full-path{
      margin-bottom: 20px;
    }
    &__text{
      padding: 5px;
      &_selected{
        border: 1px dotted grey;
        background: rgba($color: grey, $alpha: 0.15);
      }
    }
  }
</style>