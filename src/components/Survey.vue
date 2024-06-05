<template>
    <h1 class="header1">Опросник ФоЦи</h1>
    <div class="form">
        <ul class="list">
            <li v-for="(item, index) in questions" :class="{ item: true, checked: item.checked }" @click="onItemClick(item)">
                <div class="item__index">
                    {{ index + 1 }}
                </div>
                <div class="item__text">
                    {{ item.text }}
                </div>
                <div class="item__check">{{ item.checked ? "X" : "O" }}</div>
            </li>
        </ul>
        <div class="drivers">
            <table class="drivers__table">
                <tr>
                    <th v-for="(, index) in drivers">D{{ index + 1 }}</th>
                </tr>
                <tr>
                    <td v-for="value in drivers">{{ value }}</td>
                </tr>
            </table>
            <table class="maxDdrivers__table">
                <tr v-for="(maxDriver, index) in maxDrivers">
                    <th >max{{ index+1 }}:</th>
                    <td >D{{ maxDriver.drNumber }}=</td>
                    <td >{{ maxDriver.drValue }}</td>
                </tr>
                <!-- <tr>
                    <td>{{ maxDriver.drValue }}</td>
                </tr> -->
            </table>
        </div>
    </div>
</template>

<script lang="ts">
type questionType = {
    num: number;
    text: string;
    checked: boolean;
    drivers: number[];
};
export default {
    data() {
        return {
            questions: [
                { num: 1, text: "Потливость без видимых причин", checked: false, drivers: [4, 5, 6] },
                { num: 2, text: "Быстрая утомляемость, сонливость, лень", checked: false, drivers: [6, 8, 9] },
                { num: 3, text: "Частые простудные заболевания, длительное течение", checked: false, drivers: [5, 6, 7, 8] },
                { num: 4, text: "Расстройство функции сна, бессонница, кошмары", checked: false, drivers: [1, 6, 7, 9] },
                { num: 5, text: "Одышка после небольшой физической нагрузки", checked: false, drivers: [2, 5, 6, 9] },
                { num: 6, text: "Сердцебиение, учащение ритма сердца, перебои", checked: false, drivers: [3, 7] },
                { num: 7, text: "Склонность к запорам, появление козьего кала", checked: false, drivers: [1, 2, 4, 7, 8] },
                { num: 8, text: "Склонность к жидкому или кашицеобразному калу", checked: false, drivers: [5, 8, 9] },
                { num: 9, text: "Непереносимость холода, плохое самочувствие", checked: false, drivers: [2, 5, 8] },
                { num: 10, text: "Непереносимость жара, плохое самочувствие", checked: false, drivers: [2, 3, 4] },
            ],
            drivers: [0, 0, 0, 0, 0, 0, 0, 0, 0],
            maxDrivers: [
                { drNumber: 1, drValue: 0 },
                { drNumber: 2, drValue: 0 },
                { drNumber: 3, drValue: 0 },
            ],
        };
    },
    methods: {
        onItemClick(item: questionType) {
            // this.questions[index].checked = !this.questions[index].checked;

            // this.questions.forEach((item) => {
            //     if (item.checked) {
            //         item.drivers.forEach((drNum) => {

            //             this.drivers[drNum - 1] = this.drivers[drNum - 1] + 1;
            //         });
            //     }
            // });

            item.drivers.forEach((dr) => {
                item.checked ? this.drivers[dr - 1]-- : this.drivers[dr - 1]++;
            });
            item.checked = !item.checked;

            // console.log(drives);
        },
    },

    // mounted(){

    // }

    // computed: {
    //     drivers() {
    //         return {};
    //     },
    // },
    watch: {
        drivers: {
            handler() {
                let maxDriver1 = 0;
                let maxIndex1 = 0;
                let maxDriver2 = 0;
                let maxIndex2 = 0;
                let maxDriver3 = 0;
                let maxIndex3 = 0;

                this.drivers.forEach((driver, index) => {
                    if (driver >= maxDriver1) {
                        maxDriver1 = driver;
                        maxIndex1 = index;
                    }
                });
                this.drivers.forEach((driver, index) => {
                    if (maxIndex1 != index && driver >= maxDriver2) {
                        maxDriver2 = driver;
                        maxIndex2 = index;
                    }
                });
                this.drivers.forEach((driver, index) => {
                    if (maxIndex2 != index && maxIndex1 != index && driver >= maxDriver3) {
                        maxDriver3 = driver;
                        maxIndex3 = index;
                    }
                });

                this.maxDrivers = [
                    { drNumber: maxIndex1 + 1, drValue: maxDriver1 },
                    { drNumber: maxIndex2 + 1, drValue: maxDriver2 },
                    { drNumber: maxIndex3 + 1, drValue: maxDriver3 },
                ];
            },
            deep: true,
        },
    },
};
</script>

<style lang="scss" scoped>
.header1 {
    border: 2px solid coral;
    border-radius: 8px;
    font-size: 30px;
    font-weight: bold;
    color: brown;
    background: #a1c7643a;
}
.form {
    background: #dda56554;
    width: 500px;
    margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 5px;

    .list {
        list-style: none;
        display: flex;
        flex-direction: column;
        gap: 6px;
        margin: 0;
        padding: 5px;
        .item {
            display: flex;
            // width: 100%;
            gap: 5px;
            cursor: pointer;
            background: #ffffff;
            transition: 0.2s;
            // outline: 2px solid transparent;
            // outline-offset: -1px;

            &:hover{               
                // outline-color: #0ba82d9a;
                background: #efffc3;
            }

            &__index {
                flex: 0 0 auto;
                // border: 1px solid gray;
                padding: 2px;
                background: #0000002a;
                width: 18px;
            }
            &__text {
                flex: 1 1 auto;
                // border: 1px solid gray;
                text-align: left;
                padding: 2px;
            }
            &__check {
                flex: 0 0 auto;
                border: 1px solid rgb(138, 138, 138);
                padding: 2px;
                width: 16px;
                color: rgb(134, 134, 134);
            }

            &.checked {
                background: #1aff4c56;
                .item__check {
                    font-weight: 600;
                    color: rgb(0, 0, 0);
                }
            }
        }
    }
    .drivers {
        background: #ffffff;
        &__table {
            border: 1px solid rgb(56, 105, 44);
            border-radius: 8px;
            padding: 6px;

            th,
            td {
                border: 1px solid black;
                font-weight: 600;
                padding: 3px;
            }

            td {
                background: #fdff879c;
                color: rgb(23, 80, 155);
                font-weight: 600;
            }
        }
    }
}
</style>
