<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.program
        +e.container.container
            +e.H2.title.title #[span Программа]  ТРенировки
            +e.fighter
                +e.background-left
                    img(src="/public/media/images/image-bg_program.png")
                +e.img
                    img(src="/public/media/images/program-fighter_tablet.png")
            +e.content
                +e.tabs.tabs__
                    +e.BUTTON.item--program.button(type="button" :class="{'active': activeTab.index === 0}" @click="toggleTabs(0)" ref="tab0")
                        span Похудения
                    +e.BUTTON.item--program.button(type="button" :class="{'active': activeTab.index === 1}" @click="toggleTabs(1)" ref="tab1")
                        span Muay Thai
                    +e.BUTTON.item--program.button(type="button" :class="{'active': activeTab.index === 2}" @click="toggleTabs(2)" ref="tab2")
                        span MMA
                    +e.active(
                        ref="activeTab"
                        :style="{left: activeTab.left + 'px',width: activeTab.width + 'px'}"
                        )
                +e.training-lists
                    +e.block(v-for="(item,index) in programs" :class="activeTab.states[index]")
                        +e.UL.list--left
                            +e.LI.item--small-font(v-for="step in item.steps")
                                span {{ step.name }}
                                p {{ step.text }}
                        +e.UL.list--right
                            +e.LI.item--big-font(v-for="block in item.list")
                                span {{ block.col }}
                                p {{ block.text }}
                +e.A.button--prices.button--skew.--yellow(href="#" v-scroll-to="'#prices'")
                    span Посмотреть цены
</template>

<script>

    export default {
        data() {
            return {
                activeTab: {
                    index: 0,
                    left: 0,
                    width: 0,
                    states: ['active','next','next']
                },
                programs: [
                    {
                        steps: [
                            {
                                name: '01. Цель тренировки',
                                text: 'Отработка техники ударов и элементов защиты, развитие силы, ловкости, выносливости.'
                            },
                            {
                                name: '02. Уровень подготовки:',
                                text: 'Любой — нагрузка подбирается инструктором индивидуально.'
                            }
                        ],
                        list: [
                            {
                                col: '15-20',
                                text: 'Минут разминки'
                            },
                            {
                                col: '60-70',
                                text: 'Минут основная часть'
                            },
                            {
                                col: '90',
                                text: 'Минут продолжительность'
                            }
                        ]
                    },
                    {
                        steps: [
                            {
                                name: '01. Цель ',
                                text: 'Отраб силы, ловкости, выносливости.'
                            },
                            {
                                name: '02. Уподготовки:',
                                text: 'Любтруктором индивидуально.'
                            }
                        ],
                        list: [
                            {
                                col: '15-20',
                                text: 'Минут '
                            },
                            {
                                col: '60-70',
                                text: 'Минут  часть'
                            },
                            {
                                col: '90',
                                text: 'Минут '
                            }
                        ]
                    },
                    {
                        steps: [
                            {
                                name: '01. Цель тренировки',
                                text: 'Отработка техники уды, ловкости, выносливости.'
                            },
                            {
                                name: '02. Уровень :',
                                text: 'Любой — .'
                            }
                        ],
                        list: [
                            {
                                col: '15-20',
                                text: 'Минут разминки'
                            },
                            {
                                col: '70',
                                text: 'Минутя часть'
                            },
                            {
                                col: '90',
                                text: 'Минут пельность'
                            }
                        ]
                    }
                ]
            };
        },
        methods: {
            toggleTabs(index) {
//            :class="{'active': activeTab.index === index,'next': activeTab.next === index,'prev': activeTab.prev === index}"
                switch(index) {
                    case 0:
                        this.activeTab.left = this.$refs['tab' + index].offsetLeft - 3;
                        this.activeTab.states = ['active','next','next'];
                        break;
                    case 1:
                        this.activeTab.left = this.$refs['tab' + index].offsetLeft;
                        this.activeTab.states = ['prev','active','next'];
                        break;
                    case 2:
                        this.activeTab.left = this.$refs['tab' + index].offsetLeft + 3;
                        this.activeTab.states = ['prev','prev','active'];
                        break;
                }

                this.activeTab.width = this.$refs['tab' + index].clientWidth;
                this.activeTab.index = index;
            }
        },
        mounted() {
            this.toggleTabs(0);
        },
        watch: {
            'activeTab.index': function (newValue,oldValue) {
                if (newValue === 2 && oldValue === 0) {
//                    this.activeTab
                }
            }
        }
    };
</script>