<template>
  <div class="welcome">
    <h1 class="title">Hve <a @click="openInBrowser('https://github.com/hellohve/hve')"><i-icon class="github" type="social-github" ></i-icon></a></h1>
    <div class="step-container">
      <p class="start">快速开始：</p>
      <i-timeline>
        <i-timeline-item>
            <p class="time">👣 ONE</p>
            <p class="content">基本信息设置，包含源文件目录设置、Domain、Repository、Branch、Username、Email、Token、BackupRepo</p>
            <p class="tip">tip: 建议填写全部字段来使用完整功能</p>
            <i-button @click="$router.push('/setting')">配 置</i-button>
        </i-timeline-item>
        <i-timeline-item>
            <p class="time">👣 TWO</p>
            <p class="content">网站相关信息设置，包含网站标题、每页文章数、Gitment相关配置</p>
            <p class="tip">tip: 建议填写全部字段来使用完整功能</p>
            <i-button @click="$router.push('/theme')">主 题</i-button>
        </i-timeline-item>
        <i-timeline-item>
            <p class="time">👣 THREE</p>
            <p class="content">带着你的创作灵感尽情使用吧</p>
            <i-button class="go" @click="$router.push('/post-list')">👉 Go</i-button>
        </i-timeline-item>
      </i-timeline>
      <div class="footer">
        Power by
        <a @click="openInBrowser('https://github.com/SimulatedGREG/electron-vue')">electron-vue</a> |
        Design & Develop 
        <a @click="openInBrowser('https://github.com/EryouHao')">EryouHao</a>
      </div>
    </div>
  </div>
</template>

<script>
import { shell } from 'electron'
export default {
  props: {
    force: String,
  },
  data() {
    return {}
  },
  mounted() {
    const settingIsSet = this.$db.get('isSet').value()
    const themeIsSet = this.$site.get('isSet').value()
    if (settingIsSet && themeIsSet && !this.force) {
      this.$router.push('/post-list')
    }
  },
  methods: {
    openInBrowser(url) {
      shell.openExternal(url)
    },
  },
}
</script>

<style lang="scss" scoped>
.welcome {
  text-align: center;
  .title {
    font-size: 32px;
    margin: 16px;
    font-weight: normal;
  }
  .step-container {
    text-align: left;
    padding: 24px 20%;
    @media (max-width: 800px) {
      padding: 24px;
    }
  }
  .start {
    margin-bottom: 32px;
    font-size: 18px;
    color: #000;
  }
  .tip {
    color: #757575;
    margin: 16px 0 8px;
  }
  .go {
    margin-top: 8px;
  }
  .github {
    font-size: 24px;
    cursor: pointer;
    float: right;
  }
}
</style>
