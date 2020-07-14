<template>
  <div class="all">
    <h1 class="header" v-if="this.allowDisplay">Your menu is {{ menu }}</h1>
    <h1 class="header" v-else>Your menu is</h1>
    <br />
    <span class="after-text">{{ afterText }}</span>
    <b-table :items="items" :fields="fields" caption-top></b-table>
    <div v-if="showAddMenu">
      <label class="sr-only" for="input-menu">Add Menu</label>
      <b-input
        v-model="menu"
        @keyup.enter="appendMenu()"
        id="input-menu"
        class="mb-2 mr-sm-2 mb-sm-0"
        placeholder="Name of Menu"
      ></b-input>
      <b-button id="menu-button" variant="danger" @click="appendMenu()"
        >Add menu</b-button
      >
    </div>

    <br />
    <br />
    <label class="sr-only" for="input-ingredient">Add Ingredient</label>
    <b-input-group
      v-if="items.length < 10"
      prepend="Ingredient"
      id="pre-ingre"
      class="mb-2 mr-sm-2 mb-sm-0"
    >
      <b-input
        v-model="toBeAdded"
        :disabled="allowIngre == false"
        @keyup.enter="appendIngredient()"
        id="input-ingredient"
        placeholder="Add Ingredient"
      ></b-input>
    </b-input-group>
    <b-button
      v-if="items.length < 10"
      id="ingre-button"
      variant="primary"
      @click="appendIngredient()"
      >Add ingredient</b-button
    >
    {{ resultProduct }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      fields: ["Ingredients"],
      toBeAdded: "",
      items: [],
      menu: "",
      afterText: "",
      allowIngre: false,
      allowDisplay: false,
      showAddMenu: true
    };
  },
  async asyncData({ $axios }) {
    let result = await $axios.post("/api/login", { username: "phang" });
    return {
      result
    };
  },
  methods: {
    appendMenu() {
      if (this.menu) {
        this.showAddMenu = false;
        this.allowDisplay = true;
        this.allowIngre = true;
        this.afterText =
          "Your menu is already added. Now, add menu's ingredients!";
      }
    },
    appendIngredient() {
      this.afterText = "";
      this.items.push({ Ingredients: this.toBeAdded });
      this.toBeAdded = "";
      if (this.items.length == 10) {
        this.afterText = "You can not add more ingredients";
      }
    }
  }
};
</script>

<style>
.all {
  padding: 80px;
  text-align: center;
  justify-content: center;
  align-items: center;
}
.after-text {
  color: crimson;
}
</style>
