<template>
  <div>
    <div class="container-app" style="margin-top: 40px;margin-bottom: 40px">
      <h3>作品推荐 {{ WorkList.length }} 个</h3>
      <h4>作品收集，为基于图鸟UI开发的相关作品项目引流，展示在使用文档上

        图鸟UI一直在努力做的更好，2025年，也将做的更好。</h4>
      <div style="margin: 0 auto">
        <el-row :gutter="20" style="margin-top: 20px;">
          <el-col v-for="(item,index) in WorkList" :key="index" :xl="8" :lg="8" :md="12" :sm="12"  :xs="24"
                  @click="openDialog">
            <div class="works-card" @click="openDialog(item)">
              <span v-if="item.openSource" class="site-card-tag speed">开源<i class="light"></i></span>
              <span v-if="item.recommend" class="site-card-tag3 speed">推荐<i class="light"></i></span>
              <span v-else-if="!item.openSource" class="site-card-tag2 speed">群友<i class="light"></i></span>
              <div style="display: flex;flex-direction: column;">
                <div style="display: flex">
                  <el-image
                      :src="item.indexImg"
                      class="Star-img"
                      fit="fill"
                      style="width: 80px; height: 80px;border:1px #dedede solid;"></el-image>
                  <div>
                    <div style="font-size: 18px;font-weight: bold;margin: 14px 0px 12px 15px;text-align: left;">
                      {{ item.name }}
                      <a v-if="item.uniapp" :href="item.uniapp" target="_blank" @click.stop><span
                          class="iconfont">&#xe609;</span></a>
                      <a v-if="item.github" :href="item.github" target="_blank" @click.stop><span
                          class="iconfont">&#xe64a;</span></a>
                      <a v-if="item.gitee" :href="item.gitee" target="_blank" @click.stop><span
                          class="iconfont">&#xe600;</span></a>
                    </div>
                    <div style="display: flex">
                      <div v-for="(item2,index2) in item.tag"
                           style="margin: 0px 0px 0px 15px; border:1px #dedede80 solid;border-radius: 6px;padding: 0px 8px 0px 8px;font-size: 12px;">
                        {{ item2 }}
                      </div>
                    </div>
                  </div>
                </div>
                <div style="margin-top: 10px; text-align: left;">{{ item.desc }}</div>
              </div>
            </div>
          </el-col>
        </el-row>
      </div>
    </div>
    <ClientOnly>
      <el-dialog v-model="dialogVisible" custom-class="star-dialog" width="800px">
        <div>
          <div style="display: flex;flex-direction: column;">
            <div style="display: flex">
              <el-image
                  :src="dialogModel.indexImg"
                  class="Star-img"
                  fit="fill"
                  style="width: 80px; height: 80px;border:1px #dedede80 solid;"></el-image>
              <div>
                <div style="font-size: 18px;font-weight: bold;margin: 14px 0px 12px 15px;">
                  {{ dialogModel.name }}
                </div>
                <div style="display: flex">
                  <div v-for="(item2,index2) in dialogModel.tag"
                       style="margin: 0px 0px 0px 15px; border:1px #dedede80 solid;border-radius: 6px;padding: 0px 8px 0px 8px;font-size: 12px;">
                    {{ item2 }}
                  </div>
                </div>
              </div>
            </div>
            <div style="margin-top: 20px">{{ dialogModel.desc }}</div>
            <div style="margin-top: 20px">
              <a v-if="dialogModel.uniapp" :href="dialogModel.uniapp" target="_blank" @click.stop><span
                  style="color: var(--vp--works-dialog-link-color)">开源地址:</span>{{ dialogModel.uniapp }} </a>
              <a v-if="dialogModel.github" :href="dialogModel.github" target="_blank" @click.stop><span
                  style="color: var(--vp--works-dialog-link-color)">开源地址:</span>{{ dialogModel.github }}</a>
              <a v-if="dialogModel.gitee" :href="dialogModel.gitee" target="_blank" @click.stop><span
                  style="color: var(--vp--works-dialog-link-color)">开源地址:</span>{{ dialogModel.gitee }}</a>
              <a v-if="dialogModel.link" :href="dialogModel.link" target="_blank" @click.stop><span
                  style="color: var(--vp--works-dialog-link-color)">相关地址:</span>{{ dialogModel.link }}</a>
            </div>

            <div style="margin-top:35px ">
              <el-image v-for="(item3,index) in dialogModel.img" :src="item3"
                        style="width: 180px;margin: 0px 20px 0px 0px;"></el-image>
            </div>
          </div>
        </div>
      </el-dialog>
    </ClientOnly>
  </div>

</template>

<style lang="scss">
@font-face {
  font-family: 'doc-iconfont'; /* project id 1839347 */
  src: url('//at.alicdn.com/t/font_1839347_q72yio5zage.ttf') format('truetype');
}

.container-app {
  width: 1200px !important;
  margin: 0 auto;
}

@media (max-width: 1200px) {
  .container-app {
    width: 95% !important;
    margin: 0 auto;
  }
}

.Star-img {
  border-radius: 50px;
}

.grid-content {
  background: #0FD850;
}

h3 {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 10px;
}

h4 {
  font-size: 17px;
  font-weight: 400;
}

a {
  color: #03a9f4;
}


.iconfont {
  font-family: 'doc-iconfont', serif !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.star-dialog {
  border-radius: 10px !important;
}

.member-item {
  background-color: rgb(242, 242, 242);
  display: flex;
  padding: 20px;
  border-radius: 5px;
  margin-top: 25px;
  max-width: 1200px;

  &__avatar {
    height: 100px;
    flex: 0 0 100px;
    width: 100px;

    img {
      width: 100%;
      border-radius: 4px;
    }
  }

  &__info {
    margin-left: 20px;
  }

  &__name {
    color: #333;
    font-weight: bold;
    font-size: 16px;
    margin-top: 5px;
  }

  &__tag {
    display: flex;
    color: #999;
    font-size: 15px;
    margin-top: 5px;
    align-items: center;

    &__split {
      font-size: 20px;
      margin: 0 7px;
      color: #000;
    }
  }

  &__job {
    color: #555;
    font-size: 15px;
    margin-top: 7px;
  }

  &__intro {
    color: #666;
    font-size: 14px;
    margin-top: 7px;
  }
}


.works-card {
  height: 230px;
  text-align: center;
	border: 1px solid #eaeefb;
	border-radius: 10px;
	-webkit-transition: bottom 0.4s;
	transition: bottom 0.4s;
	position: relative;
	bottom: 0;
	margin: 10px 10px 10px 0;
  padding: 20px;
}

.works-card:hover {
  bottom: 6px;
	box-shadow: 0 6px 18px 0 rgba(232, 237, 250, .5);
}

.works-card:hover .mask {
  bottom: -1.5rem;
}

.works-card:hover .mask-c-1 {
  bottom: -2.5rem;
}

.site-card-tag {
  position: absolute;
  top: 0px;
  right: 0px;
  padding: 4px 8px;
  background-color: #57bd6a;
  color: #fff;
  z-index: 1;
  border-radius: 0 12px 0 12px;
  transition: 0.3s;
  font-size: 0.6rem;
  line-height: 1rem;
  opacity: 0.8;
}

.site-card-tag2 {
  position: absolute;
  top: 0px;
  right: 0px;
  padding: 4px 8px;
  background-color: #425aef;
  color: #fff;
  z-index: 1;
  border-radius: 0 12px 0 12px;
  transition: 0.3s;
  font-size: 0.6rem;
  line-height: 1rem;
  opacity: 0.8;
}
.site-card-tag3 {
  position: absolute;
  top: 0px;
  right: 0px;
  padding: 4px 8px;
  background-color: #d52b2b;
  color: #fff;
  z-index: 1;
  border-radius: 0 12px 0 12px;
  transition: 0.3s;
  font-size: 0.6rem;
  line-height: 1rem;
  opacity: 0.8;
}

.light {
  //cursor: pointer;
  position: absolute;
  //top: 0;
  width: 100px;
  height: 35px;
  background-image: -moz-linear-gradient(0deg, var(--vp--works-card-light-color-one), var(--vp--works-card-light-color-two), var(--vp--works-card-light-color-one));
  background-image: -webkit-linear-gradient(0deg, var(--vp--works-card-light-color-one), var(--vp--works-card-light-color-two), var(--vp--works-card-light-color-one));
  -webkit-animation: light_tag 4s both infinite;
  -moz-animation: light_tag 4s both infinite;
  -ms-animation: light_tag 4s both infinite;
  animation: light_tag 4s both infinite;
}

@keyframes light_tag {
  0% {
    transform: skewx(0deg);
    -o-transform: skewx(0deg);
    -moz-transform: skewx(0deg);
    -webkit-transform: skewx(0deg);
    left: -150px;
  }

  99% {
    transform: skewx(-25deg);
    -o-transform: skewx(-25deg);
    -moz-transform: skewx(-25deg);
    -webkit-transform: skewx(-25deg);
    left: 50px;
  }
}
</style>
<script lang="ts" setup>
import {onMounted, ref} from 'vue';

let dialogModel = ref({
  name: '小满社圈',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/xiaomantongcheng-wx.jpg',
  desc: '随时随地发现本地新鲜事。社区圈子论坛系统',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/xiaomantongcheng-wx.jpg'
  ],
  tag: ['同城', '社区', '圈子'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: '',
});
const openDialog = (item) => {
  dialogModel = item;
  console.log(dialogModel)
  dialogVisible.value = true;
};

function shuffleArray(array) {
  const firstFive = array.slice(0, 7);
  const remaining = array.slice(6);

  for (let i = firstFive.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [firstFive[i], firstFive[j]] = [firstFive[j], firstFive[i]];
  }

  for (let i = remaining.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [remaining[i], remaining[j]] = [remaining[j], remaining[i]];
  }

  return firstFive.concat(remaining);
}

onMounted(() => {
  WorkList.value = shuffleArray(WorkList.value);
});
const dialogVisible = ref(false);
const WorkList = ref([{
  name: '我的上铺',
  indexImg: 'https://img.ahuaaa.cn/img/AgAABjdJSeM7GY_7L3RLlqFjCJser4MI.png',
  desc: '运营了6年的外卖平台小程序，功能完善，营销功能丰富，最新版本重构使用的是图鸟ui进行开发，酷炫简约',
  img: [
    'https://img.ahuaaa.cn/img/20240302000702.png'
  ],
  tag: ['外卖','快送',],
  openSource: false,
  //是否显示推荐
  recommend: true,
  github: '',
  gitee: '',
  uniapp: ''
},{
  name: '小鸡PPT',
  indexImg: 'https://img.ahuaaa.cn/img/20230707143849.png',
  desc: '免费下载PPT，提供优质、丰富、高效的PPT模板',
  img: [
    'https://img.ahuaaa.cn/img/20230707143939.png'
  ],
  tag: ['PPT下载',],
  openSource: true,
  github: '',
  gitee: 'https://gitee.com/sunjulee/xjppt-app',
  uniapp: ''
}, {
  name: '兔兔找图',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/tutuzhaotu-wx.jpg',
  desc: '基于图鸟壁纸UI模板，实现的一款壁纸、文件处理等相关功能的微信小程序。',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/tutuzhaotu-wx.jpg'
  ],
  tag: ['文件处理', '壁纸',],
  openSource: true,
  github: 'https://github.com/tiku-cloud-platform/picture_db',
  gitee: '',
  uniapp: '',
}, {
  name: '多客社交圈子',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/duoke.jpg',
  desc: '多客圈子系统，提供开源前端和后端，是一款精心打磨的圈子社交论坛系统。让你快速拥有自己的圈子',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/duoke-wx.jpg'
  ],
  tag: ['多客', '圈子', '开源'],
  openSource: true,
  github: '',
  gitee: '',
  uniapp: 'https://ext.dcloud.net.cn/plugin?id=9617',
}, {
  name: '放心公寓',
  desc: '提供一些租房信息，智能管理自己租的房子以及只能交租，智能开门，智能化管理',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/fangxin.png',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/fangxin-wx.jpg'
  ],
  tag: ['生活', '便民'],
  openSource: true,
  github: '',
  gitee: 'https://gitee.com/ZhiNenShiDai_17674652335/cloud_apartment.git',
}, {
  name: '校园快跑跑',
  desc: '校园综合服务小程序，跑腿社区',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/xiaoyuankpp-wx.jpg',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/xiaoyuankpp-wx.jpg'
  ],
  tag: [],
  openSource: true,
  github: '',
  gitee: '',
  uniapp: 'https://ext.dcloud.net.cn/plugin?id=11188',
  link: '',
}, {
  name: 'minisns（迷你SNS）',
  desc: '社区电商程序',
  indexImg: 'https://img.ahuaaa.cn/img/20230517141313.png',
  img: [
    'https://img.ahuaaa.cn/img/20230517141328.png'
  ],
  tag: ['app', '小程序'],
  openSource: true,
  github: '',
  gitee: '',
  uniapp: 'https://ext.dcloud.net.cn/plugin?id=11115',
  link: ''
},{
  name: '执手相亲交友',
  desc: '来执手相亲交友，谈场认真且不将就的恋爱吧！',
  indexImg: 'https://img.ahuaaa.cn/img/20231122140641.png',
  img: [
    'https://img.ahuaaa.cn/img/20231122140801.png'
  ],
  tag: ['相亲交友APP',],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: 'https://a.app.qq.com/o/simple.jsp?pkgname=zs.weipaihudong.com'
}, {
  name: '比比轻壁纸',
  desc: '基于微信Skyline渲染框架+图鸟Vue3组件开发的适合个人、学生、自媒体使用的清爽型壁纸下载小程序',
  indexImg: 'https://img.ahuaaa.cn/img/20230901161455.png',
  img: [
    'https://img.ahuaaa.cn/img/20230901161511.png'
  ],
  tag: ['工具', '图片'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: 'https://mp.weixin.qq.com/s/NycGWUTHhURJ-SUHq0WE8Q'
}, {
  name: 'Coisini去水印',
  desc: '免费去抖音、小红书、微博等水印、无广告、无限制，咱就是主打一个免费。',
  indexImg: 'https://img.ahuaaa.cn/img/20230901161322.png',
  img: [
    'https://img.ahuaaa.cn/img/20230901161402.png'
  ],
  tag: ['小程序'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '电子鲁班',
  desc: '手持弹幕|AI一键抠图|尺子|MD5加密|时间戳转换|电子印章|图片添加水印|老照片修复|花体字转换|图片压缩|邮编查询|指南针|水平仪',
  indexImg: 'https://img.ahuaaa.cn/img/20230901161122.png',
  img: [
    'https://img.ahuaaa.cn/img/20230901161145.png'
  ],
  tag: ['工具'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '牛基圈晴雨表',
  desc: '您身边的投资小助手，实时查看基金预估涨幅收益！',
  indexImg: 'https://img.ahuaaa.cn/img/20230707144043.png',
  img: [
    'https://img.ahuaaa.cn/img/20230707144043.png'
  ],
  tag: ['基金'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '支出记账本',
  desc: '免费多人共享记账，3秒快速记账明细一目了然；满足家庭记账、圈子记账、公司记账、班级记账、情侣记账、个人记账、报销记账等',
  indexImg: 'https://img.ahuaaa.cn/img/20230627190454.png',
  img: [
    'https://img.ahuaaa.cn/img/20230627190518.png'
  ],
  tag: ['记账工具'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: 'AI关键词库大全',
  desc: '永久持续更新免费AI绘画关键词，描述词，提示词生成。AI智能绘画',
  indexImg: 'https://img.ahuaaa.cn/img/20230615155644.png',
  img: [
    'https://img.ahuaaa.cn/img/20230615155644.png'
  ],
  tag: ['小程序'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '麻瓜文案',
  desc: '用AI解决生活中的一些麻烦事，让生活变的有趣。我们的slogan——惬意生活由AI开启',
  indexImg: 'https://img.ahuaaa.cn/img/20230517140716.png',
  img: [
    'https://img.ahuaaa.cn/img/20230517140716.png'
  ],
  tag: ['AI工具'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '资猿圈',
  desc: '用于给程序员刷题，帮助程序员更好的找到工作积累经验，助于新手更好的学习，以及快速找到工作。',
  indexImg: 'https://img.ahuaaa.cn/img/20230517140921.png',
  img: [
    'https://img.ahuaaa.cn/img/20230517140921.png'
  ],
  tag: ['学习工具'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '吃喝玩乐嗨起来',
  desc: '每天都可以领取美团、饿了么、滴滴打车优惠券，还有各种电商隐藏优惠券，复制商品详情链接既可以获取哦！',
  indexImg: 'https://img.ahuaaa.cn/img/20230517141009.png',
  img: [
    'https://img.ahuaaa.cn/img/20230517141009.png'
  ],
  tag: ['优惠券工具'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '金陵市井',
  desc: '南京人的高颜值社交圈子',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/jinlinshijing-wx.png',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/jinlinshijing-wx.png'
  ],
  tag: ['社交'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '见知网',
  desc: '基于openai的开放接口，提供与ChatGPT一致的语言模型，为你的工作效率提升提供便捷服务。',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/jianzhiwang.jpg',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/jianzhiwang-wx.jpg'
  ],
  tag: ['gpt', '人工智能', '语言模型'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '美兜',
  desc: '记录大姨妈的极简工具',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/meidou-wx.jpg',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/meidou-wx.jpg'
  ],
  tag: [],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
}, {
  name: '一搜就学',
  desc: '基于图鸟ui的程序员学习小程序',
  indexImg: 'https://pans.ahuaaa.cn/docsimg/works/yisoujiuxue-wx.jpg',
  img: [
    'https://pans.ahuaaa.cn/docsimg/works/yisoujiuxue-wx.jpg'
  ],
  tag: ['编程学习'],
  openSource: false,
  github: '',
  gitee: '',
  uniapp: '',
  link: ''
},
  {
    name: '柒分糖图集',
    desc: '图片，壁纸',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/qifentang.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/qifentang-wx.png', 'https://pans.ahuaaa.cn/docsimg/works/qifentang-h5.png'
    ],
    tag: ['图片', '壁纸'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '穗苗去水印',
    desc: '抖音、快手、微视、皮皮虾等主流短视频平台一键免费去水印下载工具。',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/huimiao.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/huimiao-wx.jpg'
    ],
    tag: ['工具', '免费'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '练题帮手',
    desc: '一款基于FastAdmin（ThinkPHP）+Uniapp（图鸟UI）开发的小程序答题考试系统',
    indexImg: 'https://img.ahuaaa.cn/img/20230707144207.png',
    img: [
      'https://img.ahuaaa.cn/img/20230707144220.png'
    ],
    tag: ['答题'],
    openSource: false,
    github: '',
    gitee: '',
    link: 'https://www.fastadmin.net/store/exam.html'
  }, {
    name: '江夏生活网',
    desc: '江夏生活为江夏网友提供你不知道的江夏资讯、江夏招聘、江夏租房、商家优惠、生活类服务等江夏便民服务，致力江夏生活服务专业品牌。',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/jiangxia.jpg',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/jiangxia-wx.jpg'
    ],
    tag: ['圈子', '生活'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '多客社交圈子',
    indexImg: 'https://docs.ahuaaa.cn/docsimg/works/duoke.jpg',
    desc: '多客圈子系统，提供开源前端和后端，是一款精心打磨的圈子社交论坛系统。让你快速拥有自己的圈子',
    img: [
      'https://pans.ahuaaa.cn/docsimg/topimg.jpg', 'https://pans.ahuaaa.cn/docsimg/topimg.jpg', 'https://pans.ahuaaa.cn/docsimg/topimg.jpg'
    ],
    tag: ['多客', '圈子', '开源'],
    openSource: true,
    github: '',
    gitee: '',
    uniapp: '',
    link: '',
  }, {
    name: '电脑参数通',
    desc: '一个纯粹的电脑硬件参数查询对比小程序CPU、显卡参数快捷查询与对比',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/canshutong.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/canshutong-wx.png'
    ],
    tag: ['查询工具'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '传世云家谱',
    desc: '家谱制作小程序，每个家族都要有一个属于自己的云家谱。方便查看、维护更新。',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/chuanshiyun.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/chaunshiyun-wx.jpg'
    ],
    tag: ['家谱'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '企服云助手',
    desc: '企服云助手：小程序申请辅助工具，免费提供快速注册状态查询，免300认证费。（激活码找群里嘎嘎🆓）',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/qifuyunzhushou.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/qifuyunzhushou-wx.jpg'
    ],
    tag: ['工具', '小程序认证'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '迷恋自留地',
    desc: '个人博客（Net7+Vue）',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/milianziliudi.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/milianziliudi-wx.jpg'
    ],
    tag: ['博客'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '盐选解析',
    desc: '个人作品',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/yanxuanjiexi.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/yanxuanjiexi-wx.png'
    ],
    tag: ['工具', '阅读'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '封枫',
    desc: '个人作品',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/fengfeng.jpg',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/fengfeng.jpg'
    ],
    tag: ['个人'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: 'Besti AI',
    desc: '免费的ChatGPT',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/BestiAi.jpg',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/BestiAi-wx.jpg'
    ],
    tag: ['工具'],
    openSource: false,
    github: '',
    gitee: '',
  }, {
    name: '网站管家',
    desc: '手机移动端管理WordPress，z blog网站的小管家。',
    indexImg: 'https://pans.ahuaaa.cn/docsimg/works/wangzhanguanjia.png',
    img: [
      'https://pans.ahuaaa.cn/docsimg/works/wangzhanguanjia-wx.png'
    ],
    tag: ['WordPress', '管家'],
    openSource: false,
    github: '',
    gitee: '',
  },{
    name: '头像制作神器',
    desc: '基于图鸟Vue2的一款头像制作、图片处理小程序',
    indexImg: 'https://img.ahuaaa.cn/img/20240302000356.png',
    img: [
      'https://img.ahuaaa.cn/img/20240302000356.png'
    ],
    tag: ['图片处理'],
    openSource: false,
    github: '',
    gitee: '',
  },{
    name: '椰天下',
    desc: '椰天下小程序提供周边生活信息',
    indexImg: 'https://img.ahuaaa.cn/img/20240302000504.png',
    img: [
      'https://img.ahuaaa.cn/img/20240302000504.png'
    ],
    tag: ['圈子', '生活'],
    openSource: false,
    github: '',
    gitee: '',
  },{
    name: '家家康陪诊',
    desc: '陪诊小程序',
    indexImg: 'https://cdn.nlark.com/yuque/0/2025/jpeg/280373/1736855587318-assets/web-upload/31f51fe0-50f3-4fa8-9a43-b053e487ee9e.jpeg',
    img: [
      'https://cdn.nlark.com/yuque/0/2025/jpeg/280373/1736855587318-assets/web-upload/31f51fe0-50f3-4fa8-9a43-b053e487ee9e.jpeg'
    ],
    tag: ['健康', '医疗'],
    openSource: false,
    github: '',
    gitee: '',
  },]);
</script>
