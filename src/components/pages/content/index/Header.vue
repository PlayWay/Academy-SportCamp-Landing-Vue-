<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.header
        +e.container.container
            +e.wrapper.wrapper
                +e.logo
                     img(src="/public/media/images/logo.svg")
                +e.list
                    +e.A.item(href="#")
                        span Дисциплины
                    +e.A.item(href="#")
                        span Цены
                    +e.A.item(href="#")
                        span Написать нам

</template>

<script>

    export default {
        data() {
            return {};
        },
    };
</script>