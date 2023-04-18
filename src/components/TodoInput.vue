<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="addContainer" v-on:click="addTodo">
      <i class="fa-solid fa-check addBtn"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고
        <span @click="showModal = false">
          <i class="fa-solid fa-circle-xmark closeModalBtn"></i>
        </span>
      </h3>
      <span slot="body">바디: 입력하세요.</span>
      <span slot="footer">푸터 : 입력하세요.</span>
    </Modal>
  </div>
</template>

<script>
import Modal from "./common/Modal.vue";

export default {
  data: function() {
    return {
      newTodoItem: "",
      showModal: false
    };
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== "") {
        this.$emit("addTodoItem", this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function() {
      this.newTodoItem = "";
    }
  },
  components: {
    Modal: Modal
  }
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  display: flex;
  align-items: center;
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  height: 100%;
  width: calc(100% - 3rem);
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  height: 100%;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
}
</style>
