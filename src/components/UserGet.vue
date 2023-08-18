<script setup>
import { ref } from 'vue';

const users = ref(null);

// GET request using fetch 
fetch('http://localhost:8080/api/users')
    .then(response => response.json())
    .then(data => users.value = data);


</script>


<template>
    <div class="card text-center m-3">
        <h5 class="card-header">Current User List</h5>
        <!-- <div class="card-body"> {{ user.value }} </div> -->
    </div>

    <li class="user-list" v-for="user of users" :key="user.id">
        {{ user }}
    </li>

</template>



<style lang="scss" scoped>

.user-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

</style>