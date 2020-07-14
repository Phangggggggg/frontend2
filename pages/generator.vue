<template>
  <b-container class="my-3" fluid="md">
    <h1 class="header">Insert your ingredients here!</h1>
    <h4 id="repeated-text">{{ this.repeatedText }}</h4>
    <h4 id="after-text" v-if="this.items.length == 5">You can add no more ingredients.</h4>
    <b-table striped hover :items="items" :fields="fields" style="center"></b-table>
    <div v-if="allowDisplay" id="ingredients-form" inline>
      <label class="sr-only" for="ingredients">Ingredients</label>
      <b-input
        v-model="toBeAdded"
        id="ingredients"
        class="mb-2 mr-sm-2 mb-sm-0"
        @keyup.enter="appendIngredients()"
        placeholder="Ingredients"
      ></b-input>
      <b-button variant="primary" @click="appendIngredients()">Add</b-button>
    </div>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      fields: ["Ingredients"],
      items: [],
      repeatedText: "",
      toBeAdded: "",
      allowDisplay: true
    };
  },
  methods: {
    appendIngredients() {
      this.items.push({ Ingredients: this.toBeAdded });
      this.toBeAdded = "";
      if (this.items.length == 5) {
        this.allowDisplay = false;
      }
    }
  }
};
</script>
<style scoped>
.header {
  text-align: center;
  padding: 30px;
}
#after-text {
  text-align: center;
  color: firebrick;
}
</style>
