<template>
    <div class="features-area pt-100 pb-75">
        <div class="container">
            <div 
                class="row justify-content-center"
                v-if="features !== null"
            >
                <div 
                    class="col-xl-3 col-lg-4 col-sm-6 col-md-6"
                    v-for="feature in features.singleFeatures"
                    :key="feature.id"
                >
                    <div class="single-features-box">
                        <div :class="feature.class">
                            <i :class="feature.icon"></i>
                        </div>
                        <h3>{{feature.title}}</h3>
                        <p>{{feature.shortDesc}}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Features',
    data (){
        return {
            features: null,
        }
    },
    created: async function (){
        const response = await axios.get('https://cms.pbwebvision.in/api/feature?populate=*')
        const { data: {attributes} } = response.data
        this.features = attributes
    },
}
</script>