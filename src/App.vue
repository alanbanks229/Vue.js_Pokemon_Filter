<template>
  <div id="app">
    <!--  -->
    <b>GraphQL Language: Example 1</b>
    <div>
      Data: {{ example1 }}
    </div>
    <br/>
    <b>Champions: Example 2</b>
    <div>
      Data:
      <div v-for="champion in champions" :key=champion.id>
        {{ champion }}
      </div>
    </div>
    <br/>
    <button @click="getChampions">Get Champions</button>
    <button @click="getLanguage">Get Language</button>
    <hr> 
    <!--  -->
    <img alt="Vue logo" src="./assets/logo.png">
    <MainContainer/>
    <buefy-table>
    </buefy-table>
  </div>
</template>

<script>
import axios from 'axios'
import BuefyTable from './components/BuefyTable.vue'
import MainContainer from './components/MainContainer.vue'

export default {
  name: 'App',
  components:
  {
    MainContainer,
    BuefyTable
  },
  data()
  {
    return {
      example1: 'jajaja',
      champions: []
    }
  },
  methods:
  {
    async getLanguage () 
    {
      try
      {
        const res = await axios.post(
          'http://localhost:4000/graphql', {
          query: '{ language }'
        })
        this.example1 = res.data.data.language
      } catch (e) {
        console.log('err', e)
      }
    },
    async getChampions()
    {
      try
      {
        const response = await axios.post(
          'http://localhost:4000/graphql', {
            query: `{
              getChampions {
                name
              }
            }`
          }
        )
        this.champions = response.data.data
      } catch (e) {
        console.log("Welp + ", e)
      }
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
