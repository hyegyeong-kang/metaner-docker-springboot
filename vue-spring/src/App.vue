<template>
  <div>
    <div>안녕</div>
    <div :value="member.id" :key="member.id" v-for="member in members">
                <li>
                    <div>{{member.name}}</div>
                </li>
    </div>
  </div>

</template>

<script>
import {ref} from 'vue'; 
import axios from 'axios';

export default {
  setup(){
    axios.defaults.baseURL = 'http://localhost:8000';
    axios.defaults.headers.post['Content-Type'] ='application/json;charset=utf-8';
    axios.defaults.headers.post['Access-Control-Allow-Origin'] = '*';

    const members = ref([]);

    const getMemberList = async() => {
      await axios.get('/members', {
            })
            .then((response) => {
              console.log(JSON.stringify(response, null, 2));
              members.value = {...response.data}
            })
            .catch((error) => {
                console.log(error);
            });
    }
    getMemberList();
    


    return {
      members,
      getMemberList,
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
