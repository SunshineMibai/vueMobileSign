<template>
  <div class='can-vas'>
    <canvas id='can_vans'>您当前浏览器不支持canvas，建议更换浏览器！</canvas>
    <div>
         <button @click='Output'>确定</button>
         <button @click='ClearCanvas'>清空</button>
         <button @click='Canvas_goBack'>返回</button>    
      </div>
      <img :src="ImgSrc" v-if='ImgSrc'>
   </div>
</template>
<script>
   export default {
      data() {
         return {
            ImgSrc:'',
            screenWidth:document.documentElement.clientWidth
         }
      },
      mounted(){
         let canvas = document.getElementById('can_vans')
         let ctx = canvas.getContext('2d');
         let _x = 0,
         _y = 0,
         x = 0,
         y = 0;
         canvas.width = this.screenWidth - 20;// 设置画布大小
         canvas.height = 200;
         canvas.addEventListener('touchstart', function (e) {// 开始绘制
            e.preventDefault();
            _x = e.touches[0].pageX,
            _y = e.touches[0].pageY;
            ctx.beginPath();// 路径开始
            ctx.moveTo(_x - canvas.offsetTop, _y - canvas.offsetLeft);
            this.addEventListener('touchmove', function (e) {// 路径移动
               x = e.touches[0].pageX,
               y = e.touches[0].pageY;
               ctx.lineTo(x - canvas.offsetTop, y - canvas.offsetLeft);
               ctx.stroke();
            });
         });
      },
      methods:{
         Output(){
            let canvas = document.getElementById('can_vans')
            let ctx = canvas.getContext('2d')
            var oImg = new Image();
            ctx.drawImage(oImg, 0, 0);
            this.ImgSrc = canvas.toDataURL('image/png')
            //this.ImgSrc
         },
         ClearCanvas(){
            let canvas = document.getElementById('can_vans')
            let ctx = canvas.getContext('2d')
            ctx.clearRect(0, 0, canvas.width, canvas.height);
         },
         Canvas_goBack(){
            this.canvas.Url = this.ImgSrc
         }
      }
   }  
</script>
<style>
body{
   margin:0;
}
#can_vans{
   border:1px solid #ccc;
   margin:10px;
   box-sizing: border-box;
}
.can-vas>div{
   display: flex;
   justify-content: space-between;
}
.can-vas>div>button{
   background:#FF6600;
   height:35px;
   width:100px;
   color:#fff;
   border-radius: 5px;
   outline: none;
   border:none;
}
</style>