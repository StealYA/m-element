<template>
	<div class="goods">
		<div class="menu-wrapper" ref="menuWrapper">
			<ul>
				<li v-for="item in goods" class="menu-item">
					<i v-show="item.type>0" class="icon"></i><span class="text border-1px">{{item.name}}</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper" ref="foodWrapper">
			<ul>
				<li v-for="item in goods" class="food-list">
					<h1 class="title">{{item.name}}</h1>
					<ul>
						<li v-for="food in item.foods" class="food-item border-1px">
							<div class="icon">
								<img :src="food.icon" alt="" width="57" height="57">
							</div>
							<div class="content">
								<h2 class="name">{{food.name}}</h2>
								<p class="desc">{{food.description}}</p>
								<div class="extra">
									<span class="count">月售{{food.sellCount}}份</span>
									<span>好评率{{food.rating}}%</span>
								</div>
								<div class="price">
									<span class="nprice"><span class="symbol">¥</span>{{food.price}}</span>
									<span v-show="food.oldPrice" class="oprice">¥{{food.oldPrice}}</span>
								</div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	import BScroll from 'better-scroll';

	const ERR_OK = 0;

	export default {
		props: {
			seller: Object
		},
		data() {
			return {
				goods: []
			};
		},
		created() {
			this.$http.get('/api/goods').then( (res) => {
				res = res.body;
				if(res.errno === ERR_OK) {
					this.goods = res.data;
					this.$nextTick(() => {
						this._initScroll();
					})
					
				}
				//console.log(this.goods);
			})
		},
		methods: {
			_initScroll() {
				this.menuScroll = new BScroll(this.$refs.menuWrapper,{});

				this.foodScroll = new BScroll(this.$refs.foodWrapper,{});
			}
		}
	};
</script>

<style lang="stylus"rel="stylesheet/stylus">

	@import "../../common/stylus/mixin";

	.goods
		display:flex
		position:absolute
		top:174px
		width:100%
		bottom:46px
		overflow:hidden
		.menu-wrapper
			flex:0 0 80px
			width:80px
			background:#f3f5f7                      //#f3f5f7
			.menu-item
				display:table
				width:56px
				height:54px
				line-height:14px
				padding:0px 12px
				.icon
					display:inline-block
				.text
					display:table-cell
					width:56px
					vertical-align:middle
					border-1px(rgba(7,17,27,.2))
					font-size:12px
		.foods-wrapper
			flex:1
			background:#fff
			.title
				padding-left:14px
				height:26px
				line-height:26px
				border-left:2px solid #d9dde1                    //#d9dde1
				font-size:12px
				color:rgb(147,153,159)
				background:#f3f5f7
			.food-item
				display:flex
				margin:18px
				padding-bottom:18px
				border-1px(rgba(7,17,27,.2))
				&:last-child
					border-none()
					margin-bottom:0px
				.icon
					flex:0 0 57px
					width:57px
					margin-right:10px
				.content
					flex:1
					.name
						margin:2px 0px 8px
						height:14px
						line-height:14px
						font-size:14px
						color:rgb(7,17,27)
					.desc,.extra
						line-height:10px
						font-size:10px
						color:rgb(147,153,159)
					.desc
						margin-bottom:8px
						line-height:12px
					.extra
						.count
							margin-right:12px
					.price
						font-weight:700
						line-height:24px
						.nprice
							margin-right:18px
							font-size:14px
							color:rgb(240,20,20)
							.symbol
								font-size:10px
								font-weight:normal
						.oprice
							font-size:10px
							text-decoration:line-through
							color:rgb(147,153,159)
						
</style>
