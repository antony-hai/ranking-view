<template>
  <div :class="$style.container">
    <div :class="$style.header">
      <!-- <div class="input-outer"><input type="text"></div>
      <div class="btn-outer"><nut-button>搜索</nut-button></div> -->
      <nut-searchbar
        v-model="searchVal"
        @search="handleSearch"
        :class="$style.searchBar"
      >
        <template #rightin>
          <nut-button type="primary" size="small">搜索</nut-button>
        </template>
      </nut-searchbar>
    </div>
    <div :class="$style.main">
      <nut-empty description="暂无选手" v-if="players.length === 0" />
      <scroll-view
        v-else
        :enable-flex="true"
        :scroll-y="true"
        style="height: 100%"
        @scrolltolower="lower"
        :scroll-into-view="toView"
        :class="$style.scrollView"
      >
        <view :class="$style.scrollItem" v-for="item in players" :key="item">
          <image
            :src="imgUrl"
            :class="$style.img"
            mode="aspectFill"
            :lazyLoad="true"
          />
          <div :class="$style.desc">
            <div style="font-size: 13px">名字：<text>邓杨李莎</text></div>
          </div>
          <div style="font-size: 13px" :class="$style.count">
            票数：<nut-tag plain type="success">{{ item }}票</nut-tag>
          </div>
          <div :class="$style.vote">
            <nut-button
              size="small"
              type="primary"
              @click="handleVote(item)"
              style="width: 100%; border-radius: 6px"
              >投票</nut-button
            >
          </div>
        </view>
      </scroll-view>
    </div>
    <div :class="$style.footer">
      <div :class="$style.btn">活动规则</div>
      <div :class="$style.btn" @click="rankingVisible = true">排行榜</div>
    </div>

    <nut-dialog
      footer-direction="vertical"
      teleport="#app"
      :no-footer="true"
      :pop-class="$style.rankingPop"
      title="排行榜"
      v-model:visible="rankingVisible"
    >
      <div :class="raingline" v-for="(item, index) in rankingList" :key="{item}">
        <div><span>{{ index }}.</span>名字的</div>
        <div>几个票</div>
      </div>
    </nut-dialog>
  </div>
</template>

<script setup>
import { ref } from "vue";
import imgUrl from "../../images/1.jpg";
import Taro from "@tarojs/taro";

const searchVal = ref("");
const rankingVisible = ref(false)

const players = ref([1, 2, 3, 4, 5, 6, 7]);
const rankingList = ref([1,2,3,4,5,6,7])
const toView = ref("card1");

const handleSearch = (text) => {
  console.log(text);
};

const lower = (e) => {
  console.log("lower: 滑动更新TODO", e);
};

const handleVote = (player) => {
  Taro.showModal({
    content: `确定给${player}投票吗?`,
    confirmColor: "#0abab5",
    success: function (res) {
      if (res.confirm) {
        console.log("投票了");
      }
    },
  });
};
</script>

<style module lang="less">
@primary-color: #0abab5;
@container-padding: 24px;

.container {
  display: flex;
  flex-direction: column;
  height: 100%;
  // min-height: 100vh;
  box-sizing: border-box;
  // overflow-y: hidden;
}

.header {
  background-color: #fff;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: @container-padding;
  box-shadow: 0 0 8px 0 rgba(0, 0, 0, 0.04);
  width: 100%;
}
.searchBar {
  padding: 0;
  :global(.nut-searchbar__input-bar) {
    border: none;
    vertical-align: middle;
    margin-top: -4px;
  }
}

.main {
  // height: calc(100% - 200px);
  flex: 1;
  background-color: aliceblue;
  min-height: 1px;
}
.scrollView {
  height: 100%;
  padding: @container-padding;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  box-sizing: border-box;
}
.scrollItem {
  box-sizing: border-box;
  background-color: #ffffff;
  overflow: hidden;
  border-radius: 12px;
  width: 48%;
  height: 440px;
  margin-top: 20px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
  &:nth-child(-n + 2) {
    margin-top: 0;
  }
  .img {
    width: 100%;
    height: 240px;
  }
  .desc {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: gray;
    padding: 6px 12px;
  }
  .count {
    padding: 6px 12px;
    color: gray;
  }
  .vote {
    padding: 0 12px;
    margin-top: 24px;
  }
}

.footer {
  padding: @container-padding;
  display: flex;
  box-sizing: border-box;
  justify-content: space-between;
  align-items: center;
  height: 100px;
  background-color: #fff;
  width: 100%;
  > .btn {
    // background-color: @primary-color;
    background: white;
    border: 1px solid @primary-color;
    color: @primary-color;
    font-weight: 500;
    width: 48%;
    text-align: center;
    font-size: 32px;
    height: 70px;
    line-height: 70px;
    font-size: 28px;
    // color: #fff;
    border-radius: 12px;
  }
}

.rankingPop {
  height: 50%;
  :global {
    .nut-dialog__header {
      font-size: 18PX;
      font-weight: 500;
      height: 60px;
      line-height: 60px;
    }
    .nut-dialog {
      border-radius: 12px;
      padding: 32px 24px;
      height: 100%;
      overflow: hidden;
    }

  }
}
</style>
