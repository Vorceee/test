<template>
  <div>
    <select v-model="selected" @change="onChange($event)">
      <option disabled value="">Please select one</option>
      <option value="hardcore">Hardcore</option>
      <option value="inspirational">Inspirational</option>
      <option value="national">National</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: "",
    };
  },
  mounted() {
    const storedValue = localStorage.getItem("music");

    //Om det finns en lagrad value i localstorage så sätts den som selected
    if (storedValue) {
      this.selected = storedValue;
    }
  },
  methods: {
    onChange(event) {
      localStorage.setItem("music", event.target.value); //Sparar vald musik i localstorage
    },
  },
};
</script>

<style>
select {
  width: 8em;
  height: 2em;
  font-size: 1em;
  border-radius: 10px;
}
</style>
