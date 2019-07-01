<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.benefits
        +e.item--back(:style="{position: position,transform: `translate(0,${parallaxOffset}px)`}" ref="fixElement")
            +e.wrapper--back
                +e.img--back
                    img(src="public/media/images/benefit1.png")
            +e.content--back
                +e.title.text-shadow
                    span Условия #[br] размещения
                        b Условия #[br] размещения
                +e.P.info--back ASC находится на территории застройщика Top #[span Mountain Village], благодаря чему мы предлагаем выгодное размещение для наших клиентов.
        +e.item--up(:style="{boxShadow: `0px -${shadow.offset*120}px 80px 50px rgba(19,19,19,${shadow.opacity})`,transform: `translate(0,-${parallaxOffset}px)`}" ref="")
            +e.wrapper--up
                +e.img
                    img(src="public/media/images/benefit2.png")
            +e.content--up
                +e.H3.title.text-shadow
                    span Представленные #[br] кухни
                        b Представленные #[br] кухни
                +e.P.info--up На территории ASC находится ресто-зона, где готоиться не только Тайская и евпропейская кухни, но также есть зона барбекю, а также, готовятся напитки из свежих фруктов.
</template>

<script>
    import TweenLite from 'gsap';

    export default {
        props:['position','shadow'],
        data() {
            return {
                parallaxOffset: 0,
                startOffset: null
            };
        },
        methods: {
            isElementInViewport(el) {
                let top = el.offsetTop,
                    left = el.offsetLeft,
                    width = el.offsetWidth,
                    height = el.offsetHeight;

                while(el.offsetParent) {
                    el = el.offsetParent;
                    top += el.offsetTop;
                    left += el.offsetLeft;
                }

                return (
                    top < (window.pageYOffset + window.innerHeight) &&
                    left < (window.pageXOffset + window.innerWidth) &&
                    (top + height) > window.pageYOffset &&
                    (left + width) > window.pageXOffset
                );
            },
            getScroll() {
                if (window.pageYOffset !== undefined) {
                    return [pageXOffset, pageYOffset];
                } else {
                    let sx, sy, d = document,
                        r = d.documentElement,
                        b = d.body;
                    sx = r.scrollLeft || b.scrollLeft || 0;
                    sy = r.scrollTop || b.scrollTop || 0;
                    return [sx, sy];
                }
            },
            getOffset( el ) {
                let _x = 0,
                    _y = 0;
                while( el && !isNaN( el.offsetLeft ) && !isNaN( el.offsetTop ) ) {
                    _x += el.offsetLeft - el.scrollLeft;
                    _y += el.offsetTop - el.scrollTop;
                    el = el.offsetParent;
                }
                return { top: _y, left: _x };
            },
            onScroll() {
                if (this.isElementInViewport(this.$refs.fixElement)) {

                    let transform = (this.getScroll()[1] - this.startOffset  + window.innerHeight)/25;

                    TweenLite.to(this, 1, {
                        parallaxOffset: transform,
                        ease: Expo.linear,
                    });
                }
            }
        },
        mounted() {
            this.$emit('getHeight', this.$refs.fixElement.clientHeight);
            this.startOffset = this.getOffset(this.$refs.fixElement).top;

            document.addEventListener('scroll', this.onScroll);
        },
        destroyed() {
            document.removeEventListener('scroll', this.onScroll);
        }
    };
</script>