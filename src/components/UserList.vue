<script setup>
import UserItem from './UserItem.vue';

const props = defineProps({
    users: {
        type: Object,
        required: true,
    },
});

const emit = defineEmits(["delete-user", "update-user-id", 'update-user-name', 'update-user-email']);

</script>

<template>
    <div>
        <div class="card text-center m-3">
            <h2 class="card-header">Current User List</h2>
            <br />
        </div>
        <ul class="user-list" v-if="users.length > 0">
            <UserItem
                v-for="(user, index) in users" 
                :user="user"
                :index="index" 
                @delete-user="$emit('delete-user')"
                @update-user-id="(value, index) => $emit('update-user-id', value, index)"
                @update-user-name="(value, index) => $emit('update-user-name', value, index)"
                @update-user-email="(value, index) => $emit('update-user-email', value, index)"
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

    // .list-legend {
    //     margin-top: 24px;
    //     display: table;
    //     width: 100%;
    //     table-layout: fixed;
    // }
    // .list-legend span {
    //     display: table-cell;
    //     text-align: center;
    // }
    // .list-legend span:first-child {
    //     text-align: left;
    // }
    // .list-legend span:last-child {
    //     text-align: right;
    // }

</style>