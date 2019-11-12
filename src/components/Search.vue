<template>
  <div>
    <input placeholder="Search" id="search" :value="query" @input="updateFilter" >
  </div>
</template>


<script>

export default {
    name: "Search",
    props: ['query'],
    data() {
      return {
        bookies: require('./../assets/bookies.json')
      };
    },
    methods: {
        updateFilter: function(event) {
          var filteredData = this.bookies.filter(e => e.name.toLowerCase().match(event.target.value.toLowerCase()));

          this.$emit('update:query', event.target.value);
          this.$emit('input', filteredData);
        }
    }
}
</script>
<style>
  #search {
    background-color: #FFFFFF;
    border-radius: 6px;
    border: 1px solid #858586;
    height: 40px;
    line-height: 40px;
    margin-left: 10px;
    width: auto;
    display: flex;
    color: #9E9E9E;
    padding-left: 8px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
</style>