<template>
  <div>
    <h2>Hair Colors</h2>
    <div v-for="color in hairColors">
      <input 
        type="checkbox"
        v-on:click="$emit('select-hair-color', color)" 
      >
      <label>{{color}}</label>
    </div>
    <h2>Gender</h2>
    <div v-for="gender in genders">
      <input 
        type="checkbox"
        v-on:click="$emit('select-gender', gender)" 
      >
      <label>{{gender}}</label>
    </div>
  </div>
</template>

<script>
export default {
  props: ['hairColors', 'genders']
}
</script>

