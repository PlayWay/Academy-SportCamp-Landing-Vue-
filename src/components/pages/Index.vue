<template lang="pug">
    include ../../../node_modules/bemto.pug/bemto.pug

    div
        header-component
        main-component
        training-component
        live-component
        program-component
        disciplines-component
        benefits-component(ref="benefits" :position="position" :shadow="shadow" @getHeight="getHeight")
        prices-component
        relax-component
        contacts-component
        footer-component
</template>

<script>
    import Header from '@/components/pages/content/index/Header.vue'
    import Main from '@/components/pages/content/index/Main.vue'
    import Training from '@/components/pages/content/index/Training.vue'
    import Live from '@/components/pages/content/index/Live.vue'
    import Program from '@/components/pages/content/index/Program.vue'
    import Disciplines from '@/components/pages/content/index/Disciplines.vue'
    import Benefits from '@/components/pages/content/index/Benefits.vue'
    import Prices from '@/components/pages/content/index/Prices.vue'
    import Relax from '@/components/pages/content/index/Relax.vue'
    import Contacts from '@/components/pages/content/index/Contacts.vue'
    import Footer from '@/components/pages/content/index/Footer.vue'

    export default {
        data() {
            return {
                position: 'absolute',
                shadow: {
                    offset: 0,
                    opacity: 0
                },
                fixedHeight: null
            };
        },
        methods: {
            fixedBenefit () {
                if (this.getScroll()[1] >= this.$refs.benefits.$el.offsetTop) {
                    this.position = 'fixed';
                    let shadow =  (this.getScroll()[1] - this.$refs.benefits.$el.offsetTop) / this.fixedHeight ;
                    console.log(shadow)

                    if (shadow > 0.4) {
                        this.shadow.opacity = 0.4;
                    } else {
                        this.shadow.opacity = shadow;
                    }

                    if (shadow > 1 ){
                        this.shadow.offset = 1;
                    } else {
                        this.shadow.offset = shadow * 0.05;
                    }
                } else {
                    this.position = 'absolute';
                }
            },
            getHeight (data) {
                this.fixedHeight = data;
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
            }
        },
        components: {
            'header-component': Header,
            'main-component': Main,
            'training-component': Training,
            'live-component': Live,
            'program-component': Program,
            'disciplines-component': Disciplines,
            'benefits-component': Benefits,
            'prices-component': Prices,
            'relax-component': Relax,
            'contacts-component': Contacts,
            'footer-component': Footer
        },
        mounted() {
            if (window.innerWidth < 650) {
                window.addEventListener('scroll', this.fixedBenefit);
                this.position = 'absolute';
            } else {
                this.position = 'relative';
            }


        },
        destroyed() {
            if (window.innerWidth < 650) {
                window.removeEventListener('scroll', this.fixedBenefit)
            }
        }
    };
</script>