<template>
  <div id="app" >
    <Button class="save" @click="saveFile"> Save </Button>
    <div class="menu">
    <DropDown :options="['- Show All -', 'Show Active', 'Show Inactive'].concat(require('./assets/bookies.json').map(b => b.name))" v-model="bookies"/>
    <Button class="checkAll" @click="toggleSelect">
      <svg id="checked" xmlns="http://www.w3.org/2000/svg" width="19.95" height="13.82" viewBox="0 0 19.95 13.82">
        <path  d="M18.91,62.507,7.171,74.246l-6.13-6.13L0,69.156l7.171,7.171,12.78-12.78Z" transform="translate(0 -62.507)" fill="#fff"/>
      </svg>
      Check All
    </Button>
    <Button class="removeAll" @click="toggleUnselect"> 
      <svg id="unchecked" xmlns="http://www.w3.org/2000/svg" width="17.053" height="17.053" viewBox="0 0 17.053 17.053">
        <path  d="M17.053,1.055,16,0,8.526,7.472,1.055,0,0,1.055,7.472,8.526,0,16l1.055,1.055L8.526,9.581,16,17.053,17.053,16,9.581,8.526Z" fill="#fff"/>
      </svg>
      Remove All
    </Button>
    </div>
    <TableItem v-bind:bookies="bookies"/>
  </div>
</template>

<script>
import TableItem from './components/TableItem.vue'
import Button from './components/Button.vue'
import DropDown from './components/DropDown.vue'

export default {
  name: 'app',
  data() {
    return {
        bookies: require('./assets/bookies.json'),
        filter: ''
      };
  },
  components: {
    Button,
    TableItem,
    DropDown
  },
  computed: {
    filteredData: function() {
      return this.bookies.filter(el =>  el.name.toLowerCase()
      .match(this.filter.toLowerCase()))
    }
  },
    methods: {
    toggleSelect: function() {
      this.bookies.forEach(function(bookie) {
        bookie.active = 1;
      });
    },
    toggleUnselect: function() {
      this.bookies.forEach(function(bookie) {
        bookie.active = 0;
      });
    },
      saveFile: function() {
        const data = JSON.stringify(this.bookies)
        const blob = new Blob([data], {type: 'text/plain'})
        const event = document.createEvent('MouseEvents'),
        anchor = document.createElement('a');

        for(var bookie in this.bookies) {
          for(var link in this.bookies[bookie].links) {
            this.bookies[bookie].links[link] = document.getElementsByClassName("linkInput")[bookie].value
          }
        }

        anchor.download = "bookies.json";
        anchor.href = window.URL.createObjectURL(blob);
        anchor.dataset.downloadurl = ['text/json', anchor.download, anchor.href].join(':');
        event.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
        anchor.dispatchEvent(event);
    }
  }
}
</script>

<style>
#app {
  font-family: Roboto;
    background-color: #F1F3F9;

}
.menu {
  display: flex;
  justify-content: space-between;
}
#app > ul > li {
  list-style-type: none;
}
tr {
  transform: none !important;
}
.row {
  margin: 10px;
}
</style>
