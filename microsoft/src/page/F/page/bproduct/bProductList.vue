<template>
	<div id="bProductList">
		<!-- <header  class="mui-bar mui-bar-nav " data-top='0' data-offset='150' data-duration='16' data-scrollby=".mui-scroll-wrapper">
					
					<a class="mui-action-back mui-icon mui-icon-back mui-pull-left"></a>
			<h1 class="mui-title">产品列表</h1>
		</header>
		<div style="width: 100%; height: 2.1rem;">
			
		</div> -->
		<ul>
			<li v-for=" (list,index) in productList" :key="index">
			<router-link :to="{name:'FbProductDetails',query:{id:list.id}}">
				<a>
					<img src="../../assets/img/bproduct/productListImg.png" style="margin-left: 0.5rem; ">
					<div style="padding-left: 0.2rem;">
						<p class="ppp1">{{list.name}}</p>
						<p class="ppp2" style="margin-bottom: 0;padding-top: 0.5rem;">
							<span class="sa1">类别: <span class="s22">{{list.categoryName}}</span> </span> <span class="s3">台面材质: <span class="s4">{{list.productMaterial}}</span>
							</span>
						</p>
						<p class="ppp3">
							<span class="sa1">风格: <span>{{list.series}}</span> </span>
						</p>
					</div>
				</a>
				</router-link>
			</li>
		</ul>
	</div>
</template>

<script>
	import mui from '@/assets/js/mui.js'
	export default {
		name: 'bProductList',

		data() {

			return {
				productList:[]
			}

		},


		methods: {

		},
		mounted: function() {
				var that=this
				 
					this.axios({
					method: 'get',
					
					url: '/wxapi/f/products'
				
				}).then(function(res) {
					
					console.log(res.data.data)
					that.productList=res.data.data;
				
				}).catch(function(err) {
					console.log(err)
				
				})

		}
		/**/

	}
</script>

<style scoped="scoped">
	#bProductList {
		width: 100%;
		height: 100%;
		
		background-color: white;
	}

	#bProductList>ul>li {
		height: 5rem;
		padding-top: 0.55rem;
	}

	#bProductList>ul>li img {
		margin-left: 0.1rem;
		margin-top: 0.2rem;
		width: 3.5rem;
		height: 3.5rem;
		border-radius: 0.25rem;
		float: left;
	}
	#bProductList>ul>li:last-child div{
		border-bottom: none;
	}
	#bProductList>ul>li a>div {
		padding-left: 0.1rem;
		margin-left: 0.775rem;
		width: 12.1rem;
		height: 4.3rem;
		float: left;
		padding-bottom: 0.1rem;
		border-bottom: 0.025rem solid rgba(99, 99, 99, 0.3);
	}

	#bProductList>ul>li a>div>.ppp1 {
		text-overflow: ellipsis;
		width: 11.5rem;
		font-family: PingFang-SC-Medium;
		font-weight: 500;
		font-size: 0.725rem;
		margin-bottom: 0;
		color: rgba(51, 51, 51, 1);
		overflow: hidden;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
	}

	#bProductList>ul>li a>div .s22 {
		text-overflow: ellipsis;
		margin-right: 0.4rem;
		font-size: 0.575rem;
		color: rgba(99, 99, 99, 0.6);
		width: 3.375rem;
		display: inline-block;
	}

	#bProductList>ul>li a>div .ppp3 {
		padding-top: 0.5rem;
		margin-bottom: 0;
	}

	#bProductList>ul>li a>div span>span {
		text-overflow: ellipsis;
		font-size: 0.575rem;
		color: rgba(99, 99, 99, 0.6);
	}
</style>
