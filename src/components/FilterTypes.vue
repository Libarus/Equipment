<template>
    <div class="types">
        Тип
        <ul>
            <li
                v-for="type of types"
                :class="{ active : type.selected }"
                @click="select(type.title, !type.selected)">{{ type.title }}</li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "Filtertypes",
        props: {
            types: {
                required: true
            }
        },
        methods: {
            select(type, selected) {
                this.$emit('onSelectType', type, selected);
            }
        }
    }
</script>

<style scoped lang="scss">

    .types {
        padding: 0 20px 16px 20px;
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
