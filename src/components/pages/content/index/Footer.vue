<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.footer
        +e.container.container
            +e.text--1
                p © Academy Sport Camp - все права защищены Co., Ltd
            +e.text--2.--absolute
                a(href="#" target="_blank") Политика конфиденциальности
            +e.text--3.--absolute
                p Сделано в Burno
</template>

<script>

    export default {
        data() {
            return {
                swiper: {
                    freeMode: false,
                    init: true,
                    slidesPerView: 'auto',
                    loop: true
                }
            };
        }
    };
</script>