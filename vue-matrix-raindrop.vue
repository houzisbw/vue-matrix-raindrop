<template>
    <canvas id="vue-matrix-raindrop"></canvas>
</template>

<script>
	export default {
		name: 'vue-matrix-raindrop',
    props:{
        canvasWidth:{
        	type:Number,
            default:800
        },
        canvasHeight:{
            type:Number,
            default:600
        },
        fontSize:{
        	type:Number,
            default:20
        },
        fontFamily:{
        	type:String,
            default:'arial'
        },
        textContent:{
        	type:String,
            default:'abcdefghijklmnopqrstuvwxyz'
        },
        textColor:{
        	type:String,
            default:'#0F0',
            validator:function(value){
          	  var colorReg = /^#([0-9a-fA-F]{6})|([0-9a-fA-F]{3})$/g
              return colorReg.test(value)
            }
        },
        backgroundColor:{
        	type:String,
            default:'rgba(0,0,0,0.1)',
            validator:function(value){
              var reg = /^[rR][gG][Bb][Aa][\(]((2[0-4][0-9]|25[0-5]|[01]?[0-9][0-9]?),){2}(2[0-4][0-9]|25[0-5]|[01]?[0-9][0-9]?),?(0\.\d{1,2}|1|0)?[\)]{1}$/;
              return reg.test(value);
            }
        },
        speed:{
        	type:Number,
            default:10,
            validator:function(value){
              return value%1 === 0;
            }
        }
    },
    mounted:function(){
          this.initRAF();
          this.initCanvas();
          this.initRainDrop();
          this.animationUpdate();
    },
    methods:{
    	 initRAF(){
         window.requestAnimationFrame = (function(){
           return window.requestAnimationFrame       ||
                  window.webkitRequestAnimationFrame ||
                  window.mozRequestAnimationFrame    ||
                  window.oRequestAnimationFrame      ||
                  function( callback ){
                    window.setTimeout(callback, 1000 / 60);
                  };
         })();
         window.cancelAnimationFrame = (function () {
           return window.cancelAnimationFrame ||
                  window.webkitCancelAnimationFrame ||
                  window.mozCancelAnimationFrame ||
                  window.oCancelAnimationFrame ||
                  function (id) {
                    window.clearTimeout(id);
                  };
           })();

       },
    	 initCanvas(){
         this.canvas = document.getElementById('vue-matrix-raindrop');
         //需要判断获取到的canvas是否是真的canvas
         if(this.canvas.tagName.toLowerCase() !== 'canvas'){
            console.error("Error! Invalid canvas! Please check the canvas's id!")
         }
         this.canvas.width = this.canvasWidth;
         this.canvas.height = this.canvasHeight;
         this.canvasCtx = this.canvas.getContext('2d');
         this.canvasCtx.font = this.fontSize+'px '+this.fontFamily;
         this.columns = this.canvas.width / this.fontSize;
       },
       initRainDrop(){
    	 	for(var i=0;i<this.columns;i++){
    	 		this.rainDropPositionArray.push(0);
        }
       },

       animationUpdate(){
       	 this.speedCnt++;
       	 //speed为1最快，越大越慢
       	 if(this.speedCnt===this.speed){
       	 	 this.speedCnt = 0;
           //绘制背景
           this.canvasCtx.fillStyle=this.backgroundColor;
           this.canvasCtx.fillRect(0,0,this.canvas.width,this.canvas.height);
           //绘制文字
           this.canvasCtx.fillStyle=this.textColor;
           for(var i=0,len=this.rainDropPositionArray.length;i<len;i++){
             this.rainDropPositionArray[i]++;
             var randomTextIndex = Math.floor(Math.random()*this.textContent.length);
             var randomText = this.textContent[randomTextIndex];
             var textYPostion = this.rainDropPositionArray[i]*this.fontSize;
             this.canvasCtx.fillText(randomText,i*this.fontSize,textYPostion);
             if(textYPostion>this.canvasHeight){
               if(Math.random()>0.9){
                 this.rainDropPositionArray[i]=0;
               }
             }
           }

         }
         window.requestAnimationFrame(this.animationUpdate)
       }
    },
		data () {
			return {
				canvasCtx:null,
                canvas:null,
                columns:0,
                rainDropPositionArray:[],
                speedCnt:0
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
