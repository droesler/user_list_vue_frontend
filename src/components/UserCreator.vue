<script setup>

import { onMounted, reactive } from "vue";
import UserCreateButton from "../components/UserCreateButton.vue";

const userState = reactive({
    id: "",
    name: "",
    email: "",
});

const emit = defineEmits(["create-user"]);


const createUser = () => {
    if (userState.id !== "" && userState.name !== "" && userState.email != "") {
        
        const requestOptions = {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(userState),
        };

        // console.log(JSON.stringify(userState));

        fetch('http://localhost:8080/api/users', requestOptions)
          .then(response => emit("create-user", response.json()));

        userState.id = "";
        userState.name = "";
        userState.email = "";
        
        return;
    }
    alert('Fields are incomplete. Please fill out every field.')
};




</script>

<template>
    <div class="input-wrap">
        <label for="id">User id:</label>
        <input id="id" type="text" v-model="userState.id">
    </div>
    <br/>
    <div class="input-wrap">
        <label for="name">User name:</label>
        <input id="name" type="text" v-model="userState.name">
    </div>
    <br/>
    <div class="input-wrap">
        <label for="email">User email:</label>
        <input id="email" type="text" v-model="userState.email">
    </div>
    <br/>
    <UserCreateButton @click="createUser()"/>
</template>

<style lang="scss" scoped>

.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-err {
    border-color: red;
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }
}

</style>