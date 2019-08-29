<template>
  <div>
    <!-- {{hairColor}}
    <input v-on:click="$emit('toggle-is-blonde-hair')" type="checkbox" id="checkbox" v-model="hairColor">
    <label for="checkbox">hair Color</label>   -->
    <div v-for="color in hairColors">
      <input 
        type="checkbox"
        v-on:click="$emit('select-hair-color', color)" 
      >
      <label>{{color}}</label>
    </div>
  </div>
</template>

<script>
export default {
  props: ['hairColors'],
  methods: {
    toto: () => {
      console.log('before')
      this.togglehairColor()
      console.log('after')
    }
  }
}
</script>

