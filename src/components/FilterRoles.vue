<template>
    <div class="roles">
        Роль
        <ul>
            <li
                v-for="role of roles"
                :class="{ active : role.selected }"
                @click="select(role.title, !role.selected)">{{ role.title }}</li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "FilterRoles",
        props: {
            roles: {
                required: true
            }
        },
        methods: {
            select(role, selected) {
                this.$emit('onSelectRole', role, selected);
            }
        }
    }
</script>

<style scoped lang="scss">

    .roles {
        padding: 20px 16px;
        color: #374352;
        font-size: 12px;

        ul {
            padding: 0;
            margin: 8px 0 0 0;
            list-style: none;

            li {
                background-color: #e2e5eb;
                border-radius: 7px;
                color: #374352;
                font-size: 12px;
                margin-bottom: 6px;
                padding: 6px 8px;
                cursor: pointer;
            }

            li:hover {
                background-color: #d2d5db;
            }

            li.active {
                background-color: #003057;
                color: white;
            }
        }
    }

</style>
