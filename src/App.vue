<template>
  <div id="app">
    <input type="text" v-model="search" placeholder="search blogs" />
    <div class="cardContainer">
      <div v-for="(ele, index) in filteredCards" class="card" :class="{'classA': ele.rarity_id === 1, 'classB': ele.rarity_id === 2, 'classC': ele.rarity_id === 3, 'classD': ele.rarity_id === 4}">
        <p id="name" v-on:click="showInfo(index)">Name: {{ele.name}}</p>
        <div class="showDetail" v-if="ele.spells == 2">
          <p>Slug: {{ele.slug}}</p>
          <p>Mana cost: {{ele.mana_cost}}</p>
          <p>Type: {{ele.type_id}}</p>
          <p>Color: {{ele.color_id}}</p>
          <p>Gold Cost: {{ele.gold_cost}}</p>
          <p>Attack: {{ele.attack}}</p>
          <p>Health: {{ele.health}}</p>
          <p>Armor: {{ele.armor}}</p>
          <p>Hero: {{ele.hero_id}}</p>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import data from './test.json'
export default {
  name: 'app',
  data () {
    return {
      cardInfo: [],
      search: ''
    }
  },
  beforeMount(index){
    this.cardInfo = data;
  },
  computed: {
    filteredCards: function(){
      return this.cardInfo.filter((ele) => {
        return ele.name.toLowerCase().match(this.search);
      });
    }
  },
  methods: {
    showInfo(index){
      if(this.filteredCards[index].spells != '2'){
        this.filteredCards[index].spells = '2';
      }else{
        this.filteredCards[index].spells = '1';
      }

    }
  }
}
</script>

<style scoped>
#app{
  text-align: center;
}
.cardContainer{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
p{
  line-height: 8px;
}
#name:hover{
  cursor: pointer;
}
.card{
  color: white;
  background: red;
  width: 200px;
  height: 300px;
  margin: 0 37px 20px 0;
}
.classA{
  background: black;
}
.classB{
  background: grey;
}
.classC{
  background: blue;
}
.classD{
  background: purple;
}
input{
  height: 30px;
  width: 400px;
  margin-bottom: 50px;
}
</style>
