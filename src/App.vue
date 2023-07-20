<template>
    <div class = "section">
      <div class="box">
        <HelloWorld msg="What do you need right now?" />

          <div class = "block">
          </div>

          <div class = "block">
            <StateItem @clicked="this.onStateClick" v-for="(value, index) in states" :key="index" :data = "value">
            </StateItem>
          </div>
      </div>
    </div>

  <div class = "section">
    <div v-if = "this.activity" class = "box">
      <ActivityItem :activity= "this.activity"/>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import StateItem from './components/StateItem.vue'
import ActivityItem from './components/ActivityItem.vue'
import axios from 'axios'

var gsheet_url = "https://docs.google.com/spreadsheets/d/e/2PACX-1vSmSwTK5PpmSQ_ymKXcATQsACEfhQajL7IfRvqhwrdJUTK01K_ofC-sfBmm0bMxaDuGl8fSY5XRm7nQ/pub?gid=0&single=true&output=tsv"

export default{
  data(){
        return{
          states: null,
          state: null,
          activities: null,
          activity: {}
    }
  },
  components:{
    HelloWorld,
    StateItem,
    ActivityItem
  },
  methods:{
      getStates(){
        let state_list = this.activities.map(activity => activity.state).flat();
        return state_list.filter((value, index, self)=>{
          return self.indexOf(value) === index;
        });
      },
      onStateClick(value){
        this.state = value;
        this.activity = this.getActivity();
      },
      getActivity(){
        let stateActivities = this.activities.filter(item => item.state==this.state)
        return stateActivities[Math.floor(Math.random() * stateActivities.length)];
      }
    },
    mounted(){
      axios
      .get(gsheet_url)
      .then(response =>{
        let data = response.data.split("\r\n");
        let titles = data.shift().split("\t").map(item => item.toLowerCase());
        this.activities = data.map(item => {
          let activity_data = item.split("\t");
          let object = {};
          activity_data.forEach((item, i) => {
              object[titles[i]] = item;
          });
          return object;
        });
        this.states = this.getStates();
      })
    }
  }
</script>
