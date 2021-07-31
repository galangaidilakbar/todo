<template>
  <div class="todoListContainer">
    <div class="heading">
      <h2 id="title">Todo List</h2>
      <add-item-form v-on:reloadList="getList()" />
    </div>
    <list-view :items="items" v-on:reloadList="getList()" />
  </div>
</template>

<script>
import addItemForm from "./addItemForm.vue";
import listView from "./listView.vue";

export default {
  components: {
    addItemForm,
    listView,
  },
  data: function () {
    return {
      items: [],
    };
  },
  methods: {
    getList() {
      axios
        .get("api/items")
        .then((response) => {
          this.items = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
    this.getList();
  },
};
</script>

<style scoped>
.todoListContainer {
  font-family: "Nunito";
  width: 500px;
  margin: auto;
}

.heading {
  /* background: #e6e6e6; */
  background: #e5e7eb;
  padding: 10px;
  border-radius: 10px;
  margin-top: 5px;
}

#title {
  font-size: 1.5rem;
  line-height: 2rem;
  text-align: center;
  margin-bottom: 10px;
  color: #6366f1;
}
</style>