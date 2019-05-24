<template>
	<div class="list" ref="wrapper">
		<div>
			<div class="area">
				<div class="title border-topbottom">当前城市</div>
				<div class="buttom-list">
					<div class="buttom buttom-wrapper">
						<div class="buttom">{{this.$store.state.city}}</div>
					</div>
				</div>
			</div>
			<div class="area">
				<div class="title border-topbottom">热门城市</div>
				<div class="buttom-list">
					<div class="buttom buttom-wrapper" 
						v-for="item of hot" 
						:key="item.id"
						@click="clickCity(item.name)"
					>
						<div class="buttom">{{item.name}}</div>
					</div>
				</div>
			</div>
			<div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
				<div class="title border-topbottom">{{key}}</div>
				<div class="item-list">
					<div class="item border-bottom" 
						v-for="itemname of item" 
						:key="itemname.id"
						@click="clickCity(itemname.name)"
					>
					{{itemname.name}}
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import BScroll from 'better-scroll'
	export default{
		name:'cityList',
		props:{
			hot:Array,
			cities:Object,
			letter:String
		},
		methods:{
			clickCity (city) {
				this.$store.commit('changeCity',city)
				this.$router.push("/")
			}
		},
		mounted () {
			this.scroll = new BScroll(this.$refs.wrapper)
		},
		watch:{
			letter () {
				if(this.letter){
					const ele = this.$refs[this.letter][0]
					this.scroll.scrollToElement(ele)
				}
			}
		}
	}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.border-topbottom
	 &:before
	 	border-color:#ccc
	 &:after
	 	border-color:#ccc
	.border-bottom
	&:before
		border-color:#ccc
	.list
		overflow:hidden
		position:absolute
		top:1.58rem
		left:0
		right:0
		bottom:0
		.title
			line-height:.54rem
			background:#ccc
			padding-left:.2rem
			color:#666
			font-size:.26rem
		.buttom-list
			overflow:hidden
			padding:.1rem .6rem .1rem .1rem
			.buttom-wrapper
				float:left
				width:33.3%
				.buttom
					border:.02rem solid #ccc
					text-align:center
					margin:.1rem
					padding:.1rem 0
					border-radius:.06rem
		.item-list
			
			.item
				line-height:.76rem
				color:#666
				padding-left:.2rem
			
</style>