# lifeng-sproject
2017年11月2日建立
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>构造函数-轮播图</title>
    <style>
        *{margin: 0;padding: 0;}
        #pic{ width: 750px;height: 320px; margin: 50px auto;position: relative;overflow: hidden;}
        ul{position: absolute;left: 0; width: 4000px;height: 320px;transition: 1s;}
        li{width: 750px; height: 320px;float: left;list-style: none;}
        img{width: 750px;height: 320px;display: block;}
        p{width: 100px;height: 15px; position: absolute;bottom: 10px; right: 20px;}
        b{display: block;float: left;margin-right: 5px;width: 10px; height: 10px;border-radius: 10px;background: #fff;}
        .left , .right{display: block;width: 20px; height: 30px; text-align: center; font-size: 20px; line-height: 30px; position: absolute;top: 50%;margin-top: -15px;background: #ffdc46; }
        .left{left: 10px;}
        .right{right:10px;}
    </style>
   
</head>
<body>
    <div id="pic">
        <div>
            <ul id="ul">
                <li><img src="pic01.jpg" alt=""></li>
                <li><img src="pic02.jpg" alt=""></li>
                <li><img src="pic03.jpg" alt=""></li>
                <li><img src="pic04.jpg" alt=""></li>
                <li><img src="pic05.jpg" alt=""></li>
            </ul>
            <p>
                <b></b>
                <b></b>
                <b></b>
                <b></b>
                <b></b>
            </p>
        </div>
        <span class="left">&lt;</span>
        <span class="right">&gt;</span>
    </div>
    

     <script>
        window.onload = function(){
           var box = new Run('pic',4) ;
           box.init()
        }
         //创建一个构造函数
            function Run(id,Num){
                this.pic=document.getElementById(id);  //创建一个最外层的盒子属性
                this.num = Num;  //每张轮播图的索引值，从0开始，所以我设置实参的时候是轮播图片张数 - 1
                this.ul=document.getElementById('ul');
                this.li=document.getElementsByTagName('li');
                this.left=document.getElementsByClassName('left')[0]; //上一张的点击按钮
                this.right=document.getElementsByClassName('right')[0];//下一张的点击按钮
                this.b=document.getElementsByTagName('b');  //图片下面的小圆点
                this.liw=this.li[0].offsetWidth; //容器，或者说是显示出来的额图片的宽度
                this.tis=null;  //设置一格空的属性，后面赋值定时器
                this.i=0;  //设置索引属性
            }

            Run.prototype.init = function(){
                var self = this;
                self.move();
                //创建一个自动播放的定时器
                this.tis = setInterval(function(){
                    self.move();
                },2000);

                //鼠标进入轮播图动画中就关闭定时器
                this.pic.onmouseover = function(){
                    console.log("lll");
                    clearInterval(self.tis);
                };

                // 鼠标移除启动定时器
                this.pic.onmouseout = function(){
                    self.tis = setInterval(function(){
                        self.move();
                    },2000)
                };

                //点击右边按钮
                this.right.onclick = function(){
                    self.move();
                }

                //点击左边的按钮
                this.left.onclick = function(){
                    self.leftmove();
                } 
            };

            //自动播放的函数
            Run.prototype.move = function(){
                this.b[this.i].style.backgroundColor = "#fff";
                this.i++;
                if(this.i > this.num){
                    this.i = 0;
                }
                this.ul.style.left = -this.liw * this.i + "px";
                this.b[this.i].style.backgroundColor = "red";               
            };
            //点击左边按钮移动轮播图的函数
            Run.prototype.leftmove = function(){ 
                this.b[this.i].style.backgroundColor = "#fff";
                this.i--;
                if(this.i < 0){
                    this.i = this.num;
                }
                this.ul.style.left = -this.liw * this.i + "px";
                this.b[this.i].style.backgroundColor = "red";
            };
    </script>
</body>
</html>
