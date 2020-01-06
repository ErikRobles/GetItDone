<template>
  <div>
    <form @submit="addTodo">
      <input
        class="text-box"
        type="text"
        v-model="title"
        name="title"
        placeholder="Add an item to Get Done!"
      />
      <input class="btn submit-box" type="submit" value="Add" />
    </form>
  </div>
</template>

<script>
import uuid from "uuid";
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false
      };
      // Send up to parent
      this.$emit("add-todo", newTodo);

      this.title = "";
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}

input [type="text"],
.text-box {
  flex: 10;
  padding: 5px;
}

input [type="submit"],
.submit-box {
  flex: 2;
}
</style>