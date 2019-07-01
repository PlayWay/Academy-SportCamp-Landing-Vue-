<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.MAIN.main
        +e.slider.swiper-container.slider__(
            v-swiper:mySwiper="swiper" ref="swiper")
            +e.wrapper.swiper-wrapper
                +e.item.swiper-slide(
                    v-for="(item,index) in titleText"
                    ref="slides"
                    :class="{'hide': animation.hide === index,'next': animation.next === index,'prev':  animation.prev === index }"
                    )
                    +e.wrap
                        +e.img
                            IMG.swiper-lazy(data-src="public/media/images/slide1.jpg")
                        +e.content
                            +e.container.container
                                +e.H1.title(
                                    ref="title"
                                    v-html="splitSpan(item)"
                                    ) {{ item }}
                                        <!--+e.DIV.stroke-wrapper(-->
                                            <!--v-html="splitSpan(item)"-->
                                            <!--ref="strokeWrapper"-->
                                            <!--)-->
                                +e.buttons(:style="{transitionDelay: animation.delayButtons}")
                                    +e.A.button--more.button--skew.--yellow(href="#")
                                        span Узнать больше
                                    +e.A.button--order.button--skew.--transparent(href="#")
                                        span Оставить заявку
</template>

<script>
    import { TweenLite } from 'gsap'

    export default {
        data() {
            return {
                swiper: {
                    freeMode: false,
                    slidesPerView: 'auto',
                    init: true,
                    loop: true,
                    lazy: {
                        loadPrevNext: true
                    },
                    effect: 'fade',
                    speed: 1000,
                    preventInteractionOnTransition: true,
                    on: {
                        init: () => {
                            setTimeout(() => {
                                let titles = document.querySelectorAll('.slider__title');

//                                this.animation.delayButtons = `${parseFloat(this.getStyle(title[title.length - 1],'transitionDelay')) + 0.05}s`;
                                for (let i = 0; i < titles.length; i++) {

                                    let p = titles[i].getElementsByTagName('p');

                                    this.mySwiper.slides[i].querySelector('.slider__buttons').style.transitionDelay = `${parseFloat(this.getStyle(p[p.length - 1],'transitionDelay')) + 0.05}s`;
                                }
                            })
                        },
                        slideChangeTransitionEnd:() => {
                            this.animation.hide = null;

                            this.animation.gsap.map( (item) => {
                                TweenLite.set(item.target,{clearProps: "width"})
                                item.kill();
                            });

                            this.animation.gsap = [];

                            setTimeout(() => {
                                this.loading(this.mySwiper.activeIndex);
                            })
                        },
                        slideNextTransitionStart: () => {
                            setTimeout(() => {

                                if (!this.animation.start) {
                                    this.animation.start = true;
//                                    this.animation.next = this.mySwiper.realIndex + 1;
                                } else {
                                    this.animation.next = null;
                                    this.animation.hide = this.mySwiper.activeIndex - 2;

                                    if (this.mySwiper.activeIndex >= this.titleText.length) {
//                                        this.animation.next = 0;

                                        if (this.mySwiper.activeIndex !== this.mySwiper.slides.length - 1) {
                                            this.mySwiper.slides[this.mySwiper.activeIndex + 1].classList.add('next');
                                        } else {
                                            this.mySwiper.slides[this.mySwiper.activeIndex].classList.remove('next');
                                            this.mySwiper.slides[this.titleText.length - 1].classList.remove('prev');
                                            this.animation.next = 1;
                                        }

                                    }
                                }
                            })
                        },
                        slideNextTransitionEnd: () => {

                        },
                        slidePrevTransitionStart: () => {

                            setTimeout(() => {

                                this.animation.hide = this.mySwiper.activeIndex;

                                setTimeout(() => {
                                    this.animation.hide = null;
                                },600)


                                if (this.mySwiper.activeIndex === 0) {
                                    this.mySwiper.slides[this.titleText.length - 1].classList.add('prev');
                                } else {
                                    this.mySwiper.slides[this.titleText.length - 1].classList.remove('prev');
                                    this.mySwiper.slides[this.mySwiper.activeIndex].classList.remove('next');
                                }
                            })
                        }
                    }
                },
                titleText: ['Тренировочный лагерь полного цикла в Паттайе','Тренировочный лагерь полного цикла в Паттайе alo alo','Тренировочный лагерь полного цикла в Паттайе alo alo'],
                offsetLeft: null,
                animation: {
                    hide: null,
                    next: null,
                    priv: null,
                    start: false,
                    gsap: [],
                    delayButtons: 0
                }
            };
        },
        methods: {
            splitSpan(text) {
                let arr = text.split(' '),
                    strokeArr = [],
                    titleArr=[],
                    count = 0,
                    currentIndex = 0;

                arr.map((item,index) => {

                    if (item.length + count <= 15) {

                        if (typeof strokeArr[currentIndex] !== 'undefined') {
                            strokeArr[currentIndex] += ' ' + item;
                        } else {
                            strokeArr[currentIndex] =  item;
                        }
                        count += item.length + 1;

                        if (index === arr.length - 1) {
                            titleArr[currentIndex] = `<p>${strokeArr[currentIndex]}</p>`;
                            strokeArr[currentIndex] = `<span class="stroke">${strokeArr[currentIndex]}</span>`;
                        }
                    } else {
                        titleArr[currentIndex] = `<p>${strokeArr[currentIndex]}</p>`;
                        strokeArr[currentIndex] = `<span class="stroke">${strokeArr[currentIndex]}</span>`;
                        count = 0;
                        currentIndex++;
                        strokeArr[currentIndex] = item;
                        count = item.length;
                    }
                });

                titleArr = `${titleArr.join('')}<div class="slider__stroke-wrapper">${strokeArr.join('')}</div>`

                return titleArr;
            },
            getStyle(el, styleProp) {
                let value, defaultView = (el.ownerDocument || document).defaultView;
                // W3C standard way:
                if (defaultView && defaultView.getComputedStyle) {
                    // sanitize property name to css notation
                    // (hypen separated words eg. font-Size)
                    styleProp = styleProp.replace(/([A-Z])/g, "-$1").toLowerCase();
                    return defaultView.getComputedStyle(el, null).getPropertyValue(styleProp);
                } else if (el.currentStyle) { // IE
                    // sanitize property name to camelCase
                    styleProp = styleProp.replace(/\-(\w)/g, function(str, letter) {
                        return letter.toUpperCase();
                    });
                    value = el.currentStyle[styleProp];
                    // convert other units to pixels on IE
                    if (/^\d+(em|pt|%|ex)?$/i.test(value)) {
                        return (function(value) {
                            var oldLeft = el.style.left, oldRsLeft = el.runtimeStyle.left;
                            el.runtimeStyle.left = el.currentStyle.left;
                            el.style.left = value || 0;
                            value = el.style.pixelLeft + "px";
                            el.style.left = oldLeft;
                            el.runtimeStyle.left = oldRsLeft;
                            return value;
                        })(value);
                    }
                    return value;
                }
            },
            loading(index) {
                let time = 3,
                    spans = this.mySwiper.slides[index].querySelectorAll('.stroke'),
                    step = null;

                step = time / (spans.length-1);

                for (let i = 0; i < spans.length; i++) {

                    this.animation.gsap[i] = TweenLite.to(
                        spans[i],
                        step,
                        {css: {width: spans[i].scrollWidth + 'px'}, delay: step*i,ease: Power0.easeNone,
                        onComplete: () => {
                            if (i === spans.length - 1) {
                                this.hide = index;
                                this.mySwiper.slideNext();
                                setTimeout(() => {
                                    TweenLite.set(spans,{clearProps: "width"})
                                },1000)
                            }
                        }}
                    );
                }
            }
        },
    };
</script>