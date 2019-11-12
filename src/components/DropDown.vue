<template>
  <div class="drop-down" :tabindex="tabindex" @blur="open = false">
    <div class="selected" :class="{open: open}" @click="open = !open">{{ selected }}</div>
    <div class="items" :class="{selectHide: !open}">
      <div
        class="item"
        v-for="(option, i) of options"
        :key="i"
        @click="selected=option; open=false; $emit('input', updateData(option))"
      >{{ option }}</div>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    options: {
      type: Array,
      required: true
    },
    tabindex: {
      type: Number,
      required: false,
      default: 0
    }
  },
  data() {
    return {
      selected: this.options.length > 0 ? this.options[0] : null,
      open: false
    };
  },
  mounted() {
      this.$emit("input", this.$parent.bookies);
  },
  methods: {
    updateData: function(option) {
     var selection = require('./../assets/bookies.json');
     if (option=== "Show Active") {
      selection = selection.filter(e =>   e.active === 1);
     } else if (option === "Show Inactive") {
      selection = selection.filter(e =>   e.active === 0);
     } else if (option === "- Show All -"){
       return selection
     } else {
      selection = selection.filter(e => e.name === option);
     }

     return selection;
    }
  }
};
</script>

<style scoped>
.drop-down {
  position: relative;
  width: 100%;
  text-align: left;
  outline: none;
  height: 40px;
  line-height: 40px;
  margin: 10px;
  z-index: 9999;
}

.selected {
  background-color: #FFFFFF;
  border-radius: 6px;
  border: 1px solid #858586;
  color: #9E9E9E;
  padding-left: 8px;
  cursor: pointer;
  user-select: none;
}

.selected.open {
  border: 1px solid #9E9E9E;
  border-radius: 6px 6px 0px 0px;
}

.selected:after {
  position: absolute;
  content: "";
  top: 22px;
  right: 10px;
  width: 0;
  height: 0;
  border: 4px solid transparent;
  border-color: #9E9E9E transparent transparent transparent;
}

.items {
  color: #9E9E9E;
  border-radius: 0px 0px 6px 6px;
  border-right: 1px solid #9E9E9E;
  border-left: 1px solid #9E9E9E;
  border-bottom: 1px solid #9E9E9E;
  position: absolute;
  background-color: #FFFFFF;
  left: 0;
  right: 0;
  height: auto;
  max-height: 200px;
  overflow-x: hidden;
}

.item {
  color: #9E9E9E;
  padding-left: 8px;
  cursor: pointer;
  user-select: none;
}

.item:hover {
  background-color: #DFDFDF;
}

.selectHide {
  display: none;
}
</style>