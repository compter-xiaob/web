# web
# 前端练手区

## 文字云简单学习

### 使用HTML、CSS 和 Javascript 制作文字雨动画

主体部分分为文字和云 以及倒影

倒影部分可以在container容器的css样式加入

```
-webkit-box-reflect: below 1px linear-gradient(transparent,transparent,transparent,transparent,#000500);
```

PS：-webkit-box-reflect要考虑兼容性的问题

云

```
/*Style.css*/
//云底部用一个简单圆角矩形
.cloud{
    position: relative;
    width: 320px;
    height: 100px;
    background: #fff;
    border-radius: 100px;
    z-index: 100;
    filter: drop-shadow(0 0 35px #fff);
}
//云朵的头部用伪类进行填充
.cloud::before{
    content: '';
    position: absolute;
    top: -50px;
    left: 40px;
    width: 110px;
    height: 110px;
    border-radius: 50%;
    background: #fff;
    box-shadow: 90px 0 0 30px #fff;
}
```

文字雨部分

```
//简单随机创造一些文字
function randomText(){
            const text = ("abcdefghijklmnopqrstuvwxyz0123456789");
            letter = text[Math.floor(Math.random() * text.length)];
            return letter;
        }
//再将生成文字修改css样式添加到云的后代上
function rain(){
            let cloud = document.querySelector('.cloud');
            let e = document.createElement('div');
            let left = Math.floor(Math.random()*300)
            let size = Math.random() * 1.5;
            let duration = Math.random() * 1;
            e.classList.add('text');
            cloud.appendChild(e);
            e.innerText = randomText();
            e.style.left = left + 'px';
            e.style.fontSize = 0.5 + size + 'em'
            e.style.animationDuration = 1 + duration + 's';
			//文字落地到地面上消除 2s是动画时间
            setTimeout(() => {
                cloud.removeChild(e)
            }, 2000);
        }
//最后批量生成文字雨 
setInterval(function(){
            rain();
        },50)
```

最后添加一下动画即可完成

```
.text{
    position: absolute;
    height: 20px;
    top: 40px;
    line-height: 20px;
    text-transform: uppercase;
    color:#fff;
    text-shadow: 0 0 5px #fff,
    0 0 15px #fff,
    0 0 30px #fff;
    transform-origin: bottom;
    animation: animate 2s linear forwards;
}
@keyframes animate {
    0%{
        transform: translateY(0) scale(1);
    }
    50%{
        transform: translateY(145px) scale(1);
    }
    100%{
        transform: translateY(290px) scale(1);
    }
}
```

