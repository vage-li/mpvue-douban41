<template>
  <div>
    <!-- 头部 -->
    <div class="header">
      <span>豆瓣</span>
      <icon type="search"
            size="20"
            color="#00b600">
      </icon>
      <button size="mini">打开豆瓣</button>
    </div>
    <!-- 热映 -->
    <div class="content">
      <div class="category">
        <!-- 标题 热映 -->
        <div class="title">
          <span>影院热映</span>
          <a href="">更多</a>
        </div>
        <!-- 影片展示区 -->
        <scroll-view class="scroll-view_H"
                     scroll-x="true"
                     style="width: 100%" 
                     enable-flex>

          <div class="scroll-view-item_H"
               v-for="item in movieList"
               :key="item.id">
            <img :src="item.images.large"
                 alt="">
            <p class="text-line1">{{item.title}}</p>
             <div class="rating">
              <div class="stars" v-if="item.rating.average">
                <img v-for="(item, i) in 5" :key="i" src="../../../static/images/star.svg" alt="" >
                </div>
              <span>{{item.rating.average?item.rating.average:'暂无评论'}}</span>
             </div>
          </div>
         
        </scroll-view>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      movieList: []
    }
  },
  created () {
    this.getMovie()
  },
  methods: {
    getMovie () {
      wx.request({
        url: 'https://api.douban.com/v2/movie/in_theaters?apikey=0df993c66c0c636e29ecbb5344252a4a',
        header: {
          'content-type': 'application/x-www-form-urlencoded'
        },
        success: res => {
          console.log(res)
          this.movieList = res.data.subjects
        }
      })
    }
  }
}
</script>

<style lang="less">
.header {
  display: flex;
  align-items: center;
  color: #00b600;
  height: 94rpx;
  border-bottom: 1px solid #eee;
  padding: 0 36rpx;
  button {
    background-color: #42bd56;
    color: #fff;
  }
  span {
    font-size: 24px;
  }
  icon {
    flex: 1;
    margin-top: 8rxp;
    margin-left: 28rpx;
  }
}
.category {
  .title {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 28rpx 38rpx;
    height: 86rpx;
    span {
      font-size: 40rpx;
    }
    a {
      color: #42bd56;
    }
  }
}
scroll-view {
  display: flex;
  
}
.text-line1 {
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap
}
.scroll-view-item_H {
  width: 200rpx;
  img {
    height: 286rpx;
    width: 200rpx;
  }
}
.rating{
  display: flex;
}
.stars{
  img{
    width: 20rpx;
    height: 20rpx;
  }
}
</style>