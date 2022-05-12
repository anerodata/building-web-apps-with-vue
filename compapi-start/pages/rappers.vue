<template>
  <main>
    <h1>Some rappers throught the Composition Api</h1>
    <ul>
      <li v-for="rapper in rappers" v-bind:key="rapper.name"
        @click="showRapperInfo(rapper)">
        {{ rapper.name }}
      </li>
    </ul>
  </main>
</template>
<script>
// Composition API with reactive Usefull for more than one variable in
// the state
import { defineComponent, reactive, toRefs } from "@vue/composition-api"

export default defineComponent ({
  setup() {
    const state = reactive({
      rappers: [
        { name: "Prodigy", info: "From QB" },
        { name: "E-40", info: "Yup!" },
        { name: "Willie D", info: "Call me the gangsta of love" },
        { name: "Biggie", info: "Is the illest" },
        { name: "West Side Gun", info: "Ayou!" },
      ]})
    function showRapperInfo (rapper) {
      alert(`${rapper.name}: ${rapper.info}`)
    }
    return {
      ...toRefs(state),
      showRapperInfo
    }
  }
})
// Composition API with ref
/* import { defineComponent, ref } from "@vue/composition-api"

export default defineComponent ({
  setup() {
    const rappers = ref([
      { name: "Prodigy", info: "From QB" },
      { name: "E-40", info: "Yup!" },
      { name: "Willie D", info: "Call me the gangsta of love" },
      { name: "Biggie", info: "Is the illest" },
      { name: "West Side Gun", info: "Ayou!" },
    ])
    function showRapperInfo (rapper) {
      alert(`${rapper.name}: ${rapper.info}`)
    }
    return {
      rappers,
      showRapperInfo
    }
  }
  })
*/
// Options API
/*
export default {
  data() {
    return {
      rappers: [
        { name: "Prodigy", info: "From QB" },
        { name: "E-40", info: "Yup!" },
        { name: "Willie D", info: "Call me the gangsta of love" },
        { name: "Biggie", info: "Is the illest" },
        { name: "West Side Gun", info: "Ayou!" },
      ]
    }
  },
  methods: {
    showRapperInfo (rapper) {
      alert(`${rapper.name}: ${rapper.info}`)
    }
  }
}
*/
</script>
<style>
li {
  cursor: pointer;
  list-style-type: none;
}
li:hover {
  background-color: #f1f1f1;
}

</style>
