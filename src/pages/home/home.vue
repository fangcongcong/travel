<template>
	<div>
		<home-header></home-header>
		<home-swiper :list="swiperList"></home-swiper>
		<home-icons :iconsList="iconsList"></home-icons>
		<home-recommend :recommendList="recommendList"></home-recommend>
		<home-weekend :weekendList="weekendList"></home-weekend>
	</div>
</template>

<script>
	import homeHeader from './components/header'
	import homeSwiper from './components/swiper'
	import homeIcons from './components/icons'
	import homeRecommend from './components/recommend'
	import homeWeekend from './components/weekend'
	import axios from 'axios'
	import {mapState} from 'vuex'
	export default {
		name: 'home',
		components:{
			homeHeader,
			homeSwiper,
			homeIcons,
			homeRecommend,
			homeWeekend
		},
		data () {
			return {
				lastCity:'',
				swiperList:[],
				iconsList:[],
				recommendList:[],
				weekendList:[]
			}
		},
		computed:{
			...mapState(['city'])
		},
		methods: {
			getHomeInfo (){
				axios.get('/api/index.json?city='+this.city).then(this.getHomeInfoSucc)
			},
			getHomeInfoSucc (res) {
				res = res.data
				if(res.ret && res.data){
					this.swiperList = res.data.swiperList
					this.iconsList = res.data.iconList
					this.recommendList = res.data.recommendList
					this.weekendList = res.data.weekendList
				}
			}
		},
		mounted () {
			this.lastCity = this.city
			this.getHomeInfo()
		},
		activated () {
			if(this.lastCity !== this.city){
				this.lastCity = this.city
				this.getHomeInfo()
			}
		}
	}
</script>

<style>
</style>