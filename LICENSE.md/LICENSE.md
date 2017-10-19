<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			* {
				margin: 0;
				padding: 0;
				
			}
			
			body {
				padding: 50px;
			}
			
			.clearfix:after {
				content: "\20";
				clear: both;
				display: block;
				height: 0;
				font-size: 0;
			}
			.left{
				float: left;
			}
			.spic {
				width: 300px;
				height: 300px;
				border: 1px solid chartreuse;				
				margin-right: 10px;
				position: relative;
			}
			
			.spic img {
				width: 300px;
				height: 300px;
			}
			
			.smallscale {
				background: rgba(0, 0, 255, 0.3);
				position: absolute;
				left: 0;
				top: 0;
				visibility: hidden;
				width: 100px;
				height: 100px;
			}
			
			.bpic {
				width: 400px;
				height: 400px;
				border: 1px solid chartreuse;
				float: left;
				overflow: hidden;
				position: relative;
				visibility: hidden;
			}
			
			#img1 {
				width: 600px;
				height: 600px;
				position: absolute;
				left: 0;
				top: 0;
			}
			.box{
				width: 300px;
				height: 56px;
				
				position: relative;				
				overflow: hidden;
				margin-top:25px ;								
			}			
			ul{
				list-style: none;				
				position: absolute;
				margin-left: 16px;												
			}
			ul li{
				width: 56px;
				height: 56px;
				float: left;
				
				padding-right: 6px;				
			}
			ul li img{
				width: 50px;
				height: 50px;
				display: block;				
				border: 1px solid #666666;				
			}			
			#left,#right{
				width: 10px;
				height: 52px;
				border: 1px solid #666666;
				line-height: 52px;
				background: #FFFFFF;
			}
			#left {
				position: absolute;
		        left: 0px;
		        top: 0px;
		        color: #333;
		        text-decoration: none;
		        z-index: 999;		        			
			}
			
			#right {
				position: absolute;
		        right: 0px;
		        top: 0px;
		        color: #333;
		        text-decoration: none;				
			}
		</style>
	</head>

	<body>
		<div class="wrap clearfix">
			<div class="left">
			<div class="spic">
				<img src="apple.jpg" />
				<div class="smallscale"></div>
			</div>
			
			<div class="box">
				<a href="javascript:;" id="left">&lt;</a>
				<ul>
					<li><img src="images/1.jpg"/></li>
					<li><img src="images/2.jpg"/></li>
					<li><img src="images/3.jpg"/></li>
					<li><img src="images/4.jpg"/></li>
					<li><img src="images/5.jpg"/></li>
					<li><img src="images/3.jpg"/></li>
					<li><img src="images/4.jpg"/></li>
					<li><img src="images/5.jpg"/></li>
					<li><img src="images/6.jpg"/></li>-->
				</ul>				
				<a href="javascript:;" id="right">&gt;</a>
			</div>
			</div>
			<div class="bpic">
				<img src="apple.jpg" id="img1" />
			</div>
		</div>
			<script src="public.js"></script>
			<script type="text/javascript">
					
						
						
						//2.3.小放大放消失
					//3.点击下方的图片，小图和大图显示下方的图片
					//4.点击箭头oUl移动
				function Zoom(){
					//1.获取元素
					var that=this;
					this.wrap = document.querySelector(".wrap");
					this.spic = document.querySelector(".spic");
					this.smallscale = document.querySelector(".smallscale");
					this.bpic = document.querySelector(".bpic");
					this.img1 = document.querySelector("#img1");						
					this.aLi=document.getElementsByTagName("li");
					this.left = document.querySelector("#left");
					this.right = document.querySelector("#right");
					
					//2.初始化
					this.init=function(){
						//2.1.显示小放
						this.spic.onmouseover=function(){
							that.show();
							that.scalesize();
							//2.2.小放大放移动，大图移动
							this.onmousemove=function(e){
								var e=e||window.event;
								that.smallscalemove(e);
							}
						}
						this.spic.onmouseout=function(){
							that.hide();
						}												
						this.spicimg=this.spic.getElementsByTagName("img")[0]
						for(var i=0;i<this.aLi.length;i++){
							this.aLi[i].onclick=function(){							
								that.spicimg.src=this.getElementsByTagName("img")[0].src;
								that.img1.src=this.getElementsByTagName("img")[0].src
							}
						}
						var num=5;
						this.right.onclick=function(){
							if(num<that.aLi.length){
								num++;
								if(num>that.aLi.length){
									this.right.style.disabled="none";
									
								}
							}
							that.oUl.style.left=-that.aLi[0].offsetWidth*(num-5)+"px";
						}
						this.left.onclick=function(){
							if(num>5){
								num--;
								if(num<=5){
									num=5;
									this.left.style.disabled="none";									
								}
							}
							that.oUl.style.left=-that.aLi[0].offsetWidth*(num-5)+"px";
						}
						
					}
					this.oUl=document.getElementsByTagName("ul")[0];
					this.oUl.style.width=this.aLi.length*this.aLi[0].offsetWidth+"px";
					
					this.Bright=function(){
						
					}
					
					this.show=function(){
						that.smallscale.style.visibility="visible";	
						that.bpic.style.visibility="visible";
					}
					this.hide=function(){
						that.smallscale.style.visibility="hidden";	
						that.bpic.style.visibility="hidden";
					}
					this.scalesize=function(){
						this.smallscale.style.width=this.spic.offsetWidth*this.bpic.offsetWidth/this.img1.offsetWidth+"px";
						this.smallscale.style.height=this.spic.offsetHeight*this.bpic.offsetHeight/this.img1.offsetHeight+"px";
					}
					this.smallscalemove=function(e){
						var x=e.clientX-this.spic.offsetLeft-this.smallscale.offsetWidth/2;
						var y=e.clientY-this.spic.offsetTop-this.smallscale.offsetHeight/2;
						if(x<0){
							x=0;
						}else if(x>this.spic.offsetWidth-this.smallscale.offsetWidth){
							x=this.spic.offsetWidth-this.smallscale.offsetWidth-2;
						}
						if(y<0){
							y=0;
						}else if(y>this.spic.offsetHeight-this.smallscale.offsetHeight){
							y=this.spic.offsetHeight-this.smallscale.offsetHeight-2;
						}
						this.smallscale.style.left=x+"px";
						this.smallscale.style.top=y+"px";
						this.img1.style.left=-this.img1.offsetWidth/this.spic.offsetWidth*x+"px";
						this.img1.style.top=-this.img1.offsetWidth/this.spic.offsetWidth*y+"px";			
					}
					
				}
				new Zoom().init();
			</script>
		</div>
	</body>

</html>
