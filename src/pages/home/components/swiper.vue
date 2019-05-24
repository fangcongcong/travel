<template>
	<div class="swiper">
		<swiper :options="swiperOption" v-if="showSwiper">
		    <!-- slides -->
		    <swiper-slide v-for="item in list" :key="item.id">
		    	<img class="swiper-img" :src="item.imgUrl"/>
		    </swiper-slide>
		    <!-- Optional controls -->
		    <div class="swiper-pagination"  slot="pagination"></div>
		</swiper>
	</div>
</template>

<script>
	export default{
		name:'homeSwiper',
		props:{
			list:Array
		},
		data (){
			return {
				swiperOption:{
					pagination:'.swiper-pagination',
					loop:true
				}
			}
		},
		computed:{
			showSwiper () {
				return this.list.length
			}
		}
	}
</script>

<style lang="stylus" scoped>
	.swiper >>> .swiper-pagination-bullet-active
		background:#fff
	.swiper
		overflow:hidden
		width:100%
		height:0
		padding-bottom:31.25%
	.swiper-img
		width:100%
</style>