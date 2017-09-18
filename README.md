# 移动端视频全屏 #
## html ##
    <div class="videoWrap">
		<!--X5播放头部-->
		<header class="header"></header>
		
		<video 
			id="video"
			class="video" 
			poster="" 
			src="http://flv2.bn.netease.com/videolib3/1709/13/inBxZ0915/HD/inBxZ0915-mobile.mp4" autoplay="autoplay" 
			x-webkit-airplay="true" 
			playsinline="true" 
			webkit-playsinline="true" 
			x5-video-player-type="h5" 
			x5-video-player-fullscreen="true">
		</video>
		
		<!--android点击播放层 图片自己替换-->
		<div class="poster">
			<!--播放小图标 不需要可以删了-->
			<img src="http://go.163.com/2017/0819/tissot/img/9.png" class="poster-icon">
		</div>
	
	</div>
## css ##
    .videoWrap{
		position: absolute;
		width: 100%;
		height: 100%;
		left: 0;
		top: 0;
	}
	.videoWrap .video {
	  position: absolute;
	  width: 100%;
	  height: 100%;
	}
	.fullscreen .video {
	  width: 100%;
	  height: 100%;
	  object-position: center 128px;
	}
	.fullscreen .header {
	  width: 100%;
	  height: 128px;
	  background: #373B3E;
	  position: absolute;
	  top: 0;
	  left: 0;
	  z-index: 9999;
	}
	.videoWrap .poster-icon{
		width: 64px;
		height: 64px;
		position: absolute;
		left: 50%;
		margin-left: -32px;
		top: 50%;
		margin-top: -32px;
	}
	.videoWrap .poster{
		width: 100%;
		height: 100%;
		position: absolute;
		left: 0;
		top: 0;
		background: url(poster.jpg) no-repeat center top;
		display: none;
	}
## js ##
    <script src="http://go.163.com/2015/public/common/js/zepto.min.js"></script>
	<script src="http://go.163.com/2015/public/common/js/common.min.js"></script>
	<script>
		//调用视频播放
		netease.autoPlay('video');

		//安卓下需要点击播放
		if(netease.ua.android && (netease.ua.weixin || netease.ua.newsapp)){

		  $('.videoWrap .poster').show();
		  $('.videoWrap .poster').click(function(){
		    $('.videoWrap .video')[0].play();
		    setTimeout(function(){
		      $('.videoWrap .poster').hide();
		    },300);
		  });
		}

		//视频全屏 尺寸根据视频修改
		function eResize(e){
			var cw = 640,
			ch = document.documentElement.clientHeight,
				vScale, vwScale, vhScale;
			vwScale = cw / 640, vhScale = ch / 1030;
			vScale = vwScale > vhScale ? vwScale : vhScale;
			$(e).css({
				'-webkit-transform': 'scale(' + vScale + ')',
				'-webkit-transform-origin': 'center top'
			});
		} 
		eResize('.videoWrap');
		$(window).bind("resize",function(){
			eResize('.videoWrap');
		});

		//X5内核
		var player = document.querySelector('.video');
		player.addEventListener('x5videoenterfullscreen', function() {
		  // 设为屏幕尺寸
		  player.style.width = document.body.width + 'px';// 建议此处写具体的值，如'640px'
		  player.style.height = (document.body.height-128) + 'px';// 建议此处写具体的值，如'1158px'(1030+128 需加上伪标题栏高度)
		  // 在body上添加样式类以控制全屏下的展示
		  document.querySelector('.videoWrap').classList.add('fullscreen');
		});

		player.addEventListener('x5videoexitfullscreen', function() {
		  player.style.width = player.style.height = '';
		  document.querySelector('.videoWrap').classList.remove('fullscreen');
		}, false);

	</script>




## DEMO ## [点击](http://test.go.163.com/go/2015/public/team/liwenhui/fullScreenVideo/)
