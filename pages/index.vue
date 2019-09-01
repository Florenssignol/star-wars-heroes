<template>
  <div class="container">
      <h1 class="title">
        Star Wars Heroes
      </h1>
    <div>
      <input type="text" v-model="search" placeholder="search heroes">
      <SidebarFilter 
        :hairColors="heroesHairColor"
        v-on:select-hair-color="selectHairColor"
        :genders="heroesGender"
        v-on:select-gender="selectGender"
      />
      <div v-for="hero in filteredHeroes"
        v-bind:key="hero.id"
        v-bind:title="hero.name"> 
          {{hero.name}} - {{hero.gender}}
      </div>
    </div>
  </div>

</template>

<script>
import Logo from '~/components/Logo.vue'
import SidebarFilter from '~/components/SidebarFilter.vue'

export default {
  data() {
    return { 
      heroes: [
		{
			"name": "Luke Skywalker",
			"height": "172",
			"mass": "77",
			"hair_color": "blond",
			"skin_color": "fair",
			"eye_color": "blue",
			"birth_year": "19BBY",
			"gender": "male",
		},
		{
			"name": "C-3PO",
			"height": "167",
			"mass": "75",
			"hair_color": "n/a",
			"skin_color": "gold",
			"eye_color": "yellow",
			"birth_year": "112BBY",
			"gender": "n/a",
		},
		{
			"name": "R2-D2",
			"height": "96",
			"mass": "32",
			"hair_color": "n/a",
			"skin_color": "white, blue",
			"eye_color": "red",
			"birth_year": "33BBY",
			"gender": "n/a",
		},
		{
			"name": "Darth Vader",
			"height": "202",
			"mass": "136",
			"hair_color": "none",
			"skin_color": "white",
			"eye_color": "yellow",
			"birth_year": "41.9BBY",
			"gender": "male",
		},
		{
			"name": "Leia Organa",
			"height": "150",
			"mass": "49",
			"hair_color": "brown",
			"skin_color": "light",
			"eye_color": "brown",
			"birth_year": "19BBY",
			"gender": "female",
		},
		{
			"name": "Owen Lars",
			"height": "178",
			"mass": "120",
			"hair_color": "brown, grey",
			"skin_color": "light",
			"eye_color": "blue",
			"birth_year": "52BBY",
			"gender": "male",
		},
		{
			"name": "Beru Whitesun lars",
			"height": "165",
			"mass": "75",
			"hair_color": "brown",
			"skin_color": "light",
			"eye_color": "blue",
			"birth_year": "47BBY",
			"gender": "female",
		},
		{
			"name": "R5-D4",
			"height": "97",
			"mass": "32",
			"hair_color": "n/a",
			"skin_color": "white, red",
			"eye_color": "red",
			"birth_year": "unknown",
			"gender": "n/a",
		},
		{
			"name": "Biggs Darklighter",
			"height": "183",
			"mass": "84",
			"hair_color": "black",
			"skin_color": "light",
			"eye_color": "brown",
			"birth_year": "24BBY",
			"gender": "male",
		},
		{
			"name": "Obi-Wan Kenobi",
			"height": "182",
			"mass": "77",
			"hair_color": "auburn, white",
			"skin_color": "fair",
			"eye_color": "blue-gray",
			"birth_year": "57BBY",
			"gender": "male",
		}
	], 
      selectedHairColors: [],
      selectedGenders: [],
      search: "",
    }
  },
  computed: {
    heroesHairColor: function() {
      return this.heroes
        .map((hero) =>{
         return hero.hair_color
        })
        .filter((value, index, self) => { 
          return self.indexOf(value) === index;
        })
    },
    heroesGender: function() {
      return this.heroes
        .map((hero) => {
         return hero.gender
        })
        .filter((value, index, self) => {
          return self.indexOf(value) === index;
        })
    },
    filteredHeroes: function() {
      return this.heroes
        .filter((hero) => {
          if (this.selectedHairColors.length === 0) {
            return true
          }
          return this.selectedHairColors.includes(hero.hair_color)
        })
        .filter((hero) => {
          if (this.selectedGenders.length === 0) {
            return true
          }
          return this.selectedGenders.includes(hero.gender)
        })
        .filter((hero) => {
          return hero.name.toLowerCase().match(this.search.toLowerCase());
        });
    }
  },
  methods: {
    selectHairColor: function (color) {
      if (this.selectedHairColors.includes(color)) {
        this.selectedHairColors.splice(this.selectedHairColors.indexOf(color))
      } else {
        this.selectedHairColors.push(color)
      }
    },
    selectGender: function (gender) {
      if (this.selectedGenders.includes(gender)) {
        this.selectedGenders.splice(this.selectedGenders.indexOf(gender))
      } else {
        this.selectedGenders.push(gender)
      }
    },
  },
  components: {
    Logo,
    SidebarFilter
  }
}

</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
