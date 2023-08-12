<template>
  <div class="container w-100 m-auto text-center mt-3">
      <h1 class="text-danger">Todo List Application</h1>
      <add-item-form v-on:reloadlist="getItems()" />
      <list-view
          :items="items"
          v-on:reloadlist="getItems()"
          class="text-center"
      />
  </div>
</template>

<script>
import axios from "axios";
import AddItemForm from "./components/AddItemForm"
import ListView from "./components/ListView";

export default {
  components: {
      AddItemForm,
      ListView
  },

  data: function() {
      return {
          items: []
      };
  },
  methods: {
      getItems() {
          axios
              .get("http://127.0.0.1:8000/api/items")
              .then(res => {
                  this.items = res.data.items;
              })
              .catch(error => {
                  console.log(error);
              });
      }
  },
  created() {
      this.getItems();
  }
};
</script>

<style scoped></style>
