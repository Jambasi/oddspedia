<template>
  <div class="row">
    <div class="col-8">
      <table class="table table-striped">
        <draggable v-model="bookies" tag="tbody">
          <tr v-for="(item, index) in bookies" :key="item.id" class="tableRow">
            <td scope="row">
              <input type="checkbox" class="checkbox" v-model="item.active" @change="changeActiveStatus" />
              <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 30 30">
                <g id="Path_2025" data-name="Path 2025" fill="#fcfcfc">
                  <path d="M 29.4428768157959 29.5 L 0.5571239590644836 29.5 C 0.5270711779594421 29.21383666992188 0.5 28.73642921447754 0.5 28.125 L 0.5 1.875 C 0.5 1.263570070266724 0.5270711779594421 0.7861641049385071 0.5571239590644836 0.5 L 29.4428768157959 0.5 C 29.47292900085449 0.7861641049385071 29.5 1.263570070266724 29.5 1.875 L 29.5 28.125 C 29.5 28.73642921447754 29.47292900085449 29.21383666992188 29.4428768157959 29.5 Z" stroke="none"/>
                  
                  <path d="M 1.020805358886719 1 C 1.008657455444336 1.233007431030273 1 1.525447845458984 1 1.875 L 1 28.125 C 1 28.47455215454102 1.008657455444336 28.76699256896973 1.020805358886719 29 L 28.97919464111328 29 C 28.99134254455566 28.76699256896973 29 28.47455215454102 29 28.125 L 29 1.875 C 29 1.525447845458984 28.99134254455566 1.233007431030273 28.97919464111328 1 L 1.020805358886719 1 M 0.1714305877685547 0 L 29.82856941223145 0 C 29.92325019836426 0 30 0.8394699096679688 30 1.875 L 30 28.125 C 30 29.1605396270752 29.92325019836426 30 29.82856941223145 30 L 0.1714305877685547 30 C 0.07674980163574219 30 0 29.1605396270752 0 28.125 L 0 1.875 C 0 0.8394699096679688 0.07674980163574219 0 0.1714305877685547 0 Z" stroke="none" fill="#e4e7f1"/>
                   <path id="checked" d="M18.91,62.507,7.171,74.246l-6.13-6.13L0,69.156l7.171,7.171,12.78-12.78Z" transform="translate(0 -62.507)" fill="#52bc01"/>
                 </g>
              </svg>
            </td>
            <td scope="row">{{ index }}</td>
            <td class="siteInfo">
                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="130" height="45" >
                  <defs>
                    <pattern id="pattern" preserveAspectRatio="none" width="100%" height="100%" viewBox="0 0 200 101">
                       <image width="200" height="101" xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAABlCAMAAAA/BFycAAADAFBMVEVMaXEAeswAeswAeswAeswAeswAeswAeswAL14AeswAeswAeswALVsAL14AbLcAeswAL14AeswAeswAeswAeswAeswAeswAL14AL14AeswAeswAL14AL14AeswAeswAL14AeswAeswAeswAeswAeswAeswAL14AeswAL14AL14AL14AL14AL14AeswAL14AL14AeswAL14AeswAeswAL14AeswAeswAeswAL14AL14AeswAL14AeswAL14AL14AeswAL14AL14AeswAL14AL14AeswAL14AeswAL14AeswAeswAL14AeswAeswAeswAeswAeswAeswAeswAeswAL14AeswAeswAeswAeswAeswAeswAeswAL14AeswAeswAL14AL14AL14AL14AL14AL14AL14AeswAL14AL14AL14AeswAeswAeswAL14AL14AL14AL14AeswALlwAeswAL14AL14AeswAeswAL14AeswAL14AeswAeswAL14AeswAeswAeswAL14AL14AL14AeswAeswAL14AeswAeswAeswAKlcAL14AeswAeswAL14AL14AeswAeswAL14AL14AeswAL14AeswAL14AL14AL14AeswAeswAeswAeswAL14AL14AL14AL14AL14AL14AeswAeswAeswAL14AL14AeswAecsAL14AeswAeswAL14AKVUAL14AL14AeswAeswAL14AeswAeswAeswAL14AL14AL14AeswAeswAL14AeswAeswAeswAeswAeswAeswAL14AL14AL14AL14AL14AL14AeswAeswAeswAeswAL14AL14AL14AeswAL14AeswAL14AeswAeswAL14AL14AeswAL14AL14AL14AL14AfM4Aht4AHkYAfdEAQXgAKFQAHkYAg9oAi+YAfdEAeswAeswAiOEAhNkAHUUAi+QAgNUAJlEAH0gAKVUAL14AIkwAiuQALFoAhNsAL14AeswAecsAMF8AessAhNoAMWAAMGAAL19AvzHnAAAA93RSTlMAFDLsNjP38vNlkfAI9AL99mRmnlxg6UTh+dGz7N506dzVOTQeR9L2xNqqwLFZloYMHtPiDxHIJUESYs1OvXfGbygEN4PuaIt045zjo/zgQZco1xDv9Bg4LjD+5U6gBqHYYkp/A8cbtuf9azuvAd8EMYhb5H4VI4/QUb+UWC4TfE0bTA2nGYeCIp8XWBa2C5BKVDWn5xnMe/n4gHeFy18snFbKRo3DvDq67bHwpNitKqQWvprUutsc+5mTigpVrSogVutx2676ZDxz0BVsee5rgqokwoxFPj2NK68HY17nKQ9wFvTbjzXNSA5dMhk4u45FuFJ6GeGAKj2fewAABlhJREFUeNrtmXd8FEUUxx8h5A4upCcQEwhICxAIAUISEmroPVIMndAhSO9SpCjSQaqgoCBFmiiCoGCJHXvvvffuHqDi7t7ezpuZ251d9M/5/sGHffO7mfdjp7xZQCKRSCQSiUQikUgkEolEIpFIJBKJ5L/RfK7XoEGu4iV0b9V41yykixzjpfj780+/+LDZjMEzBiclbU4qX1bW0dfR5/F4fC2W79jQBI9QyWPHYoCjHhG9xD6W1FeCNIDA3wnet+81fdSlmy5+dg/8dcFvQfk+RWSIan475kGOX8h5oY/d/UhuJbBbYTmcG9DljWAa8j+GLy/YjX1bcIixtikmn4WWYiM7RD4OxKDcsgDuUDiWarotVZlohhr85JLt4N2MMRJsVW0A4sVGSgU+huDcqqqB0ZV5J+rsyhrPxIZrvz4kGH1nYJATtqJpAKeEPvq3t/exmkruXS3UifMxMxLapTKxmzRp1N2i8W9UVaI8C+AB8QtZa++jLZ1dWz3IzqFzAFO9TKyLrqwlHL+6Jqttr1kEC/wOOrJjFJPeQj1ayK2QX9l3tDrw+53C8SdpskTRdtRHbKSCnY/1THppRvwYip0uBDjH+qhiCNc62zSHCnaEqAixETsfw9n8GhgNeSSUupCbf8r4qYZumIcMtDW2ok5sXHW8BTXVdNegrXZiQEeIy4H2sXHBp0S06roiUR0bHxncon4p2JRpbmNLAFozqsmrgrJSlHFL1HPvnmb4PvUxO5rIbgcByURbCRyxR+FoZzamBQJ18wAeZEQN15mq55GRgbjvCCqZAiS7yz4p6mR8zJkR3kd30rhXD8yfAnCGEaWgLnpYbPO9SXyB+jgHJWc3RdjltMaZkaoKv0QIDY2cUxhNY9zFZjJoPAoP6GqGo7XS8TyRJYmyaob3CWfU54xsQ63tFOU4wHWt+GOQUIT+9eaEVdAICwsv6OyjDm14Dlcj7wR0hKupKjnH73qJwFw9sz2o0noGNx9L0cp72saETlQPE/0iyqJU2UYUiOY1fXGXcVRN7Iwx+lG+awIp2Kew5f1k5n08Tbe/4uwUu15QMWKWk4ae2Q6NaLMmE1BpPo5u58srZRMtKBO9jw26rKaL6rwGt1GLGaet3AMozdZ0e2GMwnEnFhQLfESE67JyIZqstrEBg0hDH6dGDipn6EOikGquooQgBs++xwVGoveN1WRv2KsG4EEX8CesmPHp6h/5JMl+o3HrdCUk65FkknCJNNMOlxW2khqoQ7p4rO3UiDZNZtEXPkKJYsEqvOULaaTK9tkqhprdMUXZKXDDEIslMlOxYr6peVQbTlzEN0m2VVREo1L3qxNsro7vI3tJuINizRBNwF4y4gaGBRhYuhFPj6sAvsZp14tgqJeD00mgXqYb0MG9fRkq721IDapWovyoTkuTcRE/DSWXsKgcwyLql92oO7ILItEOm25GNym2PGvIepFB99Pd1sRFfAt0xEVZJcJ//aopyt1yi+1gxKIaKgLydN1s9K+3mO62I6nA4BtUlLQQpDP7Cgotfi1UCX4VVUQ8qQtj0ahvgsVMv4G6i3QWpNMIaRNdGUkn2d0aqUe2sDXx63V5J7s15REy6GB6iaAL+Fl4CCVXLEinM9IWufGx7Cl2W301zXgke/JS3ki+Jp2BpkxxeIBa19ap2IPeQk+Sp0EFtcJ5SkltuBVd1129kJEouVHqM//1qkQN3s87mQ7wnR9l6LcgG9p7rNr4EzwbBXu4MpKJcstVn986zSQ8Uv/GzRvxRsIPF/xCJpLPEzz89jQPRWNdGRmHqsH3zBdE0r1FE4X8qv0TwI+XRCmeVH+72LKV3wEqoejNbnxM6UdN+w+YZJ/IMnTrJnBGLn4Pv4teyWtaxbhfaKTAzKcpCVZz6oH7MpoJ7zO5zm1uCrtwRi7/AvCnvZND+he8ekIjY4OjrEHBeFdGtqHLeBZbtmfgU5g/I//5GcBndxd5wfguJKJayFMkwZWRg+j/RRoziR5nDxyWPwC+tX4lDxu14AqhkZVkiVzpKdJcsWYmK+40gl0lvwF8FTq3o9MeIdNeRGKou0j/KDdGcrd7TSrHeBEvdglVl72ckj857bApSl0FH5X3UPiSTrU5Uj2c/GZYL48An3mK9C0j0XiQSCQSiUQikUgkEolEIpFIJBKJRCL5f/gXnITIV7nCCIwAAAAASUVORK5CYII="/>
                    </pattern>
                  </defs>
                  <rect id="_1xbet-2" data-name="1xbet" width="130" height="65"  fill="url(#pattern)"/>
                </svg>
                <p>{{ item.name }}</p>
              </td>
            <td>
                <tr v-for="(link, i) in item.links" :key="link.default" class="countriesMenu" >
                  <div v-if="i === 'default'">
                    Default
                  </div>
                  <div v-else class="countriesWrapper" >
                    <CountriesDropDown :selected="require('./../assets/countries.json').filter(c => c.code === i)[0] ? require('./../assets/countries.json').filter(c => c.code === i)[0].name : require('./../assets/countries.json')[0].name" :options="require('./../assets/countries.json').map(b => b.name)" v-model="countries" />
                  </div>
                </tr>
            </td>
            <td v-if="item.links !== undefined">
                <tr  v-for="(link, linkName) in item.links" :key="link.default" >
                    <input type="text" :value="link" class="linkInput" /> 
                    <div  v-if="linkName === 'default'"> 
                      <Button class="add" v-model="bookies" @click="addLink(bookies, index)" > 
                        <svg xmlns="http://www.w3.org/2000/svg" width="18.001" height="18.001" viewBox="0 0 18.001 18.001">
                            <path id="add_1_" data-name="add (1)" d="M18,8.143H9.858V0H8.143V8.143H0V9.858H8.143V18H9.858V9.858H18Z" fill="#fff"/>
                        </svg>
                      </Button>
                    </div>
                    <div  v-else> 
                      <Button class="delete" v-model="bookies" @click="removeLink(bookies, index, linkName)" > 
                        <svg xmlns="http://www.w3.org/2000/svg" width="17.053" height="17.053" viewBox="0 0 17.053 17.053">
                          <path id="unchecked" d="M17.053,1.055,16,0,8.526,7.472,1.055,0,0,1.055,7.472,8.526,0,16l1.055,1.055L8.526,9.581,16,17.053,17.053,16,9.581,8.526Z" fill="#fff"/>
                        </svg>
                    </Button>
                    </div>
                </tr>
            </td>
            <td v-else>
                    <tr >
                    <input type="text"/> 
                    <div>
                    <Button class="add" v-model="bookies" @click="addLink(bookies, index)" > 
                        <svg xmlns="http://www.w3.org/2000/svg" width="18.001" height="18.001" viewBox="0 0 18.001 18.001">
                            <path id="add_1_" data-name="add (1)" d="M18,8.143H9.858V0H8.143V8.143H0V9.858H8.143V18H9.858V9.858H18Z" fill="#fff"/>
                        </svg>
                    </Button>
                    </div>
                </tr>
            </td>
          </tr>
        </draggable>
      </table>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable"
import Button from "./Button"
import CountriesDropDown from './CountriesDropDown.vue'
import Vue from 'vue';
const EventBus = new Vue();
export default {
  name: "table",
  display: "Table",
  order: 8,
  components: {
    draggable,
    CountriesDropDown,
    Button
  },
  props: ["bookies"],
  data() {
    return {
        dragging: false,
        countries: require('./../assets/countries.json')
    };
  },
  methods: {
    changeActiveStatus: function(e) {
        this.$emit('input', e.target.value)
    },
    addLink: function(bookies, item) {
      if (bookies[item].links) {
        this.$set(bookies[item].links, "tempEntry", " ");
      } else {
         this.$set(bookies[item], "links", {"default": ""});
      }
    },
    getCountry: function(links, countryCode) {
      var countryByCode = this.countries.filter(c => c.code === countryCode);
      return countryByCode.length > 0 ? countryByCode[0].name :"Default";
    },
    removeLink: function(bookies, item, link) {
      Vue.delete(bookies[item].links, link)
    }
  }
};
</script>
<style scoped>

.siteInfo {
  text-align: center;
}
.buttons {
  float: left;
}
td > tr {
    display: flex;
}
.tableRow td{
    border-bottom: 2px solid #D7DAE4;
}
.tableRow > td {
    padding-top: 15px;
    padding-bottom: 15px;
    line-height: 44px;
}
button {
    float: left;
}
.table {
    width: 100%;
    height: 100%;
    background-color: #F1F3F9;
    border-collapse: collapse;
}
input {
    width: 100%;
    float: left;
    background-color: #7b839a;
    border-color: #E4E7F1;
    border-radius: 5px;
}
p{
  margin: 0px;
  line-height: 25px;
}
</style>

<style>
.items {
  max-height: 200px;
}
.countriesWrapper {
  display: contents;
}
.countriesMenu {
  margin-right: 10px;
}
</style>