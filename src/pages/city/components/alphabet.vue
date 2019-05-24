<template>
	<ul class="list">
		<li class="item" 
			v-for="item of letters" 
			:key="item"
			:ref="item"
			@touchstart.prevent="touchSatrt"
			@touchmove="touchMove"
			@touchend="touchEnd"
			@click="letterClick"
		>
			{{item}}
		</li>
	</ul>
</template>

<script>
	export default {
		name:'cityAlphabet',
		props:{
			cities:Object
		},
		computed:{
			letters () {
				const letters = []
				for(let i in this.cities){
					letters.push(i) //字母A~Z
				}
				return letters
			}
		},
		data (){
			return {
				falg:false,
				startY:0,
				timer:null
			}
		},
		updated (){
			this.startY = this.$refs['A'][0].offsetTop
		},
		methods:{
			letterClick (e) {
				this.$emit("change",e.target.innerText)
			},
			touchSatrt () {
				this.falg = true
			},
			touchMove (e) {
				if(this.falg){
					if(this.timer){
						clearTimeout(this.timer)
					}
					this.timer = setTimeout(() => {
						const touchY = e.touches[0].clientY - 79
						const index = Math.floor((touchY - this.startY) / 20)
						if(index >= 0 && index < this.letters.length){
							this.$emit("change",this.letters[index])
						}
					},16)
				}
			},
			touchEnd () {
				this.falg = false
			}
		},
		mounted () {
			
		}
	}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.list
		display:flex
		flex-direction:column  
		justify-content:center
		width:.4rem
		position:absolute
		top:1.58rem
		bottom:0
		right:0
		.item
			line-height:.4rem
			text-align:center
			color:$bgColor
</style>