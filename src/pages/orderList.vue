<template>
  <div class="order-list">
    <order-header title="订单列表">
      <template v-slot:tip>
        <span>请谨防钓鱼链接或诈骗电话，了解更多></span>
      </template>
    </order-header>
    <div class="wrapper">
      <div class="container">
        <div class="order-box">
          <loading v-if="loading"></loading>
          <div class="order" v-for="(item, i) in list" :key="i">
            <div class="order-title">
              <div class="item-info fl">
                {{ item.createTime }}
                <span>|</span>
                {{ item.receiverName }}
                <span>|</span>
                订单号：{{ item.orderNo }}
                <span>|</span>
                {{ item.paymentTypeDesc }}
              </div>
              <div class="item-money fr">
                <span>应付金额：</span>
                <span class="money">{{ item.payment }}</span>
                <span>元</span>
              </div>
            </div>
            <div class="order-content clearfix">
              <div class="good-box fl">
                <div
                  class="good-list"
                  v-for="(sub, j) in item.orderItemVoList"
                  :key="j"
                >
                  <div class="good-img">
                    <img v-lazy="sub.productImage" alt="" />
                  </div>
                  <div class="good-name">
                    <div class="p-name">{{ sub.productName }}</div>
                    <div class="p-money">
                      {{ sub.totalPrice + '×' + sub.quantity }}元
                    </div>
                  </div>
                </div>
              </div>
              <div class="good-state fr" v-if="item.status == 10">
                <a href="javascript:;" @click="goPay(item.orderNo)">{{
                  item.statusDesc
                }}</a>
              </div>
              <div class="good-state fr" v-else>
                <a href="javascript:;">{{ item.statusDesc }}</a>
              </div>
            </div>
          </div>
          <el-pagination
            class="pagination"
            background
            :pageSize="pageSize"
            layout="prev, pager, next"
            :total="total"
            @current-change="handleChange"
          >
          </el-pagination>
          <div class="load-more" v-if="false">
            <el-button type="primary" :loading="btnloading" @click="loadMore"
              >加载更多</el-button
            >
          </div>
          <div
            v-if="false"
            class="scroll-more"
            v-infinite-scroll="scollMore"
            infinite-scroll-disabled="busy"
            infinite-scroll-distance="410"
          >
            <img
              v-if="scrollLoading"
              src="/imgs/loading-svg/loading-spinning-bubbles.svg"
              alt=""
            />
          </div>
          <no-data v-if="!loading && list.length == 0"></no-data>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import OrderHeader from './../components/OrderHeader'
import Loading from './../components/Loading'
import NoData from './../components/NoData'
import { Pagination, Button } from 'element-ui'
import infiniteScroll from 'vue-infinite-scroll'
export default {
  name: 'order-list',
  components: {
    OrderHeader,
    Loading,
    NoData,
    [Pagination.name]: Pagination,
    [Button.name]: Button
  },
  directives: { infiniteScroll },
  data() {
    return {
      list: [],
      loading: true,
      pageSize: 10,
      pageNum: 1,
      total: 0,
      btnloading: false,
      busy: true,
      scrollLoading: false
    }
  },
  mounted() {
    this.getOrderList()
  },
  methods: {
    getOrderList() {
      this.btnloading = true
      this.axios
        .get('/orders', {
          params: {
            pageSize: 1,
            pageNum: this.pageNum
          }
        })
        .then(res => {
          this.loading = false
          this.list = this.list.concat(res.list)
          this.total = res.total
          this.btnloading = false
        })
        .catch(() => {
          this.loading = false
        })
    },
    goPay(orderNo) {
      this.$router.push({
        path: '/order/pay',
        query: {
          orderNo
        }
      })
    },
    //专门给scrollMore使用
    getList() {
      this.scrollLoading = true
      this.axios
        .get('/orders', {
          params: {
            pageSize: 1,
            pageNum: this.pageNum
          }
        })
        .then(res => {
          this.list = this.list.concat(res.list)
          this.scrollLoading = false
          if (res.hasNextPage) {
            this.busy = false
          } else {
            this.busy = true
          }
        })
        .catch(() => {
          this.loading = false
        })
    },
    //分页第一种方法 分页器
    handleChange(pageNum) {
      this.pageNum = pageNum
      this.getOrderList()
    },
    //分页第二种方法 加载更多
    loadMore() {
      this.pageNum++
      this.getOrderList()
    },
    // 分页第三种方法 滚动加载更多
    scollMore() {
      this.busy = true
      setTimeout(() => {
        this.pageNum++
        this.getList()
      }, 500)
    }
  }
}
</script>
<style lang="scss">
@import './../assets/scss/config.scss';
@import './../assets/scss/mixin.scss';
.order-list {
  .wrapper {
    background-color: $colorJ;
    padding-top: 33px;
    padding-bottom: 110px;
    .order-box {
      .order {
        @include border();
        background-color: $colorG;
        margin-bottom: 31px;
        &:last-child {
          margin-bottom: 0;
        }
        .order-title {
          @include height(74px);
          background-color: $colorK;
          padding: 0 43px;
          font-size: 16px;
          color: $colorC;
          .item-info {
            span {
              margin: 0 9px;
            }
          }
          .money {
            font-size: 26px;
            color: $colorB;
          }
        }
        .order-content {
          padding: 0 43px;
          .good-box {
            width: 88%;
            .good-list {
              display: flex;
              align-items: center;
              height: 145px;
              .good-img {
                width: 112px;
                img {
                  width: 100%;
                }
              }
              .good-name {
                font-size: 20px;
                color: $colorB;
              }
            }
          }
          .good-state {
            @include height(145px);
            font-size: 20px;
            color: $colorA;
            a {
              color: $colorA;
            }
          }
        }
      }
      .pagination {
        text-align: right;
      }
      .el-pagination.is-background .el-pager li:not(.disabled).active {
        background-color: #ff6600;
      }
      .el-button--primary {
        background-color: #ff6600;
        border-color: #ff6600;
      }
      .load-more,
      .scroll-more {
        text-align: center;
      }
    }
  }
}
</style>
