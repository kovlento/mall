<template>
  <div class="footer">
    <div class="footer-logo">
      <img src="/imgs/logo-footer.png" alt="" />
      <p>小米商城</p>
    </div>
    <div class="footer-link">
      <a href="javascript:;"> MIUI </a><span>|</span>
      <a href="javascript:;"> 米家 </a><span>|</span>
      <a href="javascript:;"> 米聊 </a><span>|</span>
      <a href="javascript:;"> 多看 </a><span>|</span>
      <a href="javascript:;"> 游戏 </a><span>|</span>
      <a href="javascript:;"> 政企服务 </a><span>|</span>
      <a href="javascript:;"> 小米天猫店 </a>
    </div>
    <div class="copyright">
      Copyright @2020 <span class="domain">www.mi.com</span> All Rights Reserved
    </div>
  </div>
</template>

<script>
export default {
  name: 'nav-footer'
}
</script>

<style lang="scss">
.footer {
  height: 234px;
  border-top: 4px solid #ff6600;
  background-color: #333333;
  color: #999999;
  font-size: 16px;
  text-align: center;
  .footer-logo {
    margin: 46px 0 31px 0;
    img {
      width: 53px;
      height: 36px;
      margin-bottom: 13px;
    }
  }
  .footer-link {
    a {
      color: #999999;
      display: inline-block;
    }
    span {
      margin: 0 14px;
    }
  }
  .copyright {
    margin-top: 13px;
    .domain {
      color: #ff6600;
    }
  }
}
</style>
