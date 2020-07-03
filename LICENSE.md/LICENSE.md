<style>
    * {padding:0px;margin:0px;}
    .box {width:500px;height:180px;overflow: hidden; position: relative;margin:30px auto;}
    .box img {
        width: 100%;
        height:100%;
    }
    .box span:nth-of-type(1){
        display: block;
        width: 50px;
        height: 50px;
        background:red;
        position: absolute;
        left:0;
        top:0;
    }
    .box span:nth-of-type(2){
        display: block;
        width: 50px;
        height: 50px;
        background:red;
        position: absolute;
        right: 0;
        top:0;
    }
    ul {
        list-style:none;
        position: absolute;
        bottom: 10px;
        left: 50%;
        margin-left: -30px;
    }
    ul li {
        float: left;
        width: 10px;
        height:10px;
        background: #fff;
        border-radius: 50%;
        margin-right: 10px;
    }
    ul li.active {background: blue;}
    </style>
    
    
    <div class="box box1">
        <img src="./image/img1.jpg" alt="">
        <span id="spanleft"></span>
        <span id="spanright"></span>
        <ul>
            <li class="active"></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>

    <div class="box box2">
        <img src="./image/img1.jpg" alt="">
        <span id="spanleft"></span>
        <span id="spanright"></span>
        <ul>
            <li class="active"></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
    <script src="./lunbotu.js"></script>
    <script>
        let obj1 = new Lunbotu(".box1")
        let obj2 = new Lunbotu(".box2")

        
    </script>
    
    
    
    
    
   d第一次上传  不会   
   
   function Lunbotu(el){
    this.el = document.querySelector(el)
    this.num = 1
    this.t
    this.init()
}
Lunbotu.prototype.init = function(){
    // 定时切换图片  dingshihuanIMG
    this.dingshihuanIMG()
    // 原点同步
    this.yuandiantongbu()
    // 鼠标移入移出
    this.over()
    
}

Lunbotu.prototype.dingshihuanIMG=function(){
    // 1、设置定时器
    this.t=setInterval(()=>{
        this.num++
        if(this.num==5) this.num=1
        // 1、1获取img更改路径
        let imgobj = this.el.querySelector("img")
        imgobj.src = `./image/img${this.num}.jpg`
         // 1、2调用原点同步
         this.yuandiantongbu()
    },1000)
    
}

Lunbotu.prototype.yuandiantongbu = function(){
    // 1.先获取所有原点标签
    let ulliobjs = this.el.querySelectorAll("ul>li")
    // 1.1遍历
    ulliobjs.forEach((itme)=>{
    // 1.2清除所有class
    itme.className=""
    })
    // 2.给自身添加class
    ulliobjs[this.num-1].className="active"
}
Lunbotu.prototype.over = function(){
    //1.先获取所有原点标签
    let ulliobjs = this.el.querySelectorAll("ul>li")
    // 2.遍历
    ulliobjs.forEach((itme,index)=>{
    // 2.1设置移入事件
    itme.addEventListener("mouseover",()=>{
    // 2.2清除定时器
    clearInterval(this.t)
    // 获取图片
    // console.log(index)
    let imgobj = this.el.querySelector("img")
    imgobj.src = `./image/img${index+1}.jpg`
    // 调用原点
    this.num=index+1
    this.yuandiantongbu()
    })
    itme.addEventListener("mouseout",()=>{
        this.dingshihuanIMG()
    })
    })
}
