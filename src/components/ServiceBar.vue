<template>
  <div class="service-bar">
    <div class="container">
      <ul>
        <li><span class="icon-setting"></span>预约维修服务</li>
        <li><span class="icon-sevday"></span>7天无理由退货</li>
        <li><span class="icon-fifday"></span>15天免费换货</li>
        <li><span class="icon-post"></span>满150元包邮</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'service-bar'
}
</script>

<style lang="scss">
@import '../assets/scss/mixin.scss';
.service-bar {
  padding: 33px 0;
  color: #666666;
  font-size: 16px;
  li {
    display: inline-block;
    width: 24.9%;
    text-align: center;
    border-right: 1px solid #e5e5e5;
  }
  span {
    display: inline-block;
    width: 20px;
    height: 20px;
    vertical-align: middle;
    margin-right: 8px;
  }
  .icon-setting {
    @include bgImg(20px, 20px, '/imgs/icon-setting.png');
  }
  .icon-sevday {
    @include bgImg(20px, 20px, '/imgs/icon-7day.png');
  }
  .icon-fifday {
    @include bgImg(20px, 20px, '/imgs/icon-15day.png');
  }
  .icon-post {
    @include bgImg(20px, 20px, '/imgs/icon-post.png');
  }
}
</style>
