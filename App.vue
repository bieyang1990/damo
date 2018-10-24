<template>
  <div id="app">
  	<!--<div class="top">
  		<div class="time"><img src="./assets/img/考试_01.jpg" alt="" /></div>
  		<div class="head">
  			<span class="licon"><img src="./assets/img/考试_04.jpg" alt="" /></span>
  			<h1>小巷麻辣香锅（西三旗店）</h1>
  			<span class="ricon"><img src="./assets/img/分享.jpg" alt="" /></span>
  		</div>
  		<div class="banner">
  			<img class="big" src="./assets/img/考试_07.jpg" alt="" />
  			<img  class="small" src="./assets/img/block.jpg" alt=""/>
  		</div>
  		<div class="title">
  			<h2>小巷麻辣香锅（西三旗店）</h2>
  			<h3>4.7  月售3407单   蜂鸟快送   约46分钟   距离3.4km</h3>
  			<h4>欢迎光临，用餐高峰期请提前下单，谢谢</h4>
  			<h5><span>满减</span> 满35减21 ，满66减30，满100减40 <i>4个优惠</i></h5>
  		</div>
  	</div>-->
  	<div class="nav">
  		<ul>
  			<li><router-link to='/food'>点餐</router-link></li>
  			<li><router-link to='/recommend'>评价</router-link></li>
  			<li><router-link to='/shop'>商家</router-link></li>
  		</ul>
  	</div>
    <router-view @sendprice='fn'/>
    <div class="footer" :class="hasgood">
    	<ul v-show="cartShow"><!--弹窗-->
    		<li v-for="(val,ind) in goodList" :key='ind'>
    			<p>商品:{{val.title}}</p>
    			<span>小计：￥{{val.price*val.num}}</span>
    			<i>数量：{{val.num}}</i>
    		</li>
    	</ul>
    	<div class="cart" @click="showCart"><div class="num" v-show='howmany'>{{howmany}}</div><img src="./assets/img/cart.png" alt="" /></div>
    	<p class="price">￥{{sum}}</p>
    	<div class="btn">{{btnwd}}</div>
    	
    </div>
  </div>
</template>

<script>
	
	
//	这是第一个
	
	
export default {
  name: 'App',
  data(){
  	return {
  		sum:0,
  		btnwd:'￥20起送',
  		hasgood:'',
  		dataList:[],
  		cartShow:false,
  		goodList:[]
  	}
  },
  methods:{
  	fn(data){
  		this.dataList=JSON.parse(data);
  		console.log('app',this.dataList)
  		this.goodList=this.dataList.filter((ele,ind)=>{
  			return ele.num==0?false:true;
  		})
			var sum=0;
  		this.dataList.forEach((ele,ind)=>{
  			sum+=ele.price*ele.num;
  		})
  		this.sum=sum;
  	},
  	showCart(){
  		this.cartShow=!this.cartShow;
  	}
  },
  watch:{
  	sum(newval,oldval){
  		console.log(newval,'new')
  		this.btnwd=newval==0?"￥20起送":"去结算"
  		this.hasgood=newval===0?'':'has';
  	}
  },
  computed:{
  	howmany(){
  		var num=0;
  		this.dataList.forEach((ele,ind)=>{
  			num+=ele.num;
  		})
  		return num;
  	}
  }
}
</script>

<style>
img{
	display: block;
}
#app {
  width: 100%;
  height: 100%;
  position: relative;
}

/*区域一布局*/
#app .top{
	height: 4.4rem;
	border-bottom: 1px solid #ccc;
}
#app .top .time{
	height: 0.35rem;
}
#app .top .time img{
	width: 100%;
	height: 0.35rem;
}
/*区域一头部*/
#app .head{
	height: 0.7rem;
	border-bottom: 1px solid #ccc ;
	display: flex;
	justify-content: space-between;
	align-items: center;
}
#app .head span.licon img{
	width:0.25rem ;
	height: 0.25rem;
	margin-left: 0.2rem;
}
#app .head h1{
	flex: 1;
	font-size:0.24rem ;
	text-align: center;
}
#app .head span.ricon img{
	width:0.33rem ;
	height: 0.33rem;
	margin-right: 0.2rem;
}
/*区域一轮播*/
#app .top .banner{
	height: 1.4rem;
	position: relative;
}
#app .top .banner .big{
	width:100%;
	height: 1.4rem;
}
#app .top .banner .small{
	width: 0.94rem;
	height: 0.94rem;
	position: absolute;
	top:0.77rem ;
	left: 2.15rem;
}

/*区域一很多文字*/
#app .top .title h2{
	font-size: 0.3rem;
	font-weight: bold;
	text-align: center;
	margin-top:0.3rem ;
	height: 0.6rem;
	line-height: 0.6rem;
}
#app .top .title h3{
	font-size: 0.14rem;
	text-align: center;
	line-height: 0.3rem;
}
#app .top .title h4{
	color: #999999;
	font-size: 0.14rem;
	text-align: center;
	line-height: 0.3rem;
}
#app .top .title h5{
	color: #666;
	font-size: 0.16rem;
	text-align: center;
	line-height: 0.5rem;
}
#app .top .title h5 span{
	display: inline-block;
	width: 0.4rem;
	height: .2rem;
	background: #f07373;
	border-radius: 0.02rem;
	color: #fff;
	text-align: center;
	line-height: 0.2rem;
	float: left;
	margin-left:0.5rem ;
	margin-top: 0.15rem;
}
#app .top .title h5 i{
	float: right;
	margin-right:0.5rem ;
}

</style>
<style>
/*导航部分*/
#app .nav{
	height: 0.6rem;
	width: 100%;
}
#app .nav ul{
	width: 100%;
	height: 0.6rem;
	display: flex;
}
#app .nav ul li{
	flex: 1;
	text-align: center;
}
#app .nav ul li a{
	display: inline-block;
	font-size: 0.2rem;
	color: #676767;
	height: 0.56rem;
	border-bottom: 3px solid transparent;
	line-height: 0.6rem;
}
#app .nav ul li a.active{
	color: #000;
	font-weight: bold;
	border-bottom-color:#2395ff ;
}
</style>
<style>
/*底部*/
.footer{
	width: 100%;
	height: 0.7rem;
	background: rgba(0,0,0,0.5);
	position: fixed;
	bottom: 0;
	left: 0;
	
}
.footer .cart{
	width: 0.7rem;
	height: 0.7rem;
	background: #363636;
	border-radius: 50%;
	position: absolute;
	top: -0.1rem;
	left: 0.2rem;
	display: flex;
	justify-content: center;
	align-items: center;
}
.footer .cart img{
	width: 0.33rem;
	height: 0.33rem;
}
.footer p.price{
	font-size: 0.25rem;
	color: #fff;
	line-height: 0.6rem;
	margin-left: 1rem;
}
.footer .btn{
	width: 1.5rem;
	height: 0.7rem;
	background: #535356;
	color: #fff;
	font-weight:bold ;
	text-align: center;
	font-size: 0.2rem;
	line-height: 0.7rem;
	position: absolute;
	top: 0;
	right:0;
}
.footer.has .cart{
	background:#2395ff ;
}
.footer.has .btn{
	background: #4cd964;
}
.footer ul{
	width: 100%;
	background:rgba(255,255,255,0.8);
	position: fixed;
	bottom: 0.7rem;
}
.footer ul li{
	height: 0.9rem;
	border-bottom: 1px dotted #000;
	display: flex;
	align-items: center;
}
.footer ul li p{
	font-size: 0.22rem;
	color: #666;
	margin-left: 0.2rem;
}
.footer ul li span{
	flex: 1;
	text-align: end;
	margin-right: .2rem;
	font-size: .18rem;
	color: #ff6a07;
	font-weight: bold;
}
.footer ul li i{
	font-size: .16rem;
	color: #ccc;
	font-weight: bold;
	margin-right: 0.2rem;
}
.footer .cart .num{
	width: 0.24rem;
	height: 0.18rem;
	border-radius: 0.08rem;
	font-size: 0.12rem;
	background: #ff4615;
	color: #fff;
	text-align: center;
	line-height: 0.18rem;
	position: absolute;
	top: 0;
	right: 0;
}
</style>