<template>
  <div class="recommend-radio">
    <IntoDetailsButton
      :intoDetailsButtonName="intoDetailsButtonName"
      @intoDetailsClick="intoDetailsClick"
    ></IntoDetailsButton>
    <div class="card">
      <div class="card-item" v-for="(item, index) in cardInfo" :key="index">
        <img :src="item.picUrl + '?param=170y170'" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
import IntoDetailsButton from "@/components/common/IntoDetailsButton.vue";
import { getRecommendRadioStation } from "@/network/api";
export default {
  name: "Radio",
  data() {
    return {
      intoDetailsButtonName: "主播电台",
      cardInfo: [],
    };
  },
  components: {
    IntoDetailsButton,
  },
  async created() {
    const { data } = await getRecommendRadioStation();
    this.cardInfo = data.result;
  },
  methods: {
    intoDetailsClick() {
      this.$router.push("/anchorradio");
    },
  },
};
</script>

<style scoped lang="scss">
.recommend-radio {
  width: 100%;
  margin-top: 20px;
  .card {
    display: flex;
    .card-item {
      position: relative;
      padding-bottom: 10px;
      margin-top: 10px;
      border-radius: 5px;
      width: 15%;
      padding-right: 20px;
      img {
        width: 100%;
        border-radius: 5px;
      }
    }
  }
}
</style>
