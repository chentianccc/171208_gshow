<!--
 * @Description: In User Settings Edit
 * @Author: your name
 * @Date: 2019-10-10 15:38:55
 * @LastEditTime: 2019-10-25 18:15:48
 * @LastEditors: Please set LastEditors
 -->
<template>
        <section class="msite">
        <!--首页头部-->
        <HeaderTop title="确认订单">
          <span class="header_search" slot="left" @click="$router.back()">
               <i class="iconfont icon-jiantou2"></i>
           
          </span>
           <span class="header_login" slot="right">
           <router-link to="login">
             <span class="header_login_text">登录|注册</span>
           </router-link>
            
          </span>
        </HeaderTop>
      <section class="profile_my_order border-1px">
      <!-- 服务中心 -->
      <a href="javascript:" class="my_order">
        <div class="my_order_div">
          <span>请添加一个收获地址</span>
          <span class="my_order_icon">
                <i class="iconfont icon-jiantou1"></i>
              </span>
        </div>
      </a>
    </section>
    <section class="delivery_model container_style">
      <p class="deliver_text">送达时间</p>
      <section class="deliver_time">
        <p style="color:#02a774">尽快送达 | 预计6:10</p>
        <p style="font-size:10px;background-color:#02a774;color:#fff;padding:2px;border-radius:.12rem;margin-top:-6px">蜂鸟专送</p>
      </section>
    </section>
     <section class="profile_my_order border-1px">
      <a href='javascript:' class="my">
            <!-- <span>
              <i class="iconfont icon-jifen"></i>
            </span> -->
        <div class="my_order_text">
          <span>支付方式</span>
          <span class="tow">在线支付</span>
          <span class="my_order_icon">
               <!-- <span>在线支付</span> -->
                <i class="iconfont icon-jiantou1"></i>
              </span>
        </div>
      </a>
      <!-- 硅谷外卖会员卡 -->
      <a href="javascript:" class="my">
            <!-- <span>
              <i class="iconfont icon-vip"></i>
            </span> -->
        <div class="my_order_text">
          <span>红包</span>
          <span class="tow">在APP中使用</span>
          <span class="my_order_icon">
                <!-- <span>暂时只在饿了吧APP中支持</span> -->
                <i class="iconfont icon-jiantou1"></i>
              </span>
        </div>
      </a>
    </section>
    <section class="food_list">
      <header class="list_header">
        <img src="">
        <span>嘉禾一品（温都水城</span>
      </header>
      <ul class="food_list_ul">
        <li class="food_item_style" v-for="(food,index) in cartFoods" :key="index">
          <span>{{food.name}}</span>
          <!-- <span class="tow">×3</span> -->
          <span class="my_order_icon">
                <span class="pric">{{food.price}}</span>
              </span>
        </li>
      </ul>
    </section>
    <section class="profile_my_order border-1px">
      <a href='javascript:' class="my">
            <!-- <span>
              <i class="iconfont icon-jifen"></i>
            </span> -->
        <div class="my_order_text">
          <span>餐具份数</span>
          <span class="tow">未选择</span>
          <span class="my_order_icon">
               <!-- <span>在线支付</span> -->
                <i class="iconfont icon-jiantou1"></i>
              </span>
        </div>
      </a>
      <!-- 硅谷外卖会员卡 -->
      <a href="javascript:" class="my">
            <!-- <span>
              <i class="iconfont icon-vip"></i>
            </span> -->
        <div class="my_order_text">
          <span>订单备注</span>
          <span class="tow">口味、偏好</span>
          <span class="my_order_icon">
                <!-- <span>暂时只在饿了吧APP中支持</span> -->
                <i class="iconfont icon-jiantou1"></i>
              </span>
        </div>
      </a>
    </section>
    <div class="shop_pay">
      <div class="pay">
      <div class="content">
        <div class="content_left">
          <div class="price">￥31</div>
          <div class="desc">另需配送费￥4元</div>
        </div>
        <div class="content_right">
          <a href="#">
            <div class="pay_list">结算</div>
          </a>
        </div>
      </div>
    </div>
    </div>
    
  </section>
    
</template>

<script>
  import HeaderTop from '../../components/HeaderTop/HeaderTop.vue'
  import { MessageBox } from 'mint-ui'
  import BScroll from 'better-scroll'
  import {mapState, mapGetters} from 'vuex'
   export default {
    data () {
      return {
        isShow: false
        
      }
    },
	
    components: {
      HeaderTop
    },
	 computed: {
      ...mapState(['cartFoods', 'info']),
      ...mapGetters(['totalCount', 'totalPrice']),
      payClass () {
        const {totalPrice} = this
        const {minPrice} = this.info

        return totalPrice>=minPrice ? 'enough' : 'not-enough'
      },
      // payText () {
      //   const {totalPrice} = this
      //   const {minPrice} = this.info
      //   if(totalPrice===0) {
      //     return `￥${minPrice}元起送`
      //   } else if(totalPrice<minPrice) {
      //     return `还差￥${minPrice-totalPrice}元起送`
      //   } else {
      //     return '结算'
      //   }
      // },

      listShow () {
        // 如果总数量为0, 直接不显示
        if(this.totalCount===0) {
          this.isShow = false
          return false
        }

        if(this.isShow) {
          this.$nextTick(() => {
            // 实现BScroll的实例是一个单例
            if(!this.scroll) {
              this.scroll = new BScroll('.list-content', {
                click: true
              })
            } else {
              this.scroll.refresh() // 让滚动条刷新一下: 重新统计内容的高度
            }

          })
        }

        return this.isShow
      }
    },

  }
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
  @import "../../common/stylus/mixins.styl"
   .msite  //首页
      width 100%
      overflow-x hidden
      overflow-y hidden
      // position fixed 
      // padding 0
      // margin 0
      .icon-jiantou2
          color #fff
      .my_order_div
          width 100%
          margin 0
          padding 0
          // border-bottom 1px solid #f1f1f1
          padding 30px 20px 18px 0
          font-size 16px
          color #333
          display flex
          justify-content space-between
          font-weight bold
          // margin-top 20px
          span
            display block
          .my_order_icon
            width 10px
            height 10px
            // margin-left 90px
            .icon-jiantou1
              color #bbb
              font-size 10px
      .my_order
          width 100%
          border-bottom 1px solid #f1f1f1
          // box-shadow 0px 3px 14px #A3A3A3
          padding 40px 20px 18px 0
          font-size 16px
          color #333
          display flex
          text-decoration none
          // justify-content space-between
          // margin-top 20px
          .time
            width 90px
      .delivery_model
          width 100%
          border-left 10px solid #02a774
          display flex
          align-items center
          justify-content space-between
          border-bottom 1px solid #f1f1f1
          .deliver_text
            // float left
            margin-right 30%
            padding-left 10px
            font-weight bold
            // margin-top 50%
          .deliver_time
            display flex
            flex-direction column
            align-items flex-end 
            margin-right 13px
      .profile_my_order
          margin-top 10px
          // background #fff
          border-bottom 1px solid #f1f1f1
          .my
            width 100%
            border-bottom 1px solid #f1f1f1
            padding  6px 10px 1px 0
            font-size 16px
            color #333
            display flex
            text-decoration none
            border-top 1px solid #f1f1f1
            .my_order_text
              width 100%
              margin 0
              // padding 0
              // border-bottom 1px solid #f1f1f1
              padding 6px 10px 14px 0
              font-size 16px
              color #333
              display flex
              justify-content space-between
              span
                display block
              .tow
                margin-left 50%
                color #cccccc
                font-size 14px
              .my_order_icon
                width 10px
                height 10px
                // margin-left 90px
                .icon-jiantou1
                  color #bbb
                  font-size 10px
        .food_list
          width 100%
          // padding 20px 0
          margin-top 10px
          .list_header
            padding 5px 10px
            border-bottom 1px solid #f1f1f1
            border-top 1px solid #f1f1f1
            span 
              font-weight bold
              display block
              margin-bottom 17px
          .food_list_ul
            width 100%
            list-style none
            // display: none;
            .food_item_style
              list-style none 
              display flex
              padding 16px 10px 1px 0
              width 100%
              border-bottom 1px solid #f1f1f1
              // display block
              color #333
              // justify-content space-between
              span 
                display block
              .tow
                margin-left 37%
                font-size 14px
              .my_order_icon
                margin-left 16%
				        // .pric
                //   position absolute
                //   line-height 24px
                //   font-weight 700
                //   font-size 14px
        .shop_pay
          position fixed
          left 0
          bottom 0
          z-index 50
          width 100%
          height 48px
          background #38393a
          .pay
            .content_left
              // flex 1
              float left
              width 50%
              margin-left 20px
              margin-top 4px
              .price
                color #fff
                font-weight bold
              .desc
                color #ccc
                font-size 12px  
            .content_right
              float right
              padding 14px 40px 20px 40px
              background #00b43c
              .pay_list
                color #fff
                font-weight bold
                text-decoration none
                
    </style>
