<script setup>
import UserItem from './UserItem.vue';

const props = defineProps({
    users: {
        type: Object,
        required: true,
    },
});

const emit = defineEmits(["delete-user"]);

</script>

<template>
    <div>
        <div class="card text-center m-3">
            <h5 class="card-header">Current User List</h5>
        </div>
        <!-- <ul>
            <li class="user-list" v-for="user in users" :key="user.id">
                {{ user }} {{ user.id }} {{ users.length }}
            </li>
        </ul> -->

        <ul class="user-list" v-if="users.length > 0">
            <UserItem
                v-for="user in users" 
                :user="user" 
                @delete-user="$emit('delete-user')"
            />
        </ul>

    </div>
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