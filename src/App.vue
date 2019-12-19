<template>
    <div id="app">
        <div id="header">
            <div class="wrap">
                <Breadcrumbs :breadcrumbs="breadcrumbs" />
                <h1>Оборудование</h1>
                <div class="badge">{{countItems}}</div>
            </div>
        </div>

        <div id="content-block" class="wrap">

            <div class="sidebar">
                <FilterRoles :roles="roles" @onSelectRole="selectRole"/>
                <FilterTypes :types="types" @onSelectType="selectType" />
            </div>

            <div class="content">
                <div class="alignRight">Отображено {{countShowItem}} из {{countItems}}</div>
                <Search @onSearch="onSearch" />
                <EquipCards :cards="showCards" />
            </div>

        </div>

    </div>
</template>

<script>
    import Breadcrumbs from './components/Breadcrumbs.vue';
    import EquipCards from './components/EquipCards.vue';
    import FilterRoles from "./components/FilterRoles";
    import FilterTypes from "./components/FilterTypes";
    import Search from "./components/Search";

    export default {
        name: 'app',
        data() {
            return {
                countItems: 0,
                countShowItem: 0,
                breadcrumbs: [],
                cards: [],
                showCards: [],
                roles: [],
                types: [],
                searchString: '',

                // helper functions
                processData(data) {
                    this.cards = data;
                    this.showCards = this.cards;
                    this.countItems = data.length;
                    this.countShowItem = data.length;
                    data.map((item) => {
                        let findRole = false;
                        for(let i = 0; i < this.roles.length; i++) {
                            if (this.roles[i].title === item.role) {
                                findRole = true;
                            }
                        }
                        if (!findRole) {
                            let r = { title: item.role, selected: false};
                            this.roles.push(r);
                        }

                        let findType = false;
                        for(let i = 0; i < this.types.length; i++) {
                            if (this.types[i].title === item.type) {
                                findType = true;
                            }
                        }
                        if (!findType) {
                            let r = { title: item.type, selected: false};
                            this.types.push(r);
                        }

                    });
                },

                filterData() {

                    this.showCards = this.cards;

                    // проверяем, есть ли выбранные роли
                    let selectedRoles = [];
                    this.roles.map((item) => {
                        if (item.selected) {
                            selectedRoles.push(item.title);
                        }
                    });
                    if (selectedRoles.length > 0) {
                        // выбрана хотя бы одна роль
                        this.showCards = this.showCards.filter((item) => selectedRoles.indexOf(item.role) !== -1);
                    }

                    // проверяем, есть ли выбранные типы
                    let selectedTypes = [];
                    this.types.map((item) => {
                        if (item.selected) {
                            selectedTypes.push(item.title);
                        }
                    });
                    if (selectedTypes.length > 0) {
                        // выбрана хотя бы один тип
                        this.showCards = this.showCards.filter((item) => selectedTypes.indexOf(item.type) !== -1);
                    }

                    if (this.searchString !== '') {
                        this.showCards = this.showCards.filter((item) =>
                            item.owner_fio.toLowerCase().indexOf(this.searchString.toLowerCase()) !== -1 ||
                            item.title.toLowerCase().indexOf(this.searchString.toLowerCase()) !== -1 ||
                            item.serial.toLowerCase().indexOf(this.searchString.toLowerCase()) !== -1 ||
                            item.code_ehd.toLowerCase().indexOf(this.searchString.toLowerCase()) !== -1 ||
                            item.code_ca.toLowerCase().indexOf(this.searchString.toLowerCase()) !== -1 ||
                            item.inventory_num.toLowerCase().indexOf(this.searchString.toLowerCase()) !== -1
                        );
                    }

                    this.countShowItem = this.showCards.length;
                }
            }
        },
        components: {
            Breadcrumbs,
            EquipCards,
            FilterRoles,
            FilterTypes,
            Search
        },
        mounted() {
            this.breadcrumbs = [
                { label: 'Личный кабинет', link: '/' }
            ];
            fetch('/data/equip.json')
                .then(resp => resp.json())
                .then(json => { this.processData(json); });
        },
        methods: {
            selectRole(role, selected) {
                for(let i = 0; i < this.roles.length; i++) {
                    if (this.roles[i].title === role) {
                        this.roles[i].selected = selected;
                    }
                }
                this.filterData();
            },
            selectType(type, selected) {
                for(let i = 0; i < this.types.length; i++) {
                    if (this.types[i].title === type) {
                        this.types[i].selected = selected;
                    }
                }
                this.filterData();
            },
            onSearch(searchString) {
                this.searchString = searchString;
                this.filterData();
            }
        }
    }

</script>

<style lang="scss">
    $h1color: red;

    .wrap {
        width: 1224px;
        margin: 0 auto;
    }

    #header {
        height: 120px;
        background-color: white;
    }

    h1 {
        margin-top: 10px;
        margin-bottom: 0;
        float: left;
    }

    .badge {
        background-color: #e2e5eb;
        border-radius: 40%;
        font-size: 13px;
        padding: 5px 10px;
        margin: 20px 10px;
        float: left;
        font-weight: bold;
    }

    #content-block {
        margin-top: 24px;
    }

    .sidebar {
        width: 20%;
        background-color: white;
        display: inline-block;
        vertical-align: top;
    }

    .content {
        width: 80%;
        display: inline-block;
        vertical-align: top;
    }

    .alignRight {
        float: right;
        font-size: 12px;
        color: gray;
    }

</style>

