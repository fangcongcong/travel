<template>
	<div>
		<city-header></city-header>
		<city-search :cities="cities"></city-search>
		<city-list :hot="hotList" :letter="letter" :cities="cities"></city-list>
		<city-alphabet @change="getLetter" :cities="cities"></city-alphabet>
	</div>
</template>

<script>
	import axios from 'axios'
	import cityHeader from './components/cityHeader'
	import citySearch from './components/search'
	import cityList from './components/list'
	import cityAlphabet from './components/alphabet'
	export default {
		name:'city',
		components:{
			cityHeader,
			citySearch,
			cityList,
			cityAlphabet
		},
		data (){
			return {
				hotList:[],
				cities:{},
				letter:''
			}
		},
		methods:{
			getCityInfo (){
				axios.get('/api/city.json').then(this.getCityInfoSucc)
			},
			getCityInfoSucc (res){
				console.log(res)
				if(res.data.ret && res.data){
					this.hotList = res.data.data.hotCities
					this.cities = res.data.data.cities;
				}
			},
			getLetter (letter) {
				this.letter = letter
			}
		},
		mounted () {
			this.getCityInfo()
		}
	}
</script>

<style lang="stylus" scoped>
</style>