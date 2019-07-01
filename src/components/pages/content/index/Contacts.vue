<template lang="pug">
    include ../../../../tools/mixins.pug

    +b.contacts
        +e.container.container
            +e.content
                +e.H2.title.title Расположение #[br] #[span и  контакты]
                +e.manager
                    +e.photo
                        +e.img
                            img(src="public/media/images/photo.jpg")
                    +e.name.text-shadow--right
                        span ЕЛЕНА Кудряшова #[b ЕЛЕНА Кудряшова]
                        p Менеджер по маркетингу и продажам
                +e.block--mail
                    span Электронная почта
                    a(href="mailto:helen@topmountainvillage.com") helen@topmountainvillage.com
                +e.block--half.--phone
                    span Контактный телефон
                    a(href="tel:66927125959") +66 92 712 5959
                +e.block--half.--social
                    span Социальные сети
                    +e.A.link--whats-app(href="#")
                    +e.A.link--viber(href="#")
                    +e.A.link--telegram(href="#")
                +e.block--address
                    span Адрес лагеря
                    p 16 moo 6 soi Rai Aoi Najomtien Sattahip, Thailand
            +e.location
                +e.wrapper
                    +e.map
                        googlemaps-map(
                            :center.sync="map.center"
                            :zoom.sync="map.zoom"
                            :options="map.options"
                            ref="map"
                        )
                            googlemaps-marker(
                                v-for="(item,index) in map.markers.items"
                                :title="item.title"
                                :key ="index"
                                :position="item.position"
                                :icon="map.icon"
                                :clickable="true"
                                @click="selectMarker($event,index)"
                                :ref="'marker' + index"
                            )


</template>

<script>

    export default {
        data() {
            return {
                map: {
                    center: {lat: 12.922846, lng: 100.882729},
                    point: {lat: 12.921500, lng: 100.882729},
                    zoom: 17,
                    options: {
                        zoomControl: false,
                        mapTypeControl: false,
                        scaleControl: false,
                        streetViewControl: false,

                        rotateControl: false,
                        fullscreenControl: false
                    },
                    icon: {
                        url: 'http://burno.tech/mailing/sport-camp-academy/point.svg'
                    },
                    markers: {
                        opened: {
                            el: null,
                            index: null
                        },
                        items: [
                            {
                                title: 'Pataiia',
                                position: {lat: 12.922000, lng: 100.882729},
                            },
                            {
                                title: 'Pataiia2',
                                position: {lat: 12.922800, lng: 100.882729}
                            },
                            {
                                title: 'Pataiia3',
                                position: {lat: 12.923500, lng: 100.882729}
                            }
                        ]
                    }
                }
            }
        },
        methods: {
            selectMarker(marker,index) {
                let map = this.$refs.map.$_map;

                if (this.map.markers.opened.el !== null && this.map.markers.opened.el !== marker.wa.target) {
                    let oldMarker = this.map.markers.opened.el;
                    oldMarker.setAttribute('src','http://burno.tech/mailing/sport-camp-academy/point.svg');
                    oldMarker.parentNode.style.opacity = 0;
                    this.map.markers.opened.window.close(map, this.$refs['marker' + this.map.markers.opened.index][0].$_marker)
                }

                if (this.map.markers.opened.el !== marker.wa.target) {

                    marker.wa.target.setAttribute('src','http://burno.tech/mailing/sport-camp-academy/point2.svg');
                    marker.wa.target.parentNode.style.opacity = 1;

                    let infowindow = new google.maps.InfoWindow({
                        content: '<img src="http://burno.tech/mailing/psb/1.jpg"><span>Academy Sport Camp</span><p>16 moo 6 soi Rai Aoi Najomtien Sattahip, Thailand</p>'
                    });
                    infowindow.open(map, this.$refs['marker' + index][0].$_marker);

                    this.map.markers.opened = {el: marker.wa.target, index: index, window: infowindow};
                }
            },
        },
        watch: {
            'map.markers.opened.window': function (newValue,oldValue) {
                if (newValue !== null) {
                    google.maps.event.addListener(this.map.markers.opened.window,'closeclick',() => {
                        let oldMarker = this.map.markers.opened.el;
                        oldMarker.setAttribute('src','http://burno.tech/mailing/sport-camp-academy/point.svg');
                        oldMarker.parentNode.style.opacity = 0;

                        this.map.markers.opened.el = null;
                        this.map.markers.opened.index = null;
                        this.map.markers.opened.window = null;
                    });
                }
            }
        }
    };
</script>