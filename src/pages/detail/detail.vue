<template>
	<div>
		<detail-banner 
			:bannerImg="bannerImg" 
			:bannerImgs="bannerImgs" 
			:sightName="sightName">
		</detail-banner>
		<detail-header></detail-header>
		<div class="container">
			<detail-list :list="list"></detail-list>
		</div>
	</div>
</template>

<script>
	import detailBanner from './components/banner'
	import detailHeader from './components/header'
	import detailList from './components/list'
	import axios from 'axios'
	export default {
		name:'Detail',
		components:{
			detailBanner,
			detailHeader,
			detailList
		},
		data () {
			return {
				bannerImg:'',
				bannerImgs:[],
				sightName:'',
				list: []
			}
		},
		methods:{
			getDetailInfo (){
				axios.get('/api/detail.json',{
					params:{
						id:this.$route.params.id
					}
				}).then(this.getDetailInfoSucc)
			},
			getDetailInfoSucc(res){
				if(res.data.ret && res.data.data){
					this.list = res.data.data.categoryList
					this.sightName = res.data.data.sightName
					this.bannerImg = res.data.data.bannerImg
					this.bannerImgs = res.data.data.gallaryImgs
				}
			}
		},
		mounted (){
			this.getDetailInfo()
		}
	}
</script>

<style lang="stylus" scoped>
	.container
		height:50rem
</style>