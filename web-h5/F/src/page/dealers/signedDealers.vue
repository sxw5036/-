<template>
	<div id="dealers">
	<div id="pullrefresh" class="mui-content mui-scroll-wrapper">
	<div class="mui-scroll">
       <div>
	  		   <div class="after_bg">
	  			  <div style="padding: 0.5rem 0.5rem;">
	  				  				    <div style="width:42%;  float: left; color: #FFFFFF; margin-top: 0.4rem; ">
	  				  						<div style="width: 14%; float: left; "><img style="width: 100%; margin-left: 0;" src="../../assets/img/aftersale/tongji_tu.png" /></div>
	  				  						<div  style="width: 60%; float: left;  font-size: 0.9rem; margin-top: 0.1rem; margin-left: 0.6rem;">今日统计</div>
	  				  						<div class="clearfix"></div>
	  				  				   </div> 
	  				  				    <div style="width:50%;  float: right; " class="get_tjt" @click="get_tjt">
	  				  						<div  style="width: 90%; float: left; color:rgba(255,255,255,0.6); font-size: 0.7rem; margin-top: 0.4rem;  text-align: right;">更多统计</div>
	  				  						<div style="width: 0.3rem; float: right; margin-top: 0.4rem; "><img style="width: 100%;" src="../../assets/img/aftersale/left_arrow.png" /></div>
	  				  						<div class="clearfix"></div>
	  				  				   </div> 
	  				  				   <div class="clearfix"></div>
	  			</div> 
	  				 <div>
	  					<ul class="signdeal" >
	  						<li v-for="item in countNum">
	  							<p>{{item.value}}</p>
	  							<div >{{item.name}}</div>
	  						</li>
	  					
	  					</ul>
	  					 
	  				 </div>
	  		   </div>
	  </div>
	   <div style="padding: 0.5rem;">
	   		  <div class="after_js">
	   		  	   			   <div class="aftersale_js">
	   		  					    <div style="width:8%; float: left;"><img style="width: 100%;" src="../../assets/img/aftersale/af_js.png" /></div> 
	   		  					    <div style="width: 40%; float: left; margin-left: 0.4rem; font-size: 0.9rem; margin-top: 0.2rem;">检索</div>
	   		  					   <div class="clearfix"></div>
	   		  				   </div>
	   		  				   <div class="after_inputs">
	   		  					  
	   		  					   <div class="intent_select">
	   		  						   <input class="intent_p" :readonly="readonly" type="text" v-model="searchObj.cityIdName" @click="addsiteshow=!addsiteshow" placeholder="选择地区"> 
	   		  						    
	   		  						   </input>
	   		  						   <img class="intent_icon" style="width: 0.7rem;" src="../../assets/img/dealer/left_ar.png"/>
	   		  					   </div>
	   		  					   <div style="margin-bottom: 0.5rem;">
	   		  					  						  <div style="float: left;width: 48%;margin-right: 4%; color:#a4a4a4;  height: 2rem; border-radius: 0.25rem; border:1px #d5d5d5 solid; box-sizing: border-box;position: relative;">
	   		  					  						     <select style="width:80%;font-size: 0.7rem; padding: 0; margin-left: 0.4rem; margin-top: 0.4rem;" v-model="type_intent"  >	
	   		  					  						  		    <option disabled value="">请选择类型</option>
	   		  					  						  			<option  v-for="item in typesobj" :value="item.value"  :key="item.value" style="font-size: 0.7rem;">{{ item.label }}</option>						  
	   		  					  						     </select>
	   		  					  							 <span style="position:absolute ;top:0.4rem;left:80%;"><img style="width: 0.7rem;" src="../../assets/img/dealer/left_ar.png"/></span>
	   		  					  						  </div>
	   		  					  						   <div style="float: left;width: 48%; color:#a4a4a4;  height: 2rem; border-radius: 0.25rem; border:1px #d5d5d5 solid ;box-sizing: border-box; position: relative;">
	   		  					  						      <select style="width:80%;font-size: 0.7rem; padding: 0; margin-left: 0.4rem; margin-top: 0.4rem;" v-model="status_intent">
																        <option disabled value="">请选择状态</option>
	   		  					  						   		  		<option  v-for="item in typesstatus" :value="item.value" :key="item.value" style="font-size: 0.7rem;">{{ item.label }}</option>						  
	   		  					  						      </select>
	   		  					  							  <span style="position:absolute ;top:0.4rem;left:80%;"><img style="width: 0.7rem;" src="../../assets/img/dealer/left_ar.png"/></span>
	   		  					  						   </div>
	   		  					  						   <div class="clearfix"></div>
	   		  					  </div>
	   		  					   
	   		  				   </div>
	   		  				    <div @click="getsearchdealerdatas" class="check_more">查询</div>
	   		  </div>
	   </div>
	   <div style="padding:0 0.5rem">
		   <div style="background-color: white; border-radius:0.25rem; padding:0.5rem 0">
			  <ul class="mui-table-view">
					<li class="mui-table-view-cell" v-for="item in dealerLists" @click="changePath(item.id)">
						<a class="mui-navigate-right">
							<div>
								<div style=" color: #a7a7a7 ">
									  <p style="float: left; font-size: 0.6rem;margin-left:0.2rem;">&nbsp{{item.companyName}}</p>
									  <p style="font-size: 0.6rem; color: red;float: right; margin-right: 1.2rem;">&nbsp{{item.statusName}}</p>
									  <div class="clearfix"></div>
								</div>
								<ul class="mui_ul_li">
									<li style=" float: left; color: #bdb08a;margin-left:0.2rem;">&nbsp{{item.leaderName}}【{{item.typeName}}】</li>
									<li style=" float: right; color: black;text-align: right;padding-right:1.2rem;">&nbsp{{item.dealerMobile}}</li>
									<li style=" float: left;font-size: 0.6rem;margin-bottom: 0.3rem;margin-left: 0.4rem;">渠道经理：&nbsp{{item.businessManagerName}}</li>
									<li style=" float: right;text-align: right;padding-right:1rem; margin-bottom: 0.3rem;font-size: 0.6rem; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">&nbsp{{item.mergerName}}</li>
									<div class="clearfix"></div>
								</ul>
							</div>
						</a>
					</li>				
				</ul>
		   </div>
		   
	   </div>
	   <div class="new_dealer"  @click="newsdealer()"> 新建经销商</div>
	   </div>
	   </div>
	   <Address :show="addsiteshow" @sure='surreAddress' @cancel="addsiteshow=!addsiteshow"></Address>
		
	</div>
	
</template>

<script>
	import address from '@/components/address'
	import mui from '../../assets/js/mui.js'
	export default {
		name: 'dealers',

		data() {

			return {
				 readonly:true,
                 dealerLists:[],
                  pageSize: 10,
                  pageNum: 0,
                  totalpage: 0,
                  currents: 1,
                 countNum:[],
				 status_intent:'',
				 type_intent:'',
				 
				 addsiteshow: false,
				 searchObj: {
				 	startTime: "",
				 	endTime: "",
				 	cityId:"",
				 	cityIdName:"",
				 	condation:"",
				 	dealerId:""
				 
				 },
				 typesobj:[
				 					 //  {
				 						// 	value: "0",
				 						// 	label: '请选择类型'
				 						// },
				 					   {
				 					   		value: "1",
				 					   		label: '直营店'
				 					   	},
				 					   	{
				 					   		value: "2",
				 					   		label: '店中店'
				 					   	},
				 						{
				 							value: "3",
				 							label: '专卖店'
				 						},
				 						{
				 							value: "4",
				 							label: '加盟店'
				 						},
				 						
				 ],
				 typesstatus:[
				 					 //   {
				 						// 	 
				 						// 	value: "0",
				 						// 	label: '请选择状态'
				 						// },
				 					   {
				 					   		value: "0",
				 					   		label: '意向经销商'
				 					   	},
				 					   	{
				 					   		value: "1",
				 					   		label: '签约经销商'
				 					   	},
				 						
				 						
				 						
				 ],
				
			}

		},

	      components: {
	     
	     	Address: address
	     
	     },
		methods: {
			/**
			 * 下拉刷新具体业务实现
			 */
			pulldownRefresh: function() {
			this.currents=1;
			mui('#pullrefresh').pullRefresh().endPulldownToRefresh();
			this.getsigndealerdatas()
			},
			/**
			 * 上拉加载具体业务实现
			 */
			
			pullupRefresh: function() {
			
			 this.currents++;
			 
			 console.log(this.currents,this.totalpage)
			 
			  let that = this;
			    this.axios({
			 	method: 'get',
			 	headers: {
			 		'X-Requested-With': 'XMLHttpRequest',
			 		'ContentType': 'application/json;charset=UTF-8'
			 	},
			 	url: '/wxapi/f/branchs/dealers?status0=1'+ '&pageNum=' + that.currents + '&pageSize=' + that.pageSize,
			 		}).then(res => {
			 			   that.mui('#pullrefresh').pullRefresh().endPullupToRefresh((that.currents > that.totalpage)); 
			 			   console.log(res)
			 		       var data=res.data.data.companyDto;

			 		       for (var i=0;i<data.length;i++){
			 		       that.dealerLists.push(data[i]);
			 		      } 
			 			  var countdata=res.data.data.count;
			 			  that.countNum=countdata;
			 			 
			 			  that.pageSize = res.data.pagination.pageSize;
			 			  that.pageNum = res.data.pagination.pageNum;
			 			  that.totalpage = res.data.pagination.pages;
			 	  
			 		 })
			 	},
			//三级联动
			surreAddress: function(obj) {
				console.log(obj)
				this.addsiteObj = obj;
				this.searchObj.cityId=obj.id;
				this.searchObj.cityIdName=obj.name
				this.addsiteshow = !this.addsiteshow
			},
			newsdealer:function  () {
				
				this.$router.push({ name: 'newDealers'})
				
			},
			get_tjt:function(){
				this.$router.push({ name: 'dealer_report'})
			},
			changePath:function  (id) {
				
				this.$router.push({ name: 'dealerdep', query: { id:id }})
				
			},
			
				getsigndealerdatas(){			
				   let that = this;
				   this.axios({
					method: 'get',
					headers: {
						'X-Requested-With': 'XMLHttpRequest',
						'ContentType': 'application/json;charset=UTF-8'
					},
					url: '/wxapi/f/branchs/dealers?status0=1'+ '&pageNum=' + that.currents + '&pageSize=' + that.pageSize,
				}).then(res => {
					   mui('#pullrefresh').pullRefresh().endPulldownToRefresh(); //refresh completed
					   console.log(res)
				       var data=res.data.data.companyDto;
					   that.dealerLists=[];
				       for (var i=0;i<data.length;i++){
				         that.dealerLists.push(data[i]);
				      } 
					 
					  var countdata=res.data.data.count;
					
					  that.countNum=countdata;
					 
					  that.pageSize = res.data.pagination.pageSize;
					  that.pageNum = res.data.pagination.pageNum;
					  that.totalpage = res.data.pagination.pages;
			  
				 })
			},
				getsearchdealerdatas(){			
				   let that = this;
				   that.pageSize = "";
				   that.pageNum="";
				   that.totalpage="";
				   that.currents= 1;
				   this.axios({
					method: 'get',
					headers: {
						'X-Requested-With': 'XMLHttpRequest',
						'ContentType': 'application/json;charset=UTF-8'
					},
					url: '/wxapi/f/branchs/dealers?status0=1'+(that.status_intent == '' ? '' : '&status1=' + that.status_intent)+(that.type_intent == '' ? '' : '&type=' + that.type_intent)+(that.searchObj.cityId == '' ? '' : '&cityId=' + that.searchObj.cityId)+ '&pageNum=' + that.currents + '&pageSize=' + that.pageSize,
				}).then(res => {
					   // mui('#pullrefresh').pullRefresh().endPulldownToRefresh(); //refresh completed
					   console.log(res)
				       var data=res.data.data.companyDto;
					   that.dealerLists=[];
				       for (var i=0;i<data.length;i++){
				         that.dealerLists.push(data[i]);
				      } 
					  that.pageSize = res.data.pagination.pageSize;
					  that.pageNum = res.data.pagination.pageNum;
					  that.totalpage = res.data.pagination.pages;
			  
				 })
			},
			
			 
		},
		mounted: function() {
		   this.getsigndealerdatas();
		   var that = this
		   mui.init({
		   	pullRefresh: {
		   		container: '#pullrefresh',
		   		down: {
		   			style:'circle',
		   			callback: that.pulldownRefresh
		   		},
		   		up: {
		   			contentrefresh: '正在加载...',
		   			callback: that.pullupRefresh
		   		}
		   	}
		   })
		   mui("#pullrefresh").on('tap', 'li', function (event) {
		           this.click();
		       });
			     mui("#pullrefresh").on('tap', '.new_dealer', function (event) {
			           this.click();
			       });
                      mui("#pullrefresh").on('tap', '.check_more', function (event) {
                          this.click();
                      });
					   mui("#pullrefresh").on('tap', '.get_tjt', function (event) {
					      this.click();
					  });
                    
		},
		created: function() {
			
			for(var i = mui.hooks.inits.length - 1, item; i >= 0; i--) {
		
				item = mui.hooks.inits[i];
				if(item.name == "pullrefresh") {
					item.repeat = true;
				}
			}
		
		}
		
		

	}
	
</script>

<style scoped="scoped">
	 ul li {

            margin: 0;
            padding: 0;
            list-style: none;
        }
     
		.clearfix{
			clear: both;
		}
		.after_bg{
			width: 100%;
			height: auto;
              background-image: url(../../assets/img/dealer/dearer_bg.png);
			  background-size: 100% 100%;
			  border-radius: 0.25rem;
			  padding: 0.5rem 0.5rem;
			  height: 9rem;
			  margin-bottom: -1rem;
			  margin-top: -0.5rem;
		}
		.after_js{
			background-color: white;
			border-radius: 0.25rem;
			padding: 0.5rem 0.5rem;
		}
		.after_inputs{
			margin-top: 0.5rem;
		}
		.after_inputs input{
			border-radius: 0.25rem; height: 2rem; text-align: center; color: #a4a4a4;
		}
		.mui-table-view-cell.mui-active{
			background-color: #0062CC;
		}
		.mui-table-view-cell{
			padding: 0.5rem;
			margin-left: 0.4rem;
			
		}
		.mui_ul_li li{
			width: 48%;
			margin-top: 0.5rem;
			color: #a4a4a4;
		}
	.new_dealer{
		width: 100%;
		margin-top: 0.5rem;
		background-image:url(../../assets/img/dealer/dearer_but_new.png);
		background-size: 100% 100%;
		background-repeat:no-repeat;
		text-align: center;
		line-height: 2.2rem;
		height: 2.2rem;
		color: black;
		font-size: 0.6rem;
		padding-left: 1rem;
		
			
	}
		.mui-table-view:before{
			height: 0px;
		}
		.mui-table-view:after{
			height: 0px;
		}
		.check_more{
			width: 100%;
			text-align: center;
			line-height: 2rem;
			height: 2rem;
			color: white;
			font-size: 0.7rem;
			background-image:url(../../assets/img/dealer/dearer_but_bg.png);
			background-size: 100% 100%;
			background-repeat:no-repeat;
		}
	
		.signdeal li{
			width: 32%; 
			border-right: 0.05rem solid rgba(182,188,206,0.5);
			box-sizing: border-box;
			display: inline-block;
		}
		.signdeal li:last-child{
		    border-right: none;		
		}
		.signdeal li p{
			font-size:1rem; text-align: center; color: white; margin-top: 0.9rem;
		}
		.signdeal li div{
			text-align: center;margin-bottom: 0.8rem; font-size: 0.6rem;color:rgba(255,255,255,0.5);
		}
		.intent_select{
			height: 2rem;
			width: 100%;
			border-radius:10px;
			margin-bottom: 0.5rem;
			position: relative;
		}
		.intent_p{
			width: 100%;
			height: 100%;
			font-size: 0.8rem;
			padding: 0.6rem;
			text-align: center;
			
		}
		.intent_icon{
			display: block;
			position:absolute;
			top:0.8rem;
			left:80%;
		}
		.mui-content{
			padding: 0;
		}
</style>