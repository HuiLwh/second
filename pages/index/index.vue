<template>
	<view class="content">
		<view class="status_bar">
		           <!-- 这里是状态栏 -->
		 </view>
		<view class="nav" v-for="item in navbar">
			<text class="nav-item">
				{{item}}
			</text>
		</view>
		<view class="ke-box" >			<view class="ke-item" v-for="item in data">
				<image :src="item.src" mode="widthFix"></image>
				<p class="num">
					 <span>73人学习</span> ·
					 <span>新上好课</span>			
				 </p>
				 <p class="price">
					 <span class="discount-price"><sub>￥</sub>{{item.price[0]}}</span>
					<span class="original"><sub>￥</sub>{{item.price[1]}}</</span>
				 </p>
				 <p class="discount">
					<span class="name">{{item.tag}}</span>                
				</p>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				h5:true,
				navbar:["全部","零基础","进阶课"],
				data:[]
			}
		},
		onLoad() {
			this.getdat()
			// #ifdef H5
			this.h5 = true
			// #endif 
			// #ifndef H5
			this.h5 = false
			// #endif
			
		},
		methods: {
			getdat(){
				uni.request({
					url:"http://localhost:3000/data",
					success(res) {
						console.log(res)
						 this.data = res.data
						console.log(this.data)
					}
					
				})
			}
		}
	}
</script>

<style lang="scss">
	*{
		margin: 0;
		padding: 0;
	}
	
	.content{
		.status_bar {
		       height: var(--status-bar-height);
		       width: 100%;
		   }
		
		
		width: 750rpx;
		background-color: #71777D;
		.nav{
			display: flex;
			// height: 37rpx;
			// line-height: 37rpx;
			
			align-items: center;
			.nav-item{
				margin: 5rpx;
			}
			
		}
		.ke-box{
			.ke-item{
				.num {
				    color: #71777D;
				    font-size: .29333333rem;
				    margin-bottom: 0.21333333rem;
				}
				.price{
					 .discount-price {
					    font-weight: 700;
					    color: #F01414;
					    font-size: .42666667rem;
					}
					 .original {
					    text-decoration: line-through;
					    color: #B7BBBF;
					    margin-left: 0.13333333rem;
					}
				}
				 .discount .name {
				    display: inline-block;
				    color: #F01414;
				    border: 1px solid #F01414;
				    border-radius: 2px;
				    padding: 0rem 0.10666667rem;
				    font-size: .24rem;
				    line-height: .37333333rem;
				}
			}
		}
	}
	
</style>
