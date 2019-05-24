<template>
	<div class="container" @click="hideGallary">
		<div class="wrapper">
			<swiper :options="swiperOption">
			    <!-- slides -->
			    <swiper-slide v-for="(item, index) in imgs" :key="index">
			    	<img class="gallary-img" :src="item"/>
			    </swiper-slide>
			    <!-- Optional controls -->
			    <div class="swiper-pagination"  slot="pagination"></div>
			</swiper>
		</div>
	</div>
</template>

<script>
	export default {
		name:'commonGallary',
		props:{
			imgs:{
				type:Array,
				default (){
					return []
				}
			}
		},
		data (){
			return {
				swiperOption:{
					pagination:'.swiper-pagination',
					paginationType:'fraction',
					observeParents:true,
					observer:true
				}
			}
		},
		methods:{
			hideGallary () {
				this.$emit("hideGallary")
			}
		}
	}
</script>

<style lang="stylus" scoped>
	.container >>> .swiper-container
		overflow: inherit;
	.container
		display:flex
		flex-direction:column
		justify-content:center
		z-index:99
		position:absolute
		top:0
		left:0
		right:0
		bottom:0
		background:#000
		.wrapper
			background:#fff
			.gallary-img
				width:100%
			.swiper-pagination-fraction
				bottom:-30px
				color:#fff
</style>