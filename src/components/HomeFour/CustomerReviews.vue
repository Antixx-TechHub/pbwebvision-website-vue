<template>
    <div class="feedback-area bg-gradient-color ptb-100">
        <div 
            class="container"
            v-if="feedbacks !== null"
        >
            <div class="row">
                <div class="col-lg-4 col-md-12">
                    <div class="feedback-section-title">
                        <span class="sub-title">{{feedbacks.subtitle}}</span>
                        <h2>{{feedbacks.heading}}</h2>
                    </div>
                </div>
                <div class="col-lg-8 col-md-12">
                    <div class="feedback-slides-two">
                        <carousel
                            :autoplay="5000"
                            :settings='settings'
                            :breakpoints='breakpoints'
                        >
                            <slide 
                                v-for="slide in feedbacks.singleFeedbacks" 
                                :key="slide.id"
                            >
                                <div class="single-feedback-box">
                                    <div class="client-info">
                                        <div class="d-flex align-items-center">
                                            <img :src="slide.image.data.attributes.url" alt="user">
                                            <div class="title">
                                                <h3>{{slide.name}}</h3>
                                                <span>{{slide.position}}</span>
                                            </div>
                                        </div>
                                    </div>
                                    <p>{{slide.desc}}</p>
                                    <div class="rating d-flex align-items-center justify-content-between">
                                        <h5>{{slide.category}}</h5>
                                        <div>
                                            <i class="ri-star-fill"></i>
                                            <i class="ri-star-fill"></i>
                                            <i class="ri-star-fill"></i>
                                            <i class="ri-star-fill"></i>
                                            <i class="ri-star-fill"></i>
                                        </div>
                                    </div>
                                </div>
                            </slide>

                            <template #addons>
                                <Pagination />
                            </template>
                        </carousel>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { defineComponent } from 'vue';
import { Carousel, Slide, Pagination } from 'vue3-carousel';

import 'vue3-carousel/dist/carousel.css';

export default defineComponent ({
    name: 'CustomerReviews',
    components: {
        Carousel,
        Slide,
        Pagination,
    },
    data: () => ({
        settings: {
            itemsToShow: 1,
            snapAlign: 'center',
        },
        feedbacks: null,
        breakpoints: {
            0: {
                itemsToShow: 1,
                snapAlign: 'center',
			},
            576: {
                itemsToShow: 1,
                snapAlign: 'center',
            },
            768: {
                itemsToShow: 2,
                snapAlign: 'center',
            },
            992: {
                itemsToShow: 2,
                snapAlign: 'center',
            },
            1200: {
                itemsToShow: 2,
                snapAlign: 'center',
            },
        },
    }),
    created: async function (){
        const response = await axios.get('https://cms.pbwebvision.in/api/customerreview?populate=singleFeedbacks.image')
        const { data: {attributes} } = response.data
        this.feedbacks = attributes
    },
})
</script>