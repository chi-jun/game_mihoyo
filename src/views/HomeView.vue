<script setup>
import { ref } from 'vue'
import axios from 'axios'

import {mihoyo_info, mihoyo_uid_info} from '../api/urls'
const webstaticUrl = ref('https://webstatic.mihoyo.com/hk4e/event/e20190909gacha/index.html?authkey_ver=1&sign_type=2&auth_appid=webview_gacha&init_type=301&gacha_id=eaa07ae07196ca35c36b48213560ab6df7617e&timestamp=1648597985&lang=zh-cn&device_type=mobile&ext=%7b%22loc%22%3a%7b%22x%22%3a2238.020263671875%2c%22y%22%3a212.88307189941407%2c%22z%22%3a-913.114990234375%7d%2c%22platform%22%3a%22Android%22%7d&game_version=CNRELAndroid2.6.0_R6708157_S6988297_D6731353&plat_type=android&region=cn_gf01&authkey=6kjU4RgV10PA9T184K0Y2s23S4c93kPUzNlfUAigAmBHU0UvHLerW%2bopI3N%2bqm4IjmucZhCe%2fmY0Ij1DYYjg1%2b%2bMztHOQ6dxasL6Wa9AZhVdSu6ylxbxLQYtTa%2ftSldra3RVWT43nbvQWNoTOarZb9Oi%2f7iwONH94NZmuL8XLQEh0RCgpoK2D%2fUQ9wJ3Xl%2b1gibTq6u0ZLN2vJ895G2gTMYb9MyzuTM%2bnTvEe7XE80o3M9gWM1V2Fey9ud02tKoSm7DJB5VAmC2Iq22C8SLcq6X8nV4BKid4iZ3reer0%2bMJMHUyseNn5x4piNsA0oAN%2fOicphO8nMigS2QKPEOWc4hF%2fc5JiGzpx0UzmMmBtXIWwv0tasF61%2blwskXWEnxyd64w8kA3CWiYttJW4%2b%2f8nJhmShkyq3IOAe9US8fh%2fJUO1dSBFvKBBlqfQQuwhXQr1ytIioFLIhag9Q4VwPJ9Px0XfbFQRRnTBfQF2Y1AQcHWMfB%2fgnPjIfyixDItJgILSdyMJOLzfuYKsMv9mdsZB9FFR7u5JX%2bZam8yrJRAclvckhAF0zQevMru6XnWLqeiBke2rOk4iI71dSiNjsPPAgTST07%2fEWJ%2fQBrN0giIiCeAa8SDxl4GVzaKD96DTurj9lhL38rO647vJl%2bJwpQmfFwDDYzX%2bFvMTXTU49tBZL8ATq5Q%2fqPy6Ijn31BE8ivSnfZCevvoetyMtFjLgmfyb23bSgEs9Csqx9cqWr0i%2fc658yqACN0qKPNSVGNRW901SpQNvxPh0sY2y42jCr9qfCM2QnkEna0CdxtLhD%2fPChVKKB6rZN6lyKLjXTaHPAaG71u7Zk4pB4MS%2bXsjIG5wLL17h%2bYophyb%2buQf6L11jcaxpmdaB0Oqiw%2bPjCpUINXteFoxRXURH95zz2WcB2BVaxOIHHzkQQRsiC0Fq9Na6zC%2fgy3sSc%2bPvnpxF5Ps%2bTzukbAUPIOCL9Oo0iyKhASmWFcm1lJasFQlvQBdmTk9KeQUj69CPy%2b2m4mpFTn%2bU%2fGfhyhR8c2siCzvftazDgE09bFIDUpQxs54RPC%2blpJ3RyDV4vmUEmbjAReO4oaN9tQ2IfdIXumiW8%2f8Ma17Jb2VSKue2cYm57vqV9vxWJD5DhTB7utrHRQXv9pm4CsGX6c6SxK32eCz4vJWxqSE1bFFHKkaGdmh9d2ak2sZxjHyboOqpdoxyqp5O%2fYLfVdDeGtjM6Q1c7O3xxnByG7d67StRVOtCaU7B55Q8xuSITe1MvQ4Gy9AB%2fPkuJsjo2BZ7egnAzwQlz2OEUDVLXV6%2fcEDULsSNVVPhhDPqx3RGNVi4hdJJMlm%2bDyTfTEY20MH5PyBJz7u8B1NQNT2lgN977Fw%2fUw%3d%3d&game_biz=hk4e_cn#/log')

const num = ref(0)

const limit_list = []

const limit_5_list = [
  {name: '雷电将军', idx: 78},
  {name: '神子', idx: 80},
  {name: '钟离', idx: 78}
]

const permanent_list = [
  {name: '莫娜', idx: 78}
]

const weapon_list = [
  {name: '和噗鸢', idx: 30},
  {name: '狼末', idx: 67}
]

// 查询复制链接所得到的数据
const selectList = () => {
  if (webstaticUrl) {
    axios.post('/api/genshin_impact/save_gacha_info', {data: webstaticUrl.value}).then(res => {
      console.log(res)
    })
  }
}

const getList = (eid) => {
  // num.value += 1
  // if (num.value < 5) {
  //   getList()
  // }
  // gache_type    200常驻   301up   302武器
  let _url = webstaticUrl.value.substr(webstaticUrl.value.indexOf('?') + 1)

  _url = _url.replace('#/log', '')

  let url = '/api/event/gacha_info/api/getGachaLog?' + _url + '&gacha_type=302&page=1&size=20&end_id='
  if (eid) {
    url = url + eid
  }

  axios.get(url).then(res => {
    // console.log(res.data)

    let _list = res.data.data

    console.log(_list)

    if (Number(res.data.retcode) == 0) {
      setTimeout(function() {
        getList(_list.list[_list.list.length - 1].id)
      }, 1100)
      
    }

  })
}

const filterLimit5 = (list) => {

}
const filterPermanent = (list) => {

}
const filterWeapon = (list) => {

}
</script>

<template>
  <div class="select-page">
    <div class="select-page_title">查询最新的记录</div>
    <div class="select-page_select">
      <el-input type="textarea" v-model="webstaticUrl" placeholder="请粘贴复制出来的链接地址" style="width: 60%"/>

      <el-button type="primary" size="large" style="margin-left: 30px" @click="getList(false)">查询</el-button>

      <el-button>查看历史记录</el-button>
    </div>

    <div class="select-page_conlist">
      <div class="conlist-item">
        <div class="conlist-item_title">限时up池(已 <span>20</span> 抽未抽到)</div>
        <div class="conlist-item_list-5">
          <div v-for="(item, idx) in limit_5_list" class="list_5_item" :key="idx">
            <div>{{item.name}}</div>
            <div>{{item.idx}}</div>
          </div>
        </div>
        <div></div>
      </div>
      <div class="conlist-item">
        <div class="conlist-item_title">
          常驻up池(已 <span>20</span> 抽未抽到)
        </div>
        <div class="conlist-item_list-5">
          <div v-for="(pItem, pidx) in permanent_list" :key="pidx" class="list_5_item">
            <div>{{pItem.name}}</div>
            <div>{{pItem.idx}}</div>
          </div>
        </div>
        
      </div>
      <div class="conlist-item">
        <div class="conlist-item_title">
          武器池(已 <span>20</span> 抽未抽到)
        </div>

        <div class="conlist-item_list-5">
          <div v-for="(wItem, widx) in weapon_list" :key="widx" class="list_5_item">
            <div>{{wItem.name}}</div>
            <div>{{wItem.idx}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="less">
  .select-page {
    padding: 20px;
    width: 70%;

    .select-page_title {
      font-size: 18px;
      color: red;
      font-weight: 500;
    }

    .select-page_select {
      margin-top: 30px;
      display: flex;
      align-items: center;
      // justify-content: space-between;
    }

    .select-page_conlist {
      margin-top: 20px;
      width: 100%;
      height: 500px;
      border: 1px solid #ddd;
      display: flex;
      
      .conlist-item {
        flex: 1;
        border-right: 1px solid #ddd;
        padding: 5px;
        &:last-child {
          border: none;
        }

        .conlist-item_title {
          font-size: 16px;

          span {
            color: red;
            font-weight: 500;
          }
        }

        .conlist-item_list-5 {
          height: 50%;
          overflow: auto;
          padding: 10px;
          .list_5_item {
            display: flex;
            justify-content: space-between;
            line-height: 32px;
          }
        }
      }
    }
  }
</style>
