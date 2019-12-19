<template>
    <div class="card">
        <div class="in-card">
            <div class="label-role" :class="colors[card.role.toLowerCase()]">Я {{ card.role }}</div>
            <div>
                <div class="icon">
                    <img :src="'/assets/icons/' + card.type + '.png'">
                    {{card.title}}
                </div>

                <div class="codes">
                    <div class="serial">
                        <div class="label">Серийный номер</div><br>
                        {{ card.serial }}
                    </div>
                    <div class="ehd">
                        <div class="label">Код ЕНС</div><br>
                        {{ card.code_ehd }}
                    </div>
                    <div class="sa">
                        <div class="label">Код СА</div><br>
                        {{ card.code_ca }}
                    </div>
                    <div class="num">
                        <div class="label">Инвентарный номер</div><br>
                        {{ card.inventory_num }}
                    </div>
                </div>

                <div class="codes codes-no-border">
                    <div class="activity">
                        <div class="label">Последняя активность</div><br>
                        {{ card.last_activity | convertDate  }}
                    </div>
                    <div class="user">
                        <div class="label">Устройство у сотрудника</div><br>
                        {{ card.owner_fio }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "EquipCard",
        props: {
            card: {
                required: true
            }
        },
        data() {
            return {
                colors : {
                    "пользователь": "class-red",
                    "владелец": "class-green"
                }
            }
        },
        filters: {
            convertDate(value) {
                let date = value.split('/');
                let dt = new Date(date[2], date[0], date[1]);

                let d = dt.getDate();
                if (d < 10) {
                    d = '0' + d;
                }

                let m = dt.getDate();
                if (m < 10) {
                    m = '0' + m;
                }

                return d + '.' + m + '.' + dt.getFullYear();
            }
        }
    }
</script>

<style scoped lang="scss">

    .card {

        width: 50%;
        display: -webkit-inline-flex;
        display: inline-flex;
        padding: 0 0 24px 24px;

        .in-card {

            width: 100%;
            border-radius: 7px;
            background-color: white;
            padding: 16px 24px 0 24px;

            .label-role {
                display: inline-block;
                background-color: silver;
                border-radius: 13px;
                font-size: 11px;
                padding: 5px 10px;
                color: white;
                min-width: 10px;
            }

            .class-red {
                background-color: red;
            }

            .class-green {
                background-color: green;
            }

            .icon {

                padding-top: 16px;
                font-size: 16px;
                font-weight: bold;

                * {
                    display: inline-block;
                    vertical-align: middle;
                }

            }

            .codes {

                padding: 16px 0;
                border-bottom: 1px solid silver;
                font-size: 14px;

                * {
                    display: inline-block;
                }

                .label {
                    font-size: 11px;
                    color: silver;
                }

                .serial {
                    width: 29%;
                }

                .ehd {
                    width: 29%;
                }

                .sa {
                    width: 15%;
                }

                .num {
                    width: 27%;
                }

                .activity {
                    width: 58%;
                }

                .user {
                    width: 42%;
                    color: #1f88df;
                }
            }

            .codes-no-border {
                border: 0;
            }
        }
    }

</style>
