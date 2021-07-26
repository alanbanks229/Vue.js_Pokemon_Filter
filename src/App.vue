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

    <h3>Example 3</h3>
    Name: <input v-model="name">
    <div>
      Data:
      {{ champion }}
    </div>
    <button @click="getChampionByName">Get Champion</button>

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
      example1: '',
      champions: [],
      name: 'Ashe',
      champion: {},
      updatedChampion: {},
      attack: 5.5
    }
  },
  methods:
  {
    async getLanguage(){
      try{
        const res = await axios.post('http://localhost:4000/graphql', {
          query: `
            {
              language
            }
          `
        })
        this.example1 = res.data.data.language
      } catch (e) {
        console.log('err', e)
      }
    },
    async getChampions(){
      try{
        const response = await axios.post('http://localhost:4000/graphql', {
            query:`
              {
                getChampions {
                  name
                }
              }
            `
          }
        )
        // console.log(response.data)
        this.champions = response.data.data
      } catch (e) {
        console.log("Welp + ", e)
      }
    },
    async getChampionByName () {
      const res = await axios.post('http://localhost:4000/graphql', {
        query: ` 
        query GetChampionByName($championName: String!) {
          getChampionByName(name: $championName) { 
            name
            attackDamage
          }  
        }`,
        variables: {
          championName: this.name
        }
      })
      this.champion = res.data.data.getChampionByName
    },
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
