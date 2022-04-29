<script setup>
import { ref } from 'vue'
import axios from 'axios'
const webstaticUrl = ref('')

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

const getList = (eid) => {
  // num.value += 1
  // if (num.value < 5) {
  //   getList()
  // }
  // gache_type    200常驻   301up   302武器
  let url = '/api/event/gacha_info/api/getGachaLog?authkey_ver=1&sign_type=2&auth_appid=webview_gacha&init_type=400&gacha_id=eaa07ae07196ca35c36b48213560ab6df7617e&timestamp=1643447186&lang=zh-cn&device_type=mobile&ext=%7b%22loc%22%3a%7b%22x%22%3a-660.648193359375%2c%22y%22%3a224.5959014892578%2c%22z%22%3a201.34742736816407%7d%2c%22platform%22%3a%22Android%22%7d&game_version=CNRELAndroid2.6.0_R6708157_S6988297_D6731353&plat_type=android&region=cn_gf01&authkey=o1mm1hMcT049LWps%2fryUnM%2fow6xs3MswOiFyjAGiUSOTlCm4%2bHMfW6Qv5u7zXIw2X0BeVGpW43JNb4Z%2b7bvKiIwoGKYj5HysOYo%2bSSWKcZVBZBhk50UFimCb8C8UA3adBIRhL0jix8TU5yv3ZOBCNcvPP9bP0Am5cApxmiF5Szo8zSL%2bOoql1QAQ6twGkFd4C2SEQ714KHpBJOEjmY4a5PYoKoKsq7QC62Um7KbVmM8oPdD96KO%2fapVyl0XppRxpB8FBn%2f%2f9DxEFQ1kBDMRq3TwTaBppHFiqwsynLf4NghLYoUEYg1gvPRpQnbyRbdNjP3lVRb5h4dYgIL5B0uUtwTwjshF5U2uCM4%2bNCK1zj7pRxi8idUNky0gzSVvTpOdAksQkTHCixLkhIyJgH1xNUOgb7MiiTddcLtOcofmG7woqH%2bm%2f34tXuZKRrRVWK9m8EMa2erW2%2feT4ZKQoehFseshD49Tq2Bj6t2CVirl9AOeT6WwNiH9VBaicWdwskfbZTvBiopTEVyguiaL9Rx%2fPZls2zmSUlswStCSfj5S6YSxtRfaghdvzcmxYkujK6MkDJIOurLPL0p6J6EyQE3RuFeZ1KCZOnZ%2fVGJNXj7sTRGzd4GSYRrmhOrmvnmMFGyF5OVdLt%2bxq8Cz%2fuwW0Gbd01%2baLkJ6gQmjaXVJFL%2fOH3%2f%2bXOK4do7JNpgqH0na10RrBftzvE%2blXtfyV20Fy%2f4VW%2fxmkO3zseWjXgvtfyrT2Da452BHnXVeE1zegoEjTRmfELTBvZTaACCu2MqwzSoEL7WFBC5Ndw4doPvivXDKFEQvRRgC0gtdvghKidb4kZwdrth%2fn98xttqn2jS5%2bRiH6KowuveiM%2biCNIf714ZzUI%2fpmX%2b3EBLxwoQfE6cgXB8Q9sJ03Pjm4JSWhzx2X0I39PbEhEXFyaPiNKgEZkld7HXAFPDdQrI%2fPYFXpV0qy%2buL0Q8Y%2bxJCyTqGgVp7NcGMuML6E7EjRq8Mu0HcuZav2NSfcs%2fBCZJvgkulgKJ4TAbsxSgBas3Pvd2REIxFLrS5QXNL6VDFSzA58Mr9%2b5cHmW67UxFVhCFHOKGdaQ5L9BKFnIY%2bWxbFSiPH7RtyJq%2fmVw3uc9WiaDRpV8iH9MAN%2fVztR7d3Do6jvDhPCm%2b%2bzFCc26phmgAKMXTQB0%2ff%2fmY6DA7aSpycYu7UF0yAPMIAI2xNDm87Hvw8uNiSLbQLGEY388eQJ3q6d1onxb0fpcBsIjeLChBbnUsSuLfFhTi0BwzMUU5QsciUvsASUd3LxOkKblQ8HEQUwBvCXJVSide926csGXh3c2xjWhEZef5la7R748T0NRbCC2j4DOQVUrJtfrfTyUpg5hasAv4jBbl1xsw%3d%3d&game_biz=hk4e_cn&gacha_type=301&page=2&size=2000&end_id='
  if (eid) {
    url = url + eid
  }

  axios.get(url).then(res => {
    // console.log(res.data)

    let _list = res.data.data

    console.log(_list)

    if (Number(res.data.retcode) == 0) {
      getList(_list.list[_list.list.length - 1].id)
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
