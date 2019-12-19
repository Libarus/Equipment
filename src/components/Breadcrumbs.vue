<template>
    <div class="bc">
        <ul>
            <li v-for="bc of breadcrumbs">
                <span><a :href="bc.link">{{bc.label}}</a></span>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'Breadcrumbs',
        props: {
            breadcrumbs: {
                required: true
            }
        }
    }
</script>

<style scoped>
    .bc {
        padding-top: 20px;
        font-size: 11px;
        color: gray;
    }

    ul {
        padding: 0;
        margin: 0;
        list-style: none;
    }

    li {
        display: inline-block;
        margin-right: 10px;
    }

    a {
        text-decoration: none;
        color: gray;
    }

    a:hover {
        text-decoration: underline;
    }

    span:after {
        content: '>';
        color: red;
        margin-left: 10px;
    }

</style>
