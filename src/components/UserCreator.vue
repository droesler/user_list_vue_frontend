<script setup>

import { reactive } from "vue";
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
    <h2 class="card-header">Create a New User</h2><br />
    <div class="input-wrap">
        <label for="id">id:</label>
        <span><input id="id" type="text" v-model="userState.id"></span>
    </div>
    <br/>
    <div class="input-wrap">
        <label for="name">name:</label>
        <span><input id="name" type="text" v-model="userState.name"></span>
    </div>
    <br/>
    <div class="input-wrap">
        <label for="email">email:</label>
        <span><input id="email" type="text" v-model="userState.email"></span>
    </div>
    <br/>
    <br/>
    <UserCreateButton @click="createUser()"/>
</template>

<style lang="scss" scoped>

.input-wrap {
  display: flex;
  transition: 250ms ease;

  &.input-err {
    border-color: red;
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: 2px solid #41b080;

  }

  label {
    width: 60px;
    float: left;
  }
  
  span {
    display: block;
    overflow: hidden;
  }

}

</style>