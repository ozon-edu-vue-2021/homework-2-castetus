<template>
  <li
    :class="`tree__item tree__item_${item.type}`">
    <span
      class="tree__toggler"
      @click="toggle()"
      v-if="item.contents && item.type === 'directory'">
      [ {{isOpen ? '-' : '+'}} ]
    </span>
    <span
      class="tree__text"
      @click.stop="select()"
      :class="{tree__text_selected: isSelected}">
      {{item.name}}
    </span>
    <ul
      v-if="item.contents && item.type === 'directory' && isOpen"
      v-show="isOpen">
      <tree-item
        v-for="(el, index) in item.contents"
        :key="index"
        :item="el"
        :path="fullPath">
      </tree-item>
    </ul>
  </li>
</template>

<script>
import { eventBus } from '../main';

export default {
  name: 'TreeItem',
  props: {
    item: {
      type: [Object, Array],
    },
    path: String,
    root: Boolean,
  },
  data() {
    return {
      isOpen: false,
      isSelected: false,
    };
  },
  created() {
    eventBus.$on('setFullPath', this.selectHandler);
    eventBus.$on('keyEvent', this.keyboardHandler);
    eventBus.$on('selectByUid', this.selectByUid);
  },
  mounted() {
    this.root ? this.select() : false;
  },
  computed: {
    fullPath() {
      let path = '';
      if (this.path) {
        path = this.path
      }
      return path + '/' + this.item.name;
    },
  },
  methods: {
    select() {
      this.isSelected = true;
      eventBus.$emit('setFullPath', this.fullPath);
    },
    toggle() {
      this.isOpen = !this.isOpen;
    },
    selectHandler(path) {
      if (path !== this.fullPath) {
        this.isSelected = false;
      }
    },
    keyboardHandler(code) {
      if (!this.isSelected) {
        return;
      } else {
        switch (code) {
          case 'Enter':
            this.toggle();
            break;
          case 'ArrowUp':
            this.keySelection(-1);
            break;
          case 'ArrowDown':
            this.keySelection(1);
            break;
          case 'ArrowLeft':
            this.changeLevel('up');
            break;
          case 'ArrowRight':
            this.changeLevel('down');
            break;
          default:
            break;
        }
      }
    },
    keySelection(direction) {
      const parent = this.$parent;
      const currentIndex = parent.$children.findIndex((item) => item === this);
      const targetElement = parent.$children[currentIndex + direction];
      if (targetElement) {
        this.selectTarget(targetElement);
      }
    },
    changeLevel(direction) {
      let targetElement;
      if (this.item.type === 'directory' && direction === 'down') {
        this.isOpen = true;
        targetElement = this.$children[0];
      } else if (direction === 'up' && this.$parent._props?.item) {
        targetElement = this.$parent;
      } else {
        return;
      }
      if (targetElement) {
        this.selectTarget(targetElement);
      }
    },
    selectByUid(uid) {
      if (uid === this._uid) {
        this.select();
      }
    },
    selectTarget(targetElement) {
      this.isSelected = false;
      this.$nextTick(() => {
        eventBus.$emit('selectByUid', targetElement._uid);
      });
    },
  },
}
</script>

<style lang="scss">

</style>