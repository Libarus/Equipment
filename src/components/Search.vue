<template>
    <div class="search-block">
        <div class="search-bg">
            <span class="lupa"></span>
            <input type="text" placeholder="Поиск" @keyup="startSearch">
        </div>
    </div>
</template>

<script>
    export default {
        name: "Search",
        data() {
            return {
                timerSearch: 0
            }
        },
        methods: {
            startSearch(ev) {
                let word = ev.target.value.trim();
                clearTimeout(this.timerSearch);
                this.timerSearch = setTimeout(() => {
                    this.$emit('onSearch', word);
                },500);
            }
        }
    }
</script>

<style scoped lang="scss">

    .search-block {
        width: 50%;
        padding: 0 0 24px 24px;

        .search-bg {
            background-color: white;
            border: 2px solid #c3c8ce;
            border-radius: 3px;
            padding: 8px;

            * {
                vertical-align: middle;
            }

            input {
                display: inline-block;
                font-size: 12px;
                padding: 5px;
                width: 90%;
                border: 0;
            }

        }

    }

    span{height:20px; width:20px; display:inline-block; position:relative;}
    .lupa:before, .lupa:after{content:''; height:10px; display:block; position:absolute; top:0; left:0; }
    .lupa:before{width:10px; border:3px #c3c8ce solid; border-radius:100%;-webkit-border-radius:100%;-moz-border-radius:100%;}
    .lupa:after{width:3px; background:#c3c8ce; transform:rotate(-45deg);-webkit-transform:rotate(-45deg);-moz-transform:rotate(-45deg);-o-transform:rotate(-45deg);-ms-transform:rotate(-45deg); top:11px; left:14px;}

</style>
