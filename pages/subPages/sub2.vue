<template>
  <v-row justify="center" align="center" style="display: block;">
      sub2
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
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
          tagName:'シュミレーション',
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
      ]
    }
  },
  watch: {
    
  }
}
</script>
<style>
.v-card-default{
  width: 100%;
}
</style>