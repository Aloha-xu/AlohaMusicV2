<template>
  <div class="card">
    <div class="card-content" @click="cardClick">
      <BaseImage
        :src="pic"
        class="playcard-img"
        :lazy="true"
        :isShowPlayLogo="isShowPlayLogo"
      ></BaseImage>
      <span class="palycount disapper">
        <slot name="card_palycount">{{ playCount }}</slot>
      </span>
      <!-- slot 作者名字 -->
      <div class="creattor">
        <slot name="card_creator"></slot>
      </div>
      <span class="totle-play-time">
        <slot name="totlepalytime"></slot>
      </span>
    </div>
    <div class="text">
      {{ text }}
    </div>
    <div class="card-YY-MM-DD">
      <slot name="yymmdd"></slot>
    </div>
    <div class="track-count" v-show="trackCount">{{ trackCount }}首</div>
  </div>
</template>
<script>
export default {
  name: "PlayCard",
  props: {
    pic: {
      type: String,
      default: "",
    },
    playcount: {
      type: Number,
      default: 0,
    },
    text: {
      type: String,
      default: "",
    },
    id: {
      type: Number,
      default: 0,
    },
    trackCount: {
      type: Number,
      default: 0,
    },
    isShowPlayLogo: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      activeColor: "red",
    };
  },
  computed: {
    //少于1w 就显示原本的数字
    playCount() {
      return parseInt((this.playcount / 10000).toFixed(0)) === 0
        ? this.playcount
        : parseInt((this.playcount / 10000).toFixed(0)) + "万";
    },
  },
  methods: {
    cardClick() {
      this.$emit("cardClick", this.id);
    },
  },
};
</script>

<style scoped lang="scss">
@keyframes jump {
  0% {
    transform: translate(0px, 0px);
  }
  100% {
    transform: translate(0px, -12px);
  }
}
.card {
  padding-bottom: 10px;
  margin-top: 10px;
  .card-content {
    width: 100%;
    position: relative;
    //隐藏播放次数
    &:hover .disapper {
      display: none;
    }
    .playcard-img {
      box-shadow: 2px 4px 8px #585858cc;
      border-radius: 10px;
      //上跳
      &:hover {
        animation: jump 0.9s ease 1 normal;
        transform: translate(0px, -12px);
      }
    }
    .palycount {
      position: absolute;
      top: 3px;
      right: 9px;
      font-size: 12px;
      color: white;
    }
    .creattor {
      position: absolute;
      left: 10px;
      bottom: 70px;
      color: aliceblue;
    }
    .totle-play-time {
      position: absolute;
      right: 8px;
      bottom: 7px;
      color: aliceblue;
    }
  }
  .text {
    font-size: 13px;
    letter-spacing: 0.7px;
    overflow: hidden;
    text-overflow: ellipsis;
    margin-top: 5px;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    line-height: 20px;
  }
  .card-YY-MM-DD {
    font-size: 13px;
    font-weight: 300;
    margin-top: 10px;
  }
  .track-count {
    font-size: 13px;
    font-weight: 300;
  }
}
</style>
