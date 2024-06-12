<template>
    <article class="intro">
        <img class="intro__fotoCi" src="/public/images/Zhu_xi.png" />
        <img class="intro__char" src="/public/images/Qi_character.png" />
    </article>
    <h1 class="header1">Опросник Фо Ци</h1>
    <div class="form">
        <ul class="list">
            <li v-for="(item, index) in questions" :class="{ item: true, checked: item.checked }" @click="onItemClick(item)">
                <div class="item__index">
                    {{ index + 1 }}
                </div>
                <div class="item__text">
                    {{ item.text }}
                </div>
                <div class="item__check">{{ item.checked ? "X" : "" }}</div>
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
            <!-- <table class="maxDdrivers">
                <tr v-for="maxDriver in maxDrivers">
                    <td class="maxDdrivers__discr">{{ driversNames[maxDriver.drNumber - 1] }} -</td>
                    <td>
                        <span class="maxDdrivers__val">{{ maxDriver.drValue }}</span>
                    </td>
                </tr>
            </table> -->
            <table class="maxDdrivers maxDdrivers-improoved">
                <tr v-for="maxDriverImpr in maxDriversImpr">
                    <td class="maxDdrivers__discr">
                        <span class="driversItem" v-for="dr in maxDriverImpr.drs">{{ driversNames[dr - 1] }}</span>
                    </td>
                    <td>
                        <span class="maxDdrivers__val">{{ maxDriverImpr.val }}</span>
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script lang="ts">
// const driversNames=[
// "Застой Ци",
// "Застой Крови",
// "Избыток энергии Ян",
// "Скопление Сырости и Жара",
// "Скопление Сырости и Холода",
// "Пустота Ци",
// "Пустота энергии Инь",
// "Пустота энергии Ян",
// "Пустота Крови"
// ];

type questionType = {
    num: number;
    text: string;
    checked: boolean;
    drivers: number[];
};
type maxDriverType = {
    drs: number[];
    val: number;
};
// type maxDriversImprType=maxDriverType[];

export default {
    data() {
        return {
            questions: [
                { num: 1, text: "Потливость без видимых причин", checked: false, drivers: [4, 5, 6] },
                { num: 2, text: "Быстрая утомляемость, сонливость, лень", checked: false, drivers: [6, 8, 9] },
                { num: 3, text: "Частые простудные заболевания, длительное течение", checked: false, drivers: [5, 6, 8] },
                { num: 4, text: "Расстройство функции сна, бессонница, кошмары", checked: false, drivers: [1, 6, 7, 9] },
                { num: 5, text: "Одышка после небольшой физической нагрузки", checked: false, drivers: [2, 5, 6, 9] },
                { num: 6, text: "Сердцебиение, учащение ритма сердца, перебои", checked: false, drivers: [3, 7] },
                { num: 7, text: "Склонность к запорам, появление козьего кала", checked: false, drivers: [1, 2, 4, 7, 8] },
                { num: 8, text: "Склонность к жидкому или кашицеобразному калу", checked: false, drivers: [5, 8, 9] },
                { num: 9, text: "Непереносимость холода, плохое самочувствие", checked: false, drivers: [2, 5, 8] },
                { num: 10, text: "Непереносимость жара, плохое самочувствие", checked: false, drivers: [2, 3, 4] },
                { num: 11, text: "Отрыжка воздухом, пищей, изжога, икота", checked: false, drivers: [1, 3] },
                { num: 12, text: "Прыщи, угри, гнойничковые болезни кожи, сальная кожа", checked: false, drivers: [4, 9] },
                { num: 13, text: "Жажда, потребность пить много воды", checked: false, drivers: [1, 3, 7] },
                { num: 14, text: "Покашливание, кашель, не связанный с простудой", checked: false, drivers: [5, 6, 7] },
                { num: 15, text: "Неспособность расслабиться, даже после нагрузки", checked: false, drivers: [3, 7] },
                { num: 16, text: "Онемение рук, ног, лица, участков тела", checked: false, drivers: [1, 9] },
                { num: 17, text: "Ощущение кома в горле", checked: false, drivers: [1] },
                { num: 18, text: "Мигрень", checked: false, drivers: [1] },
                { num: 19, text: 'Метеозависимость, ухудшение самочувствия "на погоду"', checked: false, drivers: [1, 2] },
                { num: 20, text: "Стремление к самоизоляции, стремление быть одному", checked: false, drivers: [1, 2, 7] },
                { num: 21, text: "Наличие в семье онкобольных среди родственников", checked: false, drivers: [2] },
                { num: 22, text: "Забывчивость, рассеянность, нарушение концентрации", checked: false, drivers: [2, 3, 6, 9] },
                { num: 23, text: "Частое употребление сладкой пищи", checked: false, drivers: [4, 5, 6] },
                { num: 24, text: "Страх высоты, закрытого пространства, другие фобии", checked: false, drivers: [1, 2] },
                { num: 25, text: "Раздражительность, вспыльчивость, беспокойство", checked: false, drivers: [3, 4, 7] },
                { num: 26, text: "Критицизм, борьба с несправедливостью", checked: false, drivers: [3] },
                { num: 27, text: "Лишний вес", checked: false, drivers: [1, 4, 5, 6, 8] },
                { num: 28, text: "Холодные руки, ноги", checked: false, drivers: [8, 9] },
                { num: 29, text: "Ощущение жара в конечностях, в лице, в теле", checked: false, drivers: [3, 4, 7] },
                { num: 30, text: "Темные круги под глазами, вокруг глаз", checked: false, drivers: [2, 8] },
                { num: 31, text: "Сухость кожи", checked: false, drivers: [2, 6, 7] },
                { num: 32, text: "Выделение светлой мочи", checked: false, drivers: [8] },
                { num: 33, text: "Выделение темной мочи", checked: false, drivers: [3, 4, 5, 7] },
                { num: 34, text: "Угревая сыпь, перхоть, себорея", checked: false, drivers: [2, 3, 4] },
                { num: 35, text: "Сухие, ломкие волосы, ногти", checked: false, drivers: [7, 9] },
                { num: 36, text: "Выпадение волос, облысение", checked: false, drivers: [2, 5, 8, 9] },
                { num: 37, text: "Выделения в уголках глаз", checked: false, drivers: [4] },
                { num: 38, text: "Худоба при обычном питании", checked: false, drivers: [7] },
                { num: 39, text: "Утолщение ног, плотные ноги", checked: false, drivers: [2] },
                { num: 40, text: "Снижение артериального давления", checked: false, drivers: [6] },
                { num: 41, text: "Снижение остроты зрения", checked: false, drivers: [7, 9] },
                { num: 42, text: "Шум в ушах, нарушение слуха", checked: false, drivers: [2, 7] },
                { num: 43, text: "Нарушение памяти на текущие события", checked: false, drivers: [7, 9] },
                { num: 44, text: "Нарушение пигментации кожи (темные, светлые пятна)", checked: false, drivers: [1, 2, 6] },
                { num: 45, text: "Блуждающие боли в теле", checked: false, drivers: [1] },
                { num: 46, text: "Неудовлетворенность вдохом, ощущение нехватки воздуха", checked: false, drivers: [1, 5] },
                { num: 47, text: "Слезотечение на ветру", checked: false, drivers: [1, 4] },
                { num: 48, text: "Тики, судороги, спазмы, заикание", checked: false, drivers: [1, 3] },
                { num: 49, text: "Ощущения жжения при мочеиспускании или опорожнении", checked: false, drivers: [3, 4] },
                { num: 50, text: "Отпечатки зубов на боковых поверхностях языка", checked: false, drivers: [5] },
            ],
            drivers: [0, 0, 0, 0, 0, 0, 0, 0, 0],
            maxDrivers: [
                { drNumber: 1, drValue: 0 },
                { drNumber: 2, drValue: 0 },
                { drNumber: 3, drValue: 0 },
            ],
            maxDriversImpr: [{ drs: [1], val: 0 }],
            driversNames: [
                "Застой Ци",
                "Застой Крови",
                "Избыток энергии Ян",
                "Скопление Сырости и Жара",
                "Скопление Сырости и Холода",
                "Пустота Ци",
                "Пустота энергии Инь",
                "Пустота энергии Ян",
                "Пустота Крови",
            ],
        };
    },
    methods: {
        onItemClick(item: questionType) {
            item.drivers.forEach((dr) => {
                item.checked ? this.drivers[dr - 1]-- : this.drivers[dr - 1]++;
            });
            item.checked = !item.checked;
        },

        calcMaxDrivers() {
            let maxDriver1 = 0;
            let maxIndex1 = 0;
            let maxDriver2 = 0;
            let maxIndex2 = 0;
            let maxDriver3 = 0;
            let maxIndex3 = 0;

            this.drivers.forEach((driver, index) => {
                if (driver > maxDriver1) {
                    maxDriver1 = driver;
                    maxIndex1 = index;
                }
            });
            this.drivers.forEach((driver, index) => {
                if (maxIndex1 != index && driver > maxDriver2) {
                    maxDriver2 = driver;
                    maxIndex2 = index;
                }
            });
            this.drivers.forEach((driver, index) => {
                if (maxIndex2 != index && maxIndex1 != index && driver > maxDriver3) {
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

        calcMaxDriversImpr() {
            // let maxDriver1 = 0;
            // let maxIndex1 = 0;
            // let maxDriver2 = 0;
            // let maxIndex2 = 0;
            // let maxDriver3 = 0;
            // let maxIndex3 = 0;
            let peaksCounter = 0;
            let exceptIndexes: number[] = [];

            let maxDriver: maxDriverType = { drs: [1], val: 0 };
            this.maxDriversImpr = [{ drs: [1], val: 0 }];
            let maxVal = 0;
            let maxIndex = 0;

            this.drivers.forEach((driver, index) => {
                if (driver > maxVal) {
                    maxVal = driver;
                    maxDriver = { drs: [index + 1], val: driver };
                    maxIndex = index;
                }
            });
            exceptIndexes.push(maxIndex);
            peaksCounter++;
            this.drivers.forEach((driver, index) => {
                if (!exceptIndexes.includes(index) && driver == maxVal) {
                    maxDriver.drs.push(index + 1);
                    exceptIndexes.push(index);
                    peaksCounter++;
                }
            });
            this.maxDriversImpr = [{ drs: [...maxDriver.drs], val: maxDriver.val }];

            if (peaksCounter < 4) {
                maxDriver = { drs: [1], val: 0 };
                maxVal = 0;
                this.drivers.forEach((driver, index) => {
                    if (!exceptIndexes.includes(index) && driver > maxVal) {
                        maxVal = driver;
                        maxDriver = { drs: [index + 1], val: driver };
                        maxIndex = index;
                    }
                });
                exceptIndexes.push(maxIndex);
                peaksCounter++;
                this.drivers.forEach((driver, index) => {
                    if (!exceptIndexes.includes(index) && driver == maxVal) {
                        maxDriver.drs.push(index + 1);
                        exceptIndexes.push(index);
                        peaksCounter++;
                    }
                });
                this.maxDriversImpr.push({ drs: [...maxDriver.drs], val: maxDriver.val });
            }

            if (peaksCounter < 4) {
                maxDriver = { drs: [1], val: 0 };
                maxVal = 0;
                this.drivers.forEach((driver, index) => {
                    if (!exceptIndexes.includes(index) && driver > maxVal) {
                        maxVal = driver;
                        maxDriver = { drs: [index + 1], val: driver };
                        maxIndex = index;
                    }
                });
                exceptIndexes.push(maxIndex);
                peaksCounter++;
                this.drivers.forEach((driver, index) => {
                    if (!exceptIndexes.includes(index) && driver == maxVal) {
                        maxDriver.drs.push(index + 1);
                        exceptIndexes.push(index);
                        peaksCounter++;
                    }
                });
                this.maxDriversImpr.push({ drs: [...maxDriver.drs], val: maxDriver.val });
            }

            // this.drivers.forEach((driver, index) => {
            //   if((this.maxDriversImpr.length>=3)||(this.maxDriversImpr.length==2 && peaksCounter>4)){

            //   }

            // if (driver = maxDriver.val) {
            //     maxDriver.drs.push(index+1);

            //     exceptIndexes.push(index);
            //     peaksCounter++;

            // }
            // if (driver > maxDriver.val) {
            //     this.maxDriversImpr.push(maxDriver);
            //     maxDriver={drs:[index+1],val:driver}

            //     exceptIndexes.push(index);
            //     peaksCounter++;
            // }
            // });
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
                this.calcMaxDrivers();
                this.calcMaxDriversImpr();
            },
            deep: true,
        },
    },
};
</script>

<style lang="scss" scoped>
.header1 {
    // border: 2px solid coral;
    // border-radius: 8px;
    font-size: 30px;
    font-weight: bold;
    color: brown;
    text-shadow: 0px 1px 4px white, 0px -1px 4px white, 1px 0px 4px white, -1px 0px 4px white;
    // background: #a1c7643a;
}
.form {
    background: #36363633;
    backdrop-filter: blur(2px);
    // width: 100%;
    // width: calc(100% - 10px);
    // max-width: 600px;
    // margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1.5vh 1.5vw;
    border-radius: 8px;
    // margin: 0;

    .list {
        list-style: none;
        display: flex;
        flex-direction: column;
        gap: 6px;
        margin: 0;
        padding: 0px;
        // width: 100%;
        max-width: 800px;
        .item {
            display: flex;
            // width: 100%;
            // gap: 5px;
            cursor: pointer;
            background: #ffffff;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.548);
            border-radius: 10px;
            border: 1px solid rgb(110, 110, 110);
            overflow: hidden;
            // transition: 0.2s;

            // &:hover{
            //     background: #efffc3;
            // }

            &__index {
                display: flex;
                align-items: center;
                justify-content: center;
                flex: 0 0 auto;
                border-right: 1px solid rgb(138, 138, 138);
                padding: 2px;
                background: #a9d8eb;
                width: 1.5em;
                // font-size: 20px;
            }
            &__text {
                flex: 1 1 auto;
                // border: 1px solid gray;
                text-align: left;
                padding: 8px;
                line-height: 1.3em;
            }
            &__check {
                display: flex;
                align-items: center;
                justify-content: center;
                flex: 0 0 auto;
                border-left: 1px solid rgb(138, 138, 138);
                border-radius: 10px;
                padding: 2px;
                width: 18px;
                // color: rgba(0, 0, 0, 0);
            }

            &.checked {
                background: #d4f8ba;
                // background: #ffe5f9;

                .item__text {
                    // background: #d4f8ba;
                    background-clip: border-box;
                }
                .item__check {
                    font-weight: 600;
                    color: rgb(0, 0, 0);
                    // background: #ffbdf1dc;
                    // background: #d4f8ba;
                }
            }
            // &:hover {
            //     background: #ffdef8;
            // }
        }
    }
    .drivers {
        display: flex;
        flex-direction: column;
        align-items: center;
        // background: #ffffff;
        &__table {
            border: 1px solid rgb(56, 105, 44);
            border-radius: 6px;
            margin-top: 30px;
            padding: 6px;
            background: #ffffff;
            opacity: 0.8;

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

        .maxDdrivers {
            background: #ffffff;
            margin-top: 10px;
            padding: 6px;
            border-radius: 6px;
            font-size: 18px;
            border-collapse: collapse;
            td {
                padding: 6px 4px;
            }
            &__discr {
                text-align: left;
                padding-right: 10px;
            }
            &__val {
                display: inline-block;
                border: 1px solid black;
                width: 1.5em;
                height: 1.5em;
                border-radius: 50%;
            }

            &.maxDdrivers-improoved {
                border-radius: 0;
                .maxDdrivers__val {
                    background: #fff9a7;
                    font-weight: 600;
                }
                td {
                    border: 1px solid rgb(109, 109, 109);
                    border-width: 1px 0;
                }
                .driversItem {
                    display: inline-block;
                    background: #525252;
                    color: rgb(253, 255, 139);
                    margin: 1px 5px 2px 0;
                    padding: 0px 8px 2px;
                    border-radius: 6px;
                }
            }
        }
    }
}
.intro {
    width: 100%;
    max-width: 700px;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    &__fotoCi {
        width: 200px;
    }
    &__char {
        filter: drop-shadow(1px 1px 3px rgb(255, 200, 48));
        // width: 100px;
    }
}
</style>
