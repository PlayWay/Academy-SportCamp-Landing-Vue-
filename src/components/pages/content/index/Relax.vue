<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.relax
        parallax-container.horizontal-card
            +e.container.container
                +e.H2.title.title Семейный #[span отдых]
                +e.content
                    +e.background
                        +e.img--family
                            parallax-element.background-image(:parallaxStrength="-0.3" :type="'depth'")
                                img(src="public/media/images/relax/bg.png")
                    +e.text--noImage
                        p Это хорошая возможность провести незабываемое время вместе с близкими. Восстановить силы и посетить значимые места Паттайи
                    +e.line
                        +e.text--pineapple
                            span Будьте здоровы
                            p Наслаждайтесь вкуснейшими тропическими фруктами и коктейлями из свежего манго, которые помогают вашему организму провести полную детоксикацию
                            +e.img--pineapple.--absolute
                                parallax-element.background-image(:parallaxStrength="-0.5" :type="'translation'")
                                    img(src="public/media/images/relax/pineapple.svg")
                            +e.img--apple.--absolute
                                parallax-element.background-image(:parallaxStrength="0.5" :type="'translation'")
                                    img(src="public/media/images/relax/apple.svg")
                        +e.text--banana
                            span Наслаждайтесь отдыхом
                            p На территории расположены SPA, спортивная площадка, бассейн и прочие приятные мелочи.
                            +e.img--juice.--absolute
                                parallax-element.background-image(:parallaxStrength="0.5" :type="'translation'")
                                    img(src="public/media/images/relax/juice.svg")
                            +e.img--banana.--absolute
                                parallax-element.background-image(:parallaxStrength="-0.5" :type="'translation'")
                                    img(src="public/media/images/relax/banana.svg")
</template>

<script>

    export default {
        data() {
            return {};
        },
    };
</script>