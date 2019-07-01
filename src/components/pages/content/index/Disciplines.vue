<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.disciplines
        +e.container.container
            +e.H2.title.title ДИСЦИПЛИНЫ #[br]#[span и ВОЗМОЖНОСТИ]
            +e.slider.swiper-container(v-swiper:main="swiper")
                +e.wrapper.swiper-wrapper
                    +e.slide.swiper-slide(v-for="item in items")
                        parallax-container.vertical-card.centered-card
                            parallax-element.background-image(:parallaxStrength="-10" :type="'depth'")
                                +e.img
                                    img(:src="item.img")
                            +e.name.text-shadow
                                parallax-element.text-container(:parallaxStrength="1" :type="'translation'")
                                    span(v-html="item.name")
                                    //b {{ item.name }}
                            +e.info
                                parallax-element.text-container(:parallaxStrength="-2" :type="'translation'")
                                    p(v-html="item.info")
            +e.pagination
</template>

<script>

    export default {
        data() {
            return {
                swiper: {
                    freeMode: false,
                    init: false,
                    slidesPerView: 1,
                    loop: true,
                    pagination: {
                        el: '.disciplines__pagination',
                        type: 'bullets',
                        clickable: false,
                        bulletClass: 'disciplines__bullet',
                        bulletActiveClass: 'active'
                    },
                },
                items: [
                    {
                        img: 'public/media/images/disciplines/1.png',
                        name: 'FITNESS, CROSSFIT & <br> POWER TRAINING <b>FITNESS, CROSSFIT & <br> POWER TRAINING</b>',
                        info: 'Фитнес и <br> Кроссфит залы'
                    },
                    {
                        img: 'public/media/images/disciplines/2.png',
                        name: 'YOGA, SPA <br> & MASSAGE <b>YOGA, SPA <br> & MASSAGE</b>',
                        info: 'Финская сауна и Джакузи.<br>Йога Студия (90 квм)'
                    },
                    {
                        img: 'public/media/images/disciplines/3.png',
                        name: 'Volleyball<br> & Soccer <b>Volleyball<br> & Soccer</b>',
                        info: 'Поле для пляжного волейбола,<br>футбола, футволея'
                    },
                    {
                        img: 'public/media/images/disciplines/4.png',
                        name: 'SWiM ZONE<b>SWiM ZONE</b>',
                        info: 'Спортивный открытый<br> бассейн (25 х 10 м)'
                    },
                    {
                        img: 'public/media/images/disciplines/5.png',
                        name: 'LEISURE<br>ZONE<b>LEISURE<br>ZONE</b>',
                        info: 'Прокат велосипедов. Зеленая<br> релакс зона. Зона досуга:<br> бильярд, настольный тенис,батут'
                    },
                    {
                        img: 'public/media/images/disciplines/5.png',
                        name: 'LEISURE<br>ZONE<b>LEISURE<br>ZONE</b>',
                        info: 'Прокат велосипедов. Зеленая<br> релакс зона. Зона досуга:<br> бильярд, настольный тенис,батут'
                    }
                ]
            };
        },
        mounted() {
            if (window.innerWidth < 650) {
                this.main.init();
            }
        }
    };
</script>