<script setup>
import { Icon } from '@iconify/vue';
const props = defineProps({
    user: {
        type: Object,
        required: true,
    },
    index: {
        type: Number,
        required: true,
    },
});

const emit = defineEmits(["delete-user", "update-user-id", 'update-user-name', 'update-user-email']);

const deleteUser = (currentId) => {
    fetch('http://localhost:8080/api/users/' + currentId, { method: 'DELETE' })
        .then(response => emit("delete-user"));
        // 'delete-user' is emit to cause the page to refresh the user list via api get
};

const updateUser = (currentId, currentName, currentEmail) => {
    const requestOptions = {
        method: 'PUT',
        headers: { 'Content-Type': 'application/json'},
        body: JSON.stringify({ id: currentId, name: currentName, email: currentEmail }),
    }
    fetch('http://localhost:8080/api/users/' + currentId, requestOptions)
        .then(response => emit("delete-user"));
        // 'delete-user' is emit to cause the page to refresh the user list via api get
};
</script>
    
<template>
    <li>
        <!-- input boxes for useItems -->
        <div class="user">
            <label for="idInput">id:</label>
            <span>
                <input name="idInput" id="idInput" type="text" :value="user.id" @input="$emit('update-user-id', $event.target.value, index)">
            </span>
            <label for="nameInput">name:</label>
            <span>
                <input id="nameInput" type="text" :value="user.name" @input="$emit('update-user-name', $event.target.value, index)">
            </span>
            <label for="emailInput">email:</label>
            <span>
                <input id="emailInput" type="text" :value="user.email" @input="$emit('update-user-email', $event.target.value, index)">
            </span>
        </div>
        <!-- buttons on right side of userItems -->
        <div class="todo-actions">
            <Icon icon="ph:check-circle" class="icon" color="#41b080" width="22" @click="updateUser(user.id, user.name, user.email)"/>
            <Icon icon="ph:trash" class="icon" color="#f95e5e" width="22" @click="deleteUser(user.id)"/>
        </div>
    </li>
</template>

<style lang="scss" scoped>
    li {
        display: flex;
        align-items: center;
        gap: 10px;
        padding: 16px 10px;
        background-color: #f1f1f1;
        box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
            0 8px 10px -6px rgb(0 0 0 / 0.1);

        &:hover {
            .todo-actions {
                opacity: 1;
            }
        }

        input[type="checkbox"] {
            appearance: none;
            width: 20px;
            height: 20px;
            background-color: #fff;
            border-radius: 50%;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);

            &:checked {
                background-color: #41b080;
            }
        }

        .user {
            flex: 1;
            width: 100%;

            label {
                width: 60px;
                float: left;
            }        

            span {
                display: block;
                overflow: hidden;
            }
            input[type="text"] {
                width: 100%;
                border: 2px solid #41b080;
            }
        }

        .todo-actions {
            display: flex;
            gap: 6px;
            opacity: 0;
            transition: 150ms ease-in-out;

            .icon {
                cursor: pointer;
            }
        }
}
</style>