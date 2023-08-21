<script setup>
import { ref } from "vue";
import UserCreator from "../components/UserCreator.vue";
import UserList from "../components/UserList.vue";

const users = ref([]);

const fetchUserList = () => {
  // GET request using fetch 
  fetch('http://localhost:8080/api/users')
      .then(response => response.json())
      .then(data => users.value = data);
}

fetchUserList();


const updateUserId = (newValue, userIndex) => { 
    users.value[userIndex].id = newValue;
}

const updateUserName = (newValue, userIndex) => {    
    users.value[userIndex].name = newValue;
}

const updateUserEmail = (newValue, userIndex) => { 
    users.value[userIndex].email = newValue;
}

</script>


<template>
  <main>
    <UserCreator @create-user="fetchUserList"/>
    <br/>
    <br/>
    <UserList 
    :users="users" 
    @delete-user="fetchUserList"
    @update-user-id="updateUserId"
    @update-user-name="updateUserName"
    @update-user-email="updateUserEmail"
    />
    <br />
    <button @click="fetchUserList()">Refresh user list</button>
  </main>
</template>


<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }

}
</style>