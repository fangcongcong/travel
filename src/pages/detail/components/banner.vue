<template>
	<div>
		<div class="banner-wrapper" @click="clickBanner">
			<img class="banner-img" :src="bannerImg" />
			<div class="banner-info">
				<div class="banner-title">{{sightName}}</div>
				<div class="banner-number"><span class="iconfont border-icon">&#xe64b;</span>39</div>
			</div>
		</div>
		<fade-animation>
			<common-gallary :imgs="bannerImgs" v-if="showGallary" @hideGallary="hideGallary"></common-gallary>
		</fade-animation>
	</div>
</template>

<script>
	import commonGallary from 'common/gallary/gallary'
	import fadeAnimation from 'common/fade/fadeAnimation'
	export default {
		name:'detailBanner',
		props:{
			sightName:String,
			bannerImgs:Array,
			bannerImg:String
		},
		data (){
			return {
				showGallary:false
			}
		},
		components:{
			commonGallary,
			fadeAnimation
		},
		methods:{
			clickBanner () {
				this.showGallary = true
			},
			hideGallary () {
				this.showGallary = false
			}
		}
	}
</script>

<style lang="stylus" scoped>
	.banner-wrapper
		position:relative
		overflow:hidden
		height:0
		padding-bottom:55%
		.banner-img
			width:100%
		.banner-info
			display:flex
			position:absolute
			left:0
			bottom:0
			right:0
			color:#fff
			background-image:linear-gradient(top,rgba(0,0,0,0),rgba(0,0,0,0.8))
			.banner-title
				flex:1
				height:.6rem
				line-height:.6rem
				padding:0 .2rem
			.banner-number
				margin-top:.14rem
				height:.32rem
				padding:0 .4rem
				line-height:.32rem
				background:rgba(0,0,0,0.8)
				border-radius:.2rem
				font-size:.32rem
				.border-icon
					font-size:.32rem
</style>