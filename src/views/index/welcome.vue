<template>
  <div class="app-container" v-infinite-scroll="load" style="overflow:auto">
    <el-row type="flex">
      <el-col v-for="o in 4" :key="o" offset="1" :span="5">
        <el-card body-style="padding: 0px">
          <img src="@/assets/custom_images/xball.jpg" class="img">
          <div style="padding: 15px">
            <span style="font-weight: bold">title</span>
            <div>
              <time>{{ currentDate }}</time>
              <el-button type="text" style="float: right;padding: 0px">更多操作</el-button>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>

    <div class="box">
      <div style="display: block">
        <div v-for="index in images" :key="images.indexOf(index)" offset="5" class="secondary">
          <a @click="test(index)" :class="index.class" :title="index.title">
            <div class="hex-1"></div>
            <div class="hex-2"></div>
          </a>
        </div>
      </div>

      <div style="margin-top: 50px;display: block;margin-left: 105px">
        <div v-for="index in 4" :key="images.indexOf(images[index])" offset="4" class="secondary">
          <a @click="test(images[index])" :class="images[index].class" :title="images[index].title">
            <div class="hex-1"></div>
            <div class="hex-2"></div>
          </a>
        </div>
      </div>

      <div style="margin-top: 50px;display: block">
        <div v-for="index in images" :key="images.indexOf(index)" class="secondary">
          <a @click="test(index)" :class="index.class" :title="index.title">
            <div class="hex-1"></div>
            <div class="hex-2"></div>
          </a>
        </div>
      </div>
    </div>
    <p v-if="loading">加载中...</p>
  </div>
</template>

<script>
export default {
  name: 'Welcome',
  data() {
    return {
      currentDate: this.dateFtt('yyyy-MM-dd hh:mm:ss', new Date()),
      images: [
        { title: '../../assets/custom_images/xball.jpg', class: 'hex a' },
        { title: '../../assets/custom_images/baskateball.jpg', class: 'hex b' },
        { title: '../../assets/custom_images/football.jpg', class: 'hex c' },
        { title: '../../assets/custom_images/qixing.jpg', class: 'hex d' },
        { title: '../../assets/custom_images/swim.jpg', class: 'hex e' }
      ],
      loading: false
    }
  },
  methods: {
    // 时间格式化
    dateFtt(fmt, date) {
      const o = {
        'M+': date.getMonth() + 1, // 月份
        'd+': date.getDate(), // 日
        'h+': date.getHours(), // 小时
        'm+': date.getMinutes(), // 分
        's+': date.getSeconds(), // 秒
        'q+': Math.floor((date.getMonth() + 3) / 3), // 季度
        'S': date.getMilliseconds() // 毫秒
      }
      if (/(y+)/.test(fmt)) { fmt = fmt.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length)) }
      for (var k in o) {
        if (new RegExp('(' + k + ')').test(fmt)) {
          fmt = fmt.replace(RegExp.$1, (RegExp.$1.length === 1)
            ? (o[k]) : (('00' + o[k]).substr(('' + o[k]).length)))
        }
      }
      return fmt
    },
    test(obj) {
      alert(obj.title)
    },
    load() {
      this.loading = true
      alert(111)
      setTimeout(() => {
        this.loading = false
      }, 2000)
    }
  }
}
</script>

<style scoped>
  .img{
    width: 100%;
  }
  .img:hover{
    transition: all 0.3s ease-in-out;
    /*transform: rotateX(30deg);*/
    transform: translateY(4.6734px) scale(2.14762);
  }
  .box{
    width: 65%;
    margin: 100px auto;
  }
  .secondary{
    margin: 10px;
    display: inline-block;
    position: relative;
  }
  .secondary > a{
    background-color: #4AB7BD;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-size: auto 220px;
  }
  .hex{
    border: 1px solid lightgray;
    width: 190px;
    height: 110px;
    display: block;
    float: left;
    line-height: 111px;
    text-align: center;
    font-size: 18px;
    word-spacing: 1px;
  }
  .hex:hover{
    transition: all 0.3s ease-in-out;
    transform: translateY(45.6734px) scale(1.14762);
  }
  .a{
    background-image: url("https://builtbybuffalo.com/uploads/work/300/1616190654.png");
  }
  .b{
    background-image: url("https://builtbybuffalo.com/uploads/work/300/1306190728.png");
  }
  .c{
    background-image: url("https://builtbybuffalo.com/uploads/work/300/252340614.jpg");
  }
  .d{
    background-image: url("https://builtbybuffalo.com/uploads/work/300/35605953.jpg");
  }
  .e{
    background-image: url("https://builtbybuffalo.com/uploads/work/300/1524531779.png");
  }
  .hex > div{
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    overflow: hidden;
    background: inherit;
  }
  .hex-1{
    transform: rotate(60deg);
    z-index: -1
  }
  .hex-2{
    transform: rotate(-60deg);
    z-index: -2
  }
  .secondary .hex-1:before, .secondary .hex-2:before{
    content: '';
    position: absolute;
    background: inherit;
    left: 0;
    background: inherit;
    transform: rotate(-60deg) translate(-110px,0);
  }
</style>
