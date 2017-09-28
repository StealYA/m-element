<template>
	<div class="header">
		<div class="background">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>
		<div class="content-wrapper">
			<div class="avatar">
				<img :src="seller.avatar" width="64" height="64" alt="" class="avatar-pic">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div class="supports" v-if="seller.supports">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{seller.supports[0].description}}</span>
				</div>
				<div class="supports-count" v-if="seller.supports" @click="showDetail">
					<span class="count">{{seller.supports.length}}个</span>
					<i class="icon-keyboard_arrow_right"></i>
				</div>
			</div>
		</div>
		<div class="bulletin-wrapper" @click="showDetail">
			<span class="bulletin-title"></span>
			<span class="bulletin-txt">{{seller.bulletin}}</span>
			<i class="icon-keyboard_arrow_right"</i>
		</div>
		<div v-show="detailShow" class="detail">
			<div class="detail-wrapper clearfix">
				<div class="detail-main">
					<h1 class="name">{{seller.name}}</h1>
					<div class="star-wrapper">
						<star :size="48" :score="seller.score"></star>
					</div>
					<div class="title">
						<div class="line"></div>
						<div class="text">优惠信息</div>
						<div class="line"></div>
					</div>
					<ul class="supports" v-if="seller.supports">
						<li class="supports-item" v-for="(item,$index) in seller.supports">
							<span class="icon" :class="classMap[$index]"></span>
							<span class="text">{{item.description}}</span>
						</li>
					</ul>
					<div class="title">
						<div class="line"></div>
						<div class="text">商家信息</div>
						<div class="line"></div>
					</div>
					<div class="seller-bulletin">{{seller.bulletin}}</div>
				</div>
			</div>
			<div class="detail-close">
				<i class="icon-close" @click="closeDetail"></i>
			</div>
		</div>
	</div>
</template>

<script>
	import star from "../../components/star/star";

	export default {
		props : {
			seller : Object
		},
		data() {
			return {
				detailShow : false
			}
		},
		methods : {
			showDetail : function() {
				this.detailShow = true;
			},
			closeDetail : function() {
				this.detailShow = false;
			}
		},
		created() {
			this.classMap = ['decrease','discount','special','invoive','guarantee'];
		},
		components : {
			'star' : star
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"
	
	.header
		position:relative
		overflow:hidden
		color:#fff
		background:rgba(7,17,27,.5)
		.background
			position:absolute
			top:0px
			left:0px
			width:100%
			height:100%
			z-index:-1
			filter:blur(10px)
		.content-wrapper
			position:relative
			padding:24px 12px 18px 24px
			font-size:0px
			.avatar
				display:inline-block
				vertical-align:top
				.avatar-pic
					border-radius:4px
			.content
				display:inline-block
				margin-left:16px
				.title
					margin:2px 0px 8px 0px
					.brand
						display:inline-block
						vertical-align:top
						width:30px
						height:18px
						bg-img('brand')
						background-size:30px 18px
					.name
						margin-left:6px
						font-size:16px
						font-weight:bold
				.description
					margin-bottom:10px
					line-height:12px
					font-size:12px
				.supports
					.icon
						display:inline-block
						vertical-align:top
						width:12px
						height:12px
						margin-right:4px
						background-size:12px 12px
						&.decrease
							bg-img('decrease_1')
						&.discount
							bg-img('discount_1')
						&.guarantee
							bg-img('guarantee_1')
						&.invoive
							bg-img('invoice_1')
						&.special
							bg-img('special_1')
					.text
						font-size:10px
						line-height:12px
				.supports-count
					position:absolute
					right:12px
					bottom:14px
					padding:0px 8px
					height:24px
					line-height:24px
					border-radius:14px
					background:rgba(0,0,0,0.2)
					text-align:center
					.count
						vertical-align:top
						font-size:10px
					.icon-keyboard_arrow_right
						margin-left:2px
						line-height:24px
						font-size:10px
		.bulletin-wrapper
			position:relative
			height:28px
			line-height:28px
			padding:0px 22px 0px 12px
			white-space:nowrap
			overflow:hidden
			text-overflow:ellipsis
			background:rgba(7,17,27,.2)
			.bulletin-title
				display:inline-block
				vertical-align:middle
				width:22px
				height:12px
				bg-img('bulletin')
				background-size:22px 12px
			.bulletin-txt
				vertical-align:middle
				font-size:10px
				margin-right:4px
			.icon-keyboard_arrow_right
				position:absolute
				right:12px
				top:10px
				font-size:10px
		.detail
			position:fixed
			top:0px
			left:0px
			z-index:100
			width:100%
			height:100%
			overflow:auto
			background:rgba(7,17,27,.8)
			.detail-wrapper
				width:100%
				min-height:100%
				.detail-main
					margin-top:64px
					padding-bottom:64px
					.name
						line-height:16px
						text-align:center
						font-size:16px
						font-weight:700
					.star-wrapper
						margin-top:16px
						padding:2px 0px
						text-align:center
					.title
						display:flex
						width:80%
						margin:28px auto 24px
						.line
							flex:1
							position:relative
							top:-6px
							border-bottom:1px solid rgba(255,255,255,.2)
						.text
							padding:0px 12px
							line-height:14px
							font-size:14px
							font-weight:700
					.supports
						width:72%
						margin:0px auto
						.supports-item
							margin-bottom:12px
							.icon
								display:inline-block
								vertical-align:top
								width:16px
								height:16px
								margin-right:6px
								background-size:16px 16px
								&.decrease
									bg-img('decrease_2')
								&.discount
									bg-img('discount_2')
								&.guarantee
									bg-img('guarantee_2')
								&.invoive
									bg-img('invoice_2')
								&.special
									bg-img('special_2')
							.text
								font-size:12px
								line-height:12px						
					.seller-bulletin
						width:72%
						line-height:24px
						margin:0px auto
						font-size:12px
			.detail-close
				position:relative
				width:32px
				height:32px
				margin:-64px auto 0px auto
				font-size:32px
				.icon-close
					position:absolute
					top:0px
					left:0px
					font-size:32px
						
</style>