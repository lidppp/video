<template>
  <div class="home">
    <div class="title" :style="{top:titleTop+'%',left:left+'%'}">
      炮视频
      <span>当前为{{activeAdrName}}</span>
    </div>
    <div class="inputbox" :style="{top:top+'%'}">
      <input
        type="text"
        placeholder="请输入视频网址，记得加http或者https，否则会导致不是您想要的视频"
        class="search"
        @blur="bl"
        v-model="url"
      />
      <div class="btn" @click="tsShowFn">观看</div>
      <div class="btn rLinebtn" @click="rLineFn">更换线路</div>
    </div>
    <HelloWorld v-if="show" :msg="goUrl" :style="{opacity:iframeOpacity}" />
    <div
      class="prompt"
      v-show="tsShow"
      :style="{opacity:opacitydata,transition:' all 0.5s'}"
    >视频格式不正确呦</div>
    <div v-show="rLShow" class="rLShowBox" :style="{opacity:rLShowBoxOpacity}">
      <div class="rLineBox">
        <div class="rLtitle">当前为{{activeAdrName}}</div>
        <div class="rLBtnbox">
          <div
            v-for="item,index in addresses"
            @click="changeAddr(item.url,item.name,item.id)"
            :key="item.id"
            :class="{active:item.id==activeAdr}"
          >{{item.name}}</div>
        </div>
      </div>
      <div class="zheZhao" @click="closerLine"></div>
    </div>
    <footer>
      本网站仅支持学习交流，勿用非法用途！本站不承担任何责任！
      <br />您在适用本网站是请确保已经阅读
      <router-link :to="{name:'about'}" style="color:#15f574">免责声明</router-link>
      <br />联系邮箱：1512282028@qq.com
    </footer>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/if.vue";
import { setTimeout, clearTimeout } from "timers";
export default {
  name: "home",
  data() {
    return {
      url: "",
      show: false,
      tsShow: false,
      opacitydata: 0,
      goUrl: "",
      top: 50,
      iframeOpacity: 0,
      titleTop: 40,
      left: 47,
      rLShow: false,
      addresses: [
        { name: "线路1", url: "http://jx.618g.com/?url=", id: 0 },
        { name: "线路2", url: "https://660e.com/?url=", id: 1 }
      ],
      activeAdr: 0,
      activeAdrName: "线路1",
      address: "http://jx.618g.com/?url=",
      rLShowBoxOpacity: 0
    };
  },
  components: {
    HelloWorld
  },
  methods: {
    bl() {
      var strRegex = /^(?:http(s)?:\/\/)?[\w.-]+(?:\.[\w\.-]+)+[\w\-\._~:/?#[\]@!\$&'\*\+,;=.]+$/;
      var re = new RegExp(strRegex);
      if (!re.test(this.url)) {
        this.showMsg();
      } else {
        this.goUrl = this.address + this.url;
        return true;
      }
    },
    tsShowFn() {
      if (this.goUrl == "") {
        this.showMsg();
        return false;
      }
      this.left = 5;
      this.top = 2;
      this.titleTop = 2;
      this.show = true;
      setTimeout(() => {
        this.iframeOpacity = 1;
      }, 0);
    },
    showMsg() {
      if (this.tsShow) {
        return false;
      }
      clearTimeout(tsshowTime);
      this.tsShow = true;
      var tsshowTime = setTimeout(() => {
        this.opacitydata = 1;
        setTimeout(() => {
          this.opacitydata = 0;
          setTimeout(() => {
            this.tsShow = false;
            return false;
          }, 1000);
        }, 3000);
      }, 0);
    },
    rLineFn() {
      this.rLShow = true;
      setTimeout(() => {
        this.rLShowBoxOpacity = 1;
      }, 1);
    },
    changeAddr(url, name, id) {
      this.activeAdrName = name;
      this.address = url;
      this.activeAdr = id;
    },
    closerLine() {
      this.rLShowBoxOpacity = 0;
      setTimeout(() => {
        this.rLShow = false;
      }, 501);
    }
  }
};
</script>
<style>
.home {
  padding-top: 9.41vh;
  box-sizing: border-box;
  height: 100%;
  align-content: center;
  position: relative;
}
.btn {
  display: inline-block;
  padding: 6px 24px;
  margin-bottom: 0;
  font-size: 14px;
  font-weight: 400;
  line-height: 1.42857143;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -ms-touch-action: manipulation;
  touch-action: manipulation;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  background-image: none;
  color: #fff;
  background-color: #15f574;
  border-color: #15f574;
  transition: all 0.5s ease 0s;
  -webkit-transition: all 0.5s ease 0s;
  -moz-transition: all 0.5s ease 0s;
  border-radius: 8px;
}
.btn:hover {
  outline: none;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.search {
  height: 28px;
  width: 500px;
  padding: 0 15px;
  margin-right: 15px;
  border-radius: 8px;
  background: none;
  outline: none;
  border: 1px #15f574 solid;
}
.inputbox {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  margin: auto;
  width: max-content;
  height: 7vh;
  transform: scaleX(-50%);
  transition: all 0.5s;
}
.prompt {
  position: fixed;
  height: 36px;
  width: max-content;
  line-height: 36px;
  font-size: 14px;
  background: rgba(0, 0, 0, 0.7);
  color: #fff;
  padding: 0 12px;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  transition: opacity 0.5s;
}
.title {
  width: max-content;
  height: max-content;
  font-size: 24px;
  position: absolute;
  top: 40%;
  left: 50%;
  transform: scale(-50%);
  transition: all 0.5s ease 0s;
  background-image: linear-gradient(
    0deg,
    #3498db,
    #f47920 10%,
    #d71345 20%,
    #f7acbc 30%,
    #ffd400 40%,
    #3498db 50%,
    #f47920 60%,
    #d71345 70%,
    #f7acbc 80%,
    #ffd400 90%,
    #3498db
  );
  -webkit–moz–ms-background-image: linear-gradient(
    0deg,
    #3498db,
    #f47920 10%,
    #d71345 20%,
    #f7acbc 30%,
    #ffd400 40%,
    #3498db 50%,
    #f47920 60%,
    #d71345 70%,
    #f7acbc 80%,
    #ffd400 90%,
    #3498db
  );
  background-size: 14000% 30000%;
  animation: mymove 120s ease infinite normal;
  -webkit-animation: mymove 120s ease infinite normal;
  -moz-animation: mymove 120s ease infinite normal;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit–moz–ms-background-clip: text;
  /*必需加前缀 -webkit- 才支持这个text值 */
  -webkit-text-fill-color: transparent;
}
.title > span {
  font-size: 14px;
}
@keyframes mymove {
  0% {
    background-position: 0% 0%;
  }

  50% {
    background-position: 50% 100%;
  }

  100% {
    background-position: 100% 0%;
  }
}
.rLinebtn {
  margin-left: 15px;
}
.rLineBox {
  width: 400px;
  height: 300px;
  border: #15f574 1px solid;
  box-sizing: border-box;
  padding: 40px;
  text-align: center;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #fff;
  z-index: 1;
}
.zheZhao {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  top: 0;
  left: 0;
}
.rLtitle {
  color: #15f574;
  margin-bottom: 48px;
}
.rLBtnbox {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.rLBtnbox > div {
  border: #15f574 1px solid;
  padding: 8px 12px;
  border-radius: 8px;
  cursor: pointer;
  user-select: none;
}
.rLBtnbox > div.active {
  background: #15f574;
  color: #fff;
}
.rLShowBox {
  transition: all 0.5s;
  opacity: 0;
}
footer {
  position: absolute;
  width: 100%;
  text-align: center;
  bottom: 18px;
  font-size: 12px;
  line-height: 16px;
  z-index: -1;
}
</style>

