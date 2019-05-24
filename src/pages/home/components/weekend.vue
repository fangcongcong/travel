<template>
	<div>
		<div class="recommend-title">周末去哪儿</div>
		<div class="item" v-for="item of weekendList" :key="item.id">
			<div class="item-img-wrap">
				<img class="item-img" :src="item.imgUrl" />
			</div>
			<div class="item-info">
				<p class="item-title">{{item.title}}</p>
				<p class="item-desc">{{item.desc}}</p>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		name:'homeWeekend',
		props:{
			weekendList:Array
		}
	}
</script>

<style lang="stylus" scoped>
	@import '~styles/mixins.styl'
	.recommend-title
		line-height:.8rem
		text-indent:.2rem
		background:#ccc
	.item-img-wrap
		overflow:hidden
		height:0
		padding-bottom:37.17%
		.item-img
			width:100%
	.item-info
		flex:1
		padding:.1rem
		min-height:0
		.item-title
			line-height:.54rem
			font-size:.32rem
			ellipsis()
		.item-desc
			line-height:.4rem
			color:#ccc
			ellipsis()
</style>
