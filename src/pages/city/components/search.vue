<template>
	<div>
		<div class="search">
			<input class="search-input" v-model="searchVal" type="text" placeholder="输入城市名或拼音" />
		</div>
		<div class="search-content" v-show="searchVal" ref="search">
			<ul>
				<li class="search-item border-bottom" 
					v-for="item of list" 
					:key="item.id"
					@click="clickCity(item.name)"
				>
					{{item.name}}({{item.spell}})
				</li>
				<li class="search-item border-bottom" v-show="noData">没有找到相关的数据</li>
			</ul>
		</div>
	</div>
</template>

<script>
	import BScroll from 'better-scroll'
	export default {
		name:'Search',
		props:{
			cities:Object
		},
		data () {
			return {
				searchVal:'',
				list:[],
				timer:null
			}
		},
		methods:{
			clickCity (city) {
				this.$store.commit('changeCity',city)
				this.$router.push("/")
			}
		},
		mounted (){
			this.scroll = new BScroll(this.$refs.search)
		},
		computed:{
			noData (){
				return !this.list.length
			}
		},
		watch:{
			searchVal (){
				if(this.timer){
					clearTimeout(this.timer)
				}
				this.timer = setTimeout(()=>{
					let result = []
					for(let i in this.cities){
						this.cities[i].forEach((value) => {
							if(value.spell.indexOf(this.searchVal) > -1 || value.name.indexOf(this.searchVal) > -1){
								result.push(value)
							}
						})
					}
					this.list = result
				},100)
			}
		}
	}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.search
		height:.72rem
		background:$bgColor
		padding: 0rem .1rem
		.search-input
			box-sizing:border-box
			width:100%
			height:.62rem
			line-height:.62rem
			text-align:center
			border-radius:.06rem
			color:#666
			padding: 0 .1rem
	.search-content
		overflow:hidden
		position:absolute
		z-index:1
		top:1.58rem
		left:0
		bottom:0
		right:0
		background:#fff
		.search-item
			padding:.2rem
			color:#666
</style>