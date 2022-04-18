<template>
  <v-row justify="center" align="center" style="display: block;">
    <v-card style="display: flex;margin: 20px;justify-content: center;align-items: center;">
      <v-col cols="6" sm="4" md="3">
        <v-card style="width: 100%;height: auto;">
          <img
            src="/header.jpg"
            style="width:100%;height:100%;"
          >
        </v-card>
      </v-col>
      <v-col cols="6" sm="4" md="3">
        <v-row no-gutters v-for="(item, i) in specialFeatureItems" :key="i">
          <v-col>
            <v-card style="font-size:20px;padding-left:2px;margin-bottom:5%;"> {{ item.name }} </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-card>
    <v-card style="margin: 20px;">
      <v-form>
        <v-container>
          <v-text-field
            label="自由検索"
          ></v-text-field>
        </v-container>
      </v-form>
    </v-card>
    <v-card style="margin: 20px;">
      <v-container>
        <v-row>
          <v-col v-for="(tagItems,i) in tagsItemList" :key="i" cols="12" sm="4" md="4">
            <v-checkbox v-for="(tagItem,j) in tagItems" :key="j"
              v-model="selectTags"
              :label="tagItem.tagName"
              color="primary"
              :value="tagItem.tagId"
              hide-details
            ></v-checkbox>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
    <v-card>
      <v-row v-for="(steamItem,i) in steamSelectItems" :key="i">
        <v-col style="display:flex" v-for="(item,j) in steamItem" :key="j">
          <iframe :src="item.srcUrl" frameborder="0" height="190"></iframe>
          <v-textarea :value="item.defaultText"></v-textarea>
        </v-col>
      </v-row>
    </v-card>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      selectTags:[],
      specialFeatureItems: [
        {
          name:'セール品',
          link:'/'
        },
        {
          name:'ジャンル特集',
          link:'/'
        },
        {
          name:'無料配布',
          link:'/'
        },
        {
          name:'開発者インタビュー',
          link:'/'
        },
      ],
      tagsItemList: [
        [{
          tagId:1,
          tagName:'アクション',
        },
        {
          tagId:2,
          tagName:'シミュレーション',
        },
        {
          tagId:3,
          tagName:'ストラテジー',
        }],
        [{
          tagId:4,
          tagName:'RPG',
        },
        {
          tagId:5,
          tagName:'Switch',
        }]
      ],
      //steam情報表示マスターデータ
      steamItemsData: [
        [
          {
            srcUrl:"https://store.steampowered.com/widget/1504570/",
            tagId:[1,2],
            defaultText:"アクション,シミュレーション ※リンク適当です。タグのテスト中",
          },
          {
            srcUrl:"https://store.steampowered.com/widget/1245620/440410/",
            tagId:[2],
            defaultText:"シミュレーション ※リンク適当です。タグのテスト中",
          },
          {
            srcUrl:"https://store.steampowered.com/widget/703080/202709/",
            tagId:[3],
            defaultText:"ストラテジー ※リンク適当です。タグのテスト中",
          }
        ],
        [
          {
            srcUrl:"https://store.steampowered.com/widget/1504570/",
            tagId:[4],
            defaultText:"RPG ※リンク適当です。タグのテスト中",
          },
          {
            srcUrl:"https://store.steampowered.com/widget/1245620/440410/",
            tagId:[5],
            defaultText:"Switch ※リンク適当です。タグのテスト中",
          },
          {
            srcUrl:"https://store.steampowered.com/widget/703080/202709/",
            tagId:[1,4],
            defaultText:"アクション,RPG ※リンク適当です。タグのテスト中",
          }
        ],
        [
          {
            srcUrl:"https://store.steampowered.com/widget/1504570/",
            tagId:[3,4],
            defaultText:"ストラテジー,RPG ※リンク適当です。タグのテスト中",
          },
          {
            srcUrl:"https://store.steampowered.com/widget/1245620/440410/",
            tagId:[2,5],
            defaultText:"シミュレーション,Switch ※リンク適当です。タグのテスト中",
          },
          {
            srcUrl:"https://store.steampowered.com/widget/703080/202709/",
            tagId:[1,5],
            defaultText:"アクション,Switch ※リンク適当です。タグのテスト中",
          }
        ]
      ],
      //タグ等で絞り込まれたsteamの情報
      steamSelectItems: [],
    }
  },
  mounted(){
    this.steamSelectItems = this.steamItemsData;
  },
  watch: {
    selectTags(){
      //一つもタグが選択されていない、またはすべて選択されている場合マスターデータをそのまま表示
      if(this.selectTags.length === 0 || this.selectTags.length === 5){
        this.steamSelectItems = this.steamItemsData;
        return this.steamSelectItems;
      }
      let selectItems = [];
      this.steamSelectItems = [];

      //一度データを一つの配列にまとめる
      for(let steamItems of this.steamItemsData){
        for(let items of steamItems){
          selectItems.push(items);
        }
      }
      console.log(selectItems);
      //tagをand条件で含んでいるデータに配列にまとめる
      let listPunctuate = [];
      let flag = true;
      for(let item of selectItems){
        for(let tagId of this.selectTags){
          if(!item.tagId.includes(tagId)){
            flag = false;
            break;
          }
        }
        if(flag){
          listPunctuate.push(item);
        }
        if(listPunctuate.length === 3){
          this.steamSelectItems.push(listPunctuate);
          listPunctuate = [];
        }
        flag = true;
      }
      if(listPunctuate.length !== 0){
        this.steamSelectItems.push(listPunctuate);
      }
      

      //まとめたデータを表示用に3小づつの配列に変換

      
    }
  },
  methods:{

  }
}

</script>
<style>
.v-card-default{
  width: 100%;
}
</style>