<template>
  <div class="countries-drop-down" :tabindex="tabindex" @blur="open = false">
    <div class="countries-selected" :class="{open: open}" @click="open = !open">{{ selected }}</div>
    <div class="countries-items" :class="{countries_selectHide: !open}"  :style="{zIndex: 1}">
      <div
        class="countries-item"
        v-for="(option, i) of options"
        :key="i"
        @click="selected=option; open=false;"
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
    },
    countries: Array,
    styles: String,
    selected: String
  },
  data() {
    return {
      open: false
    };
  },
  mounted() {
      this.$emit("input", this.countries);
  },
  methods: {
  }
};
</script>

<style scoped>
.countries-drop-down {
  position: relative;
  width: 100%;
  text-align: left;
  outline: none;
  height: 40px;
  line-height: 40px;
}

.countries-selected {
  background-color: #FFFFFF;
  border-radius: 6px;
  border: 1px solid #858586;
  color: #9E9E9E;
  padding-left: 8px;
  cursor: pointer;
  user-select: none;
}

.countries-selected.open {
  border: 1px solid #9E9E9E;
  border-radius: 6px 6px 0px 0px;
}

.countries-selected:after {
  position: absolute;
  content: "";
  top: 22px;
  right: 10px;
  width: 0;
  height: 0;
  border: 4px solid transparent;
  border-color: #9E9E9E transparent transparent transparent;
}

.countries-items {
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
  max-height: 80px;
  overflow-x: hidden;
}

.countries-item {
  color: #9E9E9E;
  padding-left: 8px;
  cursor: pointer;
  user-select: none;
}

.countries-item:hover {
  background-color: #DFDFDF;
}

.countries_selectHide {
  display: none;
}
</style>