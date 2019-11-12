
<template >
    <button class="normal" :class="type" :disabled="disabled" @click="callback($event)" >
        <slot></slot>
    </button>
</template>
<script>
export default {
  name: "Button",
  props: {
    type: String,
    disabled: Boolean
  },
  methods: {
    callback: function(e) {
      this.$emit('click', e);
    }
  }
}
</script>
<style>
button {
  outline: none;
  padding: 10px 20px;
  border: 1px solid #ddd;
  color: #333;
  background-color:#fff;
  border-radius: 4px;
  font-size: 14px;
  font-family: '微软雅黑',arail;
  cursor: pointer;
}

button.checkAll {
    background-color: #023955;
    color: #fff;
    width: 150px;
    height: 40px;
    margin-top: 12px;
    margin-bottom: 8px;
    margin-right: 5px;
    float: left;
  }
button.save {
    background-color: #017AAF;
    color: #fff;
    width: 150px;
    height: 40px;
    margin: 10px;
}

button.removeAll {
    background-color: #ff4949;
    color: #fff;
    width: 150px;
    height: 40px;
    float: left;
    margin-top: 12px;
    margin-bottom: 8px;
    margin-right: 10px;
}

button.delete {
    background-color: #ff4949;
    color: #fff;
    height: 44px;

}
#checked {
  width: 15px;
  height: 15px;
  margin-left: -30px;
}

#unchecked {
  width: 15px;
  height: 15px;
  margin-left: -15px;
}
button.add {
    background-color: #13ce66;
    color: #fff;
    height: 44px;
}
</style>