<template>
<div class="full-height">
    <flexbox :gutter="0" wrap="wrap">
        <flexbox-item :span="1/4" v-for="city in cities" :key="city.name">
            <div v-bind="city" :class="checkSelect(city.name)" 
            @click="toggleCity(city.name)">{{$t(city.name)}}</div>
        </flexbox-item>
    </flexbox>
    </div>
</template>

<script>
import {mapMutations} from 'vuex'
import { Flexbox, FlexboxItem, XButton } from 'vux'
import { mapGetters, mapActions } from 'vuex'

export default {
    components: {
        Flexbox,
        FlexboxItem,
        XButton
    },

    computed: {
        ...mapGetters([
            'cities',
            'selectedCities',
        ]),
    },

    mounted() {
        this.SET_HEADER({
            title:this.$t('More'),
            leftOption:{showBack: true}
        })
    },

    methods: {
        ...mapMutations(['SET_HEADER']),
        ...mapActions(['toggleCity']),
        checkSelect(name){
            for(let city of this.selectedCities){
                if(city.name === name){
                    return 'selector active'
                }
            }
            return 'selector'
        }
    },

  


}
</script>

<style>
.selector {
    text-align: center;
    border: 1px solid #e5e5e5;
    margin: 0.5rem 0.5rem;
    padding: 0.5rem;
    border-radius: 1rem;
}

.active {
    border: 1px solid #4078C0;
}
</style>