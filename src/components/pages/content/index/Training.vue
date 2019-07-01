<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.training
        +e.container.container
            +e.background
                img(src="public/media/images/training-bg_mobile.png")
            +e.wrapper.wrapper
                +e.H2.title.title тренируйся #[br] #[span и живи]
                +e.P.info Наш лагерь посещают много известных спортсменов и звезд. Хотите стать лучше? Тренируйтесь с лучшими!
                +e.UL.list.list__
                    +e.LI.item--training
                        span 10 минут
                        p Дорога до Паттайи
                    +e.LI.item--training
                        span 200 +
                        p Гостей обслуживается
                    br
                    +e.LI.item--training
                        span 15 тренеров
                        p Профессионалов своего дела
                +e.A.button.button.button--skew.--transparent(href="#prices" v-scroll-to="'#prices'")
                    span Посмотреть цены
</template>

<script>

    export default {
        data() {
            return {};
        },
    };
</script>