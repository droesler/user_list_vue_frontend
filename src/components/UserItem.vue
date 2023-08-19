<script setup>
import { Icon } from '@iconify/vue';
const props = defineProps({
    user: {
        type: Object,
        required: true,
    },
});

const emit = defineEmits(["edit-user", "update-user", "delete-user"]);

const deleteUser = (currentId) => {
    fetch('http://localhost:8080/api/users/' + currentId, { method: 'DELETE' })
        .then(response => emit("delete-user"));
};

</script>
    
<template>
    <li>
        <div class="todo">
            <!-- <input v-if="todo.isEditing" type="text" :value="todo.todo" @input="$emit('update-todo', $event.target.value, index)"> -->
            <span>
                 {{ "id: " + user.id + " | name: " + user.name + " | email: " + user.email }} 
            </span>
        </div>
        <div class="todo-actions">
            <!-- <Icon v-if="todo.isEditing" icon="ph:check-circle" class="icon" color="#41b080" width="22" @click="$emit('edit-todo', index)"/>
            <Icon v-else icon="ph:pencil-fill" class="icon" color="#41b080" width="22" @click="$emit('edit-todo', index)"/> -->
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

        .todo {
            flex: 1;


            input[type="text"] {
                width: 100%;
                padding: 2px 6px;
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