<template>
	<div class="maskCommunity" @touchmove.prevent>
		<div class="maskCommunity_content">
			<textarea ref="textarea" class="maskCommunity_content_textarea" name="content" placeholder="说两句..." autofocus="autofocus"></textarea>
	        <p>
	        	 <a href="javascript:;" class="maskCommunity_content_btn maskCommunity_content_cancel" v-on:click="maskCommunityCancel()" >取消</a>
	        	 <a href="javascript:;" class="maskCommunity_content_btn maskCommunity_content_commit" @click="replyBtn()">发送</a>
	        </p>
	     	<p class="prompt" v-show="prompt">输入的内容不能为空！！</p>
		</div>
		
	</div>
</template>

<script>
	
	export default{
		props:{
			maskflage:{
				type:Boolean
			}
		},
		data(){
			return{
				flage:this.maskflage,
				prompt:false
			}
		},
		methods:{
			maskCommunityCancel(){
				this.closeMask()
			},
			replyBtn(){
				if(!this.$refs.textarea.value){
					this.prompt=true
					setTimeout(()=>{
						this.prompt=false
					},1000)
					return 
				}else{
					this.$emit("backmsg",this.$refs.textarea.value)
					this.closeMask()
					this.$refs.textarea.value=""
				}
				
			},
			//关闭显示框
			closeMask(){
				if(this.flage){
					this.flage=false
				}
				//向父级发送flage，表示要关掉弹出层，发送的是一个事件
				this.$emit("backMaskflage",this.flage)
			}
		}
	}
</script>

<style scoped="scoped">
	.maskCommunity{
		width: 100%;
		min-height: 100%;
		position: fixed;
		top: 0;
		left: 0;
		background: rgba(0,0,0,0.5);
		z-index: 100;
	}
	.maskCommunity_content{
		position: fixed;
	    z-index: 999;
	    width: 100%;
	    left: 0;
	    top: 50%;
	    
	    background: #ffffff;
	    padding: 0.25rem 0.2rem;
	    max-width: 640px;
	    margin:-30% auto 0;
	}
	.maskCommunity_content_textarea{
		    width: 100%;
		    min-height: 1.2rem;
		    outline: none;
		    resize: none;
		    border: 0.01rem #d6d6d6 solid;
		    color: #202020;
		    background: #f4f4f4;
		    font-size: 0.15rem;
		    padding: 0.1rem;
	}
	.maskCommunity_content_btn{
		width: 0.9rem;
	    height: 0.3rem;
	    line-height: 0.3rem;
	    text-align: center;
	    font-size: 0.15rem;
	    color: #ffffff;
	    margin-top: 0.1rem;
	}
	.maskCommunity_content_cancel{
		    float: left;
   		 background: #c5c5c5;
	}
	.maskCommunity_content_commit{
		   float: right;
    		background: #ff7e19;
	}
	.prompt{
		font-size: 0.14rem;
		line-height: 0.3rem;
		color: #fff;
		text-align: center;
		width: 50%;
		background: #202020;
		position: absolute;
		top: 30%;
		left: 50%;
		transform: translate(-50%,0);
	}
</style>