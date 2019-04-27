# Js-carousel
原生js实现轮播图


      <!DOCTYPE html>
      <html>

      <head>
      <title>轮播图</title>
      <meta charset="utf-8">
      </head>
      <style type="text/css">
      body,
      html {
      padding: 0;
      margin: 0;
      }

   .wrapper {
    width: 800px;
    min-width: 800px;
    max-width: 800px;
    overflow: hidden;
    height: 400px;
    border: 1px solid red;
    margin: 50px auto;
    position: relative;
   }

  .container {
    width: 4000px;
    height: 100%;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-size: 0px;
    position: absolute;
  }

  .container li,
  .container li>img {
    padding: 0;
    margin: 0;
    display: inline-block;
    height: 100%;
    list-style: none;
    width: 800px;
  }

  .btn {
    min-width: 800px;
    position: absolute;
    top: 45%;
    height: 60px;
  }

  .btn::after {
    clear: both;
    content: '';
  }

  .btn-left {
    float: left;
    width: 100px;
    height: 100%;
    opacity: 0.35;
    background-color: #000;
    font-size: 60px;
    z-index: 999;
    line-height: 60px;
    cursor: pointer;
    color: #fff;
  }

  .btn-right {
    float: right;
    width: 100px;
    height: 100%;
    opacity: 0.35;
    background-color: #000;
    font-size: 60px;
    z-index: 999;
    cursor: pointer;
    text-align: center;
    line-height: 60px;
    color: #fff;
  }

  .point {
    position: absolute;
    bottom: 2%;
    width: 200px;
    height: 30px;
    list-style: none;
    left: 35%;
   }

  .point li {
    height: 15px;
    width: 15px;
    border-radius: 50%;
    margin: 10px;
    display: inline-block;
    cursor: pointer;
  }
  .active{
	background-color: red;
  }
  .normal{
	background-color: #fff;
	opacity: 0.6;
  }
        </style>

	<body>
        <div class="wrapper">
        <ul class="container">
            <li class="oli"><img src="./images/banner02.jpg"></li>
            <li class="oli"><img src="./images/banner03.jpg"></li>
            <li class="oli"><img src="./images/banner05.jpg"></li>
            <li class="oli"><img src="./images/banner06.jpg"></li>
            <li class="oli"><img src="./images/banner09.jpg"></li>
        </ul>
        <ul class="point">
            <li class="po normal"></li>
            <li class="po normal"></li>
            <li class="po normal"></li>
            <li class="po normal"></li>
            <li class="po normal"></li>
        </ul>
        <div class="btn">
            <div class="btn-left">
                <</div> <div class="btn-right">>
            </div>
        </div>
    </div>
    <script type="text/javascript">
    var oindex = 0,
    	pindex = 0,
        len = document.getElementsByClassName('oli'),
        oleft = document.getElementsByClassName('btn-left')[0],
        oright = document.getElementsByClassName('btn-right')[0],
        obox = document.getElementsByClassName('container')[0],
        opoint = document.getElementsByClassName('po'),
        timer;

    function init() {
        bindEvent();
        slide();
    }
    init();

    function bindEvent() {
        for (var i = 0; i < len.length; i++) {
            len[i].oindex = i;
        }
        for(var j = 0;j<opoint.length;j++){
    		opoint[j].pindex = j;
    	}
        //监听鼠标点击向左
        oleft.addEventListener('click', function(e) {
            move('left')
        })

        //监听鼠标点击向右
        oright.addEventListener('click', function(e) {
            move('right')
        })

        //监听鼠标移入事件
        obox.addEventListener('mouseenter', function(e) {
            clearInterval(timer);
        })

        //监听鼠标离开事件
        obox.addEventListener('mouseleave', function(e) {
            //设置定时器 延迟2000ms
            slide();
        })
    }

    //移动函数
    function move(dir) {

        if (dir == 'left') {
            oindex++;
            pindex++;
            oindex = oindex > len.length - 1 ? 0 : oindex;
            pindex = pindex > len.length - 1 ? 0 : pindex;
        } else {
            oindex--;
            pindex--;
            oindex = oindex < 0 ? len.length - 1 : oindex;
            pindex = pindex < 0 ? len.length - 1 : pindex;
        }
        for(var j = 0;j<opoint.length;j++){
    		if(opoint[j].pindex == oindex){
    			opoint[j].className ="po active"
    		}else{
    			opoint[j].className ="po normal"
    		}
    	}
        obox.style.left = -oindex * 800 + 'px';
    }
    //自动轮播
    function slide() {
        clearInterval(timer);
        //设置定时器 延迟2000ms
        timer = setInterval(function() {
            move('left')
        }, 2000);
    }
    </script>
</body>

</html>


