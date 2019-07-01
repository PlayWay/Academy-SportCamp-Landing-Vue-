<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.prices#prices
        +e.container.container
            +e.H2.title.title Цена на абонементы #[span спортивного лагеря]
            +e.wrapper--main
                +e.content
                    +e.toggle-bar
                        +e.tabs.tabs__
                            +e.BUTTON.item--prices.button(type="button" :class="{'active': activeTab.index === 0}" @click="toggleTabs(0)" ref="tab0")
                                span Абонемент
                            +e.BUTTON.item--prices.button(type="button" :class="{'active': activeTab.index === 1}" @click="toggleTabs(1)" ref="tab1")
                                span Проживание
                            +e.active(
                                ref="activeTab"
                                :style="{left: activeTab.left + 'px',width: activeTab.width + 'px'}"
                            )
                        +e.info
                            p Абонемент дает вам право посещать спортивный лагерь «Academy» в течении указанного на нем периода.
                    +e.table.table__(:class="{'active': activeTab.index === 0}")
                        +e.head
                            +e.wrapper--head
                                +e.col--1.--head
                                    p Действует
                                +e.col--2.--head
                                    p Кол-во людей
                                +e.col--3.--head
                                    p Тип доступа*
                                +e.col--4.--head
                                    p Стоимость
                        +e.body
                            +e.scroller
                                +e.line(v-for="item in 2")
                                    +e.wrapper--line
                                        +e.col--1.--body
                                            p 1 день
                                        +e.col--2.--body
                                            p 1 человек
                                        +e.col--3.--body
                                            p Базовый
                                        +e.col--4.--body
                                            p 900 бат
                                        +e.col--5.--body
                                            +e.BUTTON.button.button--skew.--yellow(type="button")
                                                span Купить
                                                    b за 99999 бат
                                +e.line(v-for="item in 2")
                                    +e.wrapper--line
                                        +e.col--1.--body
                                            p 1 день
                                        +e.col--2.--body
                                            p 1 человек
                                        +e.col--3.--body
                                            p Базовый
                                        +e.col--4.--body.--sale
                                            b 3000 бат #[strong 12 900 бат] #[div #[p -30%]]
                                        +e.col--5.--body
                                            +e.BUTTON.button.button--skew.--yellow.--sale(type="button")
                                                span Купить #[i за #[b 3000 бат #[strong 12 900 бат] #[div #[p -30%]]]]
                    +e.cards.cards__(:class="{'active': activeTab.index === 1}")
                        +e.item(:class="{'active': toggleIndex === index}" v-for="item,index in 2")
                            +e.wrapper--item
                                +e.top
                                    +e.BUTTON.button--toggle.button(type="button" :class="{'active': toggleIndex === index}" @click="toggleVillas(index)")
                                        span Вилла Дель Twin
                                            b
                                    +e.min-price
                                        p Проживание от #[span 70000 бат]
                                +e.toggle
                                    +e.wrapper--toggle
                                        +e.img
                                            img(src="public/media/images/prices_img.jpg")
                                        +e.content
                                            p Двухэтажный дом на 2 спальни c уникальной придомовой территорией, зелеными насаждениями и живой оградой.
                                            p 260 кв.м. прекрасно спланированной жилой площади включает в себя 2 спальни, 2 ванные комнаты, гостиную и кухню.
                                            p Снаружи тропический сад — еще одна привлекательная особенность.
                                +e.info
                                    +e.col--1
                                        span Срок действия
                                        p 7 дней
                                    +e.col--2
                                        span Размещение до
                                        p 4
                                    +e.col--3
                                        span Тип доступа
                                        p Полный*
                                    +e.col--4
                                        span Проживание от
                                        p Top Mountain Village
                                    +e.BUTTON.button--price.button--skew.--yellow(type="button")
                                        span Купить #[b от 70000 бат]
                +e.notice.notice__
                    +e.item
                        span Базовый*
                        p Питание и работа с тренером не включены
                    +e.item
                        span Полный*
                        p Питание и работа с тренером при размещении в TMV

 </template>

<script>

    export default {
        data() {
            return {
                toggleIndex: null,
                activeTab: {
                    index: 0,
                    left: 0,
                    width: 0
                }
            };
        },
        methods: {
            toggleTabs(index) {
                if (index === 0) {
                    this.activeTab.left = this.$refs['tab' + index].offsetLeft - 2;
                } else {
                    this.activeTab.left = this.$refs['tab' + index].offsetLeft + 2;
                }
                this.activeTab.width = this.$refs['tab' + index].clientWidth + 1;
                this.activeTab.index = index;
            },
            toggleVillas(index) {
                if (index !== this.toggleIndex) {
                    this.toggleIndex = index;
                } else {
                    this.toggleIndex = null;
                }
            }
        },
        mounted() {
            this.toggleTabs(0);
        }
    };
</script>