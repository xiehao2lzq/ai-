<template>
  <div class="basicInformation">
    <div class="rightLogo"></div>
    <div class="title clear">
      <p></p>
      <span>基础信息</span>
    </div>
    <ul>
      <li class="clear">
        <img src="../../../static/bgImage/device1.png" alt />
        <p>设备总数</p>
        <span>{{info.totalNum}}个</span>
      </li>
      <li class="clear">
        <img src="../../../static/bgImage/device2.png" alt />
        <p>在线设备数</p>
        <span>{{info.onlineNum}}个</span>
      </li>
      <li class="clear">
        <img src="../../../static/bgImage/device3.png" alt />
        <p>离线设备数</p>
        <span>{{info.offlineNum}}个</span>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  data() {
    return {
      info: {}
    };
  },
  computed: {
    ...mapState({
      selectedValue: state => state.homePage.selectedValue
    }),
    ...mapState({
      url: state => state.homePage.url
    })
  }, 
  created() {
    this.$axios({
      method: "get",
      url: "http://" + this.url + ":9000/sjwl/webapi/device/info",
      headers: {
        Authorization: sessionStorage.getItem("Authorization")
      },
      params: {
        areaId: "0",
        xqCode: this.selectedValue,
        subdistrictId: ""
      }
    }).then(res => {
      //console.log(res,111)
      if (res.data.code == "1000") {
        this.info = res.data.data;
      }
    });
  }
};
</script>

<style lang="scss" scoped>
.basicInformation {
  width: 516px;
  height: 482px;
  background: #2f324b;
  box-shadow: 0px 1px 8px 0px rgba(28, 31, 52, 0.99);
  border-radius: 4px;
  position: relative;
  margin-left: 11px;
  margin-top: 10px;
  overflow: hidden;
  float: left;
}
.rightLogo {
  width: 123px;
  height: 14px;
  background: url(../../../static/bgImage/point.png);
  position: absolute;
  top: 0;
  right: 4px;
}
.basicInformation {
  .title {
    margin-top: 13px;
    margin-left: 10px;
    p {
      width: 6px;
      height: 16px;
      float: left;
      background: linear-gradient(
        0deg,
        rgba(35, 197, 235, 1),
        rgba(35, 230, 189, 1)
      );
      box-shadow: 0px 3px 7px 0px rgba(0, 0, 0, 0.12);
      border-radius: 2px;
      margin-right: 10px;
    }
    span {
      float: left;
      font-size: 16px;
      line-height: 16px;
    }
  }
}
ul {
  width: 100%;
  margin-top: 48px;
  li:nth-child(odd) {
    width: 444px;
    height: 100px;
    background: rgba(40, 42, 63, 1);
    margin: 27px auto 0;
    line-height: 68px;
    font-size: 24px;
    img {
      float: left;
      margin-top: 30px;
      margin-left: 12px;
    }
    p {
      float: left;
      margin-left: 20px;
      background: linear-gradient(
        0deg,
        rgba(35, 197, 235, 1) 0%,
        rgba(35, 230, 189, 1) 100%
      );
      -webkit-background-clip: text;
      color: transparent;
      margin-top: 20px;
    }
    span {
      float: right;
      margin-right: 20px;
      background: linear-gradient(
        0deg,
        rgba(35, 197, 235, 1) 0%,
        rgba(35, 230, 189, 1) 100%
      );
      -webkit-background-clip: text;
      color: transparent;
      margin-top: 20px;
    }
  }
  li:nth-child(even) {
    width: 444px;
    height: 100px;
    background: rgba(40, 42, 63, 1);
    margin: 27px auto 0;
    line-height: 68px;
    font-size: 24px;
    img {
      float: left;
      margin-top: 30px;
      margin-left: 12px;
    }
    p {
      float: left;
      margin-left: 20px;
      background: linear-gradient(
        180deg,
        rgba(62, 173, 250, 1) 0.4150390625%,
        rgba(6, 104, 225, 1) 100%
      );
      -webkit-background-clip: text;
      color: transparent;
      margin-top: 20px;
    }
    span {
      float: right;
      margin-right: 20px;
      background: linear-gradient(
        180deg,
        rgba(62, 173, 250, 1) 0.4150390625%,
        rgba(6, 104, 225, 1) 100%
      );
      -webkit-background-clip: text;
      color: transparent;
      margin-top: 20px;
    }
  }
}
</style>