<template>
  <div class="addItem">
    <input type="text" v-model="item.name" autofocus />
    <font-awesome-icon
      icon="plus-square"
      @click="addItem()"
      :class="[item.name ? 'active' : 'inactive', 'plus']"
    />
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      item: {
        name: "",
      },
    };
  },
  methods: {
    addItem() {
      if (this.item.name == "") {
        return;
      }

      axios
        .post("api/item/store", {
          item: this.item,
        })
        .then((response) => {
          if (response.status == 201) {
            this.item.name = "";
            this.$emit("reloadList");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
.addItem {
  display: flex;
  justify-content: center;
  align-items: center;
}

input {
  background: #f7f7f7;
  border: 0px;
  outline: none;
  margin-right: 10px;
  width: 100%;
  padding: 5px 10px;
  border-radius: 5px;
}

.plus {
  font-size: 20px;
  cursor: pointer;
}

.active {
  /* color: #00ce25; */
  color: #34d399;
}

.inactive {
  color: #999999;
}
</style>