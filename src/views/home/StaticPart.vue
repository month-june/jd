<template>
  <div class="position">
    <span class="iconfont position_icon">&#xe648;</span>
    咸嘉大学生公寓2栋
    <span class="iconfont position_notice">&#xe60a;</span>
  </div>
  <div class="search">
    <span class="iconfont">&#xe677;</span>
    <span class="search_text">山姆会员商店优惠商品</span>
  </div>
  <div class="banner">
    <img class="banner_img" src="http://www.dell-lee.com/imgs/vue3/banner.jpg" alt="">
  </div>
  <div class="icons">
    <div class="icons_item" v-for="(item,index) in iconList" :key="index">
      <img :src="'http://www.dell-lee.com/imgs/vue3/'+item.imgName+'.png'" alt="" class="icons_item_img">
      <p class="icons_item_desc">{{item.desc}}</p>
    </div>
  </div>
  <div class="gap"></div>
</template>

<script>
export default {
    name:'StaticPart',
    setup(){
      const iconList=[
        { imgName:'超市',desc:'超市便利' },
        { imgName:'菜市场',desc:'菜市场' },
        { imgName:'水果店',desc:'水果店' },
        { imgName:'鲜花',desc:'鲜花绿植' },
        { imgName:'医药健康',desc:'医药健康' },
        { imgName:'家居',desc:'家居时尚' },
        { imgName:'蛋糕',desc:'烘培蛋糕' },
        { imgName:'签到',desc:'签到' },
        { imgName:'大牌免运',desc:'大牌免运' },
        { imgName:'红包',desc:'红包套餐' }
      ]
      return{iconList}
    }
}
</script>

<style lang="scss" scoped>
// scoped属性，让页面css只作用于本组件
@import '../../style/virables.scss';
@import '../../style/mixins.scss';
.position{ 
  position: relative;
  padding: .16rem .24rem .16rem 0;
  line-height: .22rem;
  font-size: .16rem;
  // overflow: hidden;
  // white-space: nowrap;
  // text-overflow: ellipsis;
  @include ellipsis;
  .position_icon{
    position: relative;
    font-size: .2rem;
    top: .01rem;
  }
  .position_notice{
    position:absolute;
    right: 0rem;   
    top: .17rem;
    font-size: .2rem;
  }
  color:$content-fontColor;
}
.search{
  margin-bottom: .12rem;
  line-height: .32rem;
  background: $search-bgColor;
  color: $search-fontColor;
  border-radius: .16rem;
  font-size: .14re;
  .iconfont{
    font-size: .16rem;
    display: inline-block;
    position: relative;
    top: .01rem;
    padding: 0 .08rem 0 .16rem;
  }
  &_text{
    display: inline-block;
    font-size: .14rem;
  }
}
.banner{
  height: 0;
  overflow: hidden;
  // 防抖，图片长宽比为25，4%
  padding-bottom: 25.4%;
  &_img{
    width: 100%;
  }
}
.icons{
  display: flex;
  flex-wrap: wrap;
  margin-top: .16rem;
  &_item{
    width:20%;
    &_img{
      display: block;
      width: .4rem;
      height: .4rem;
      margin: 0 auto;
    }
    &_desc{
      margin: .06rem 0 .16rem 0;
      text-align: center;
      color: $content-fontColor;
    }
  }
}
.gap{
  margin:0 -.18rem;
  height: .1rem;
  background: $content-bgColor
}
</style>