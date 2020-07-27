<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
     <!--整个题目+答案-->
    <div style="display: block" v-for="(item,key) in showData" v-bind:key="key">
      <p style="margin-bottom: 0;text-align: left;font-size: medium;font-weight: bold"
         v-html="(key+1)+'.'+item.question"></p>
      <p style="margin-bottom: 1px;margin-top: 1px;text-align: left; font-size: small" v-for="(answer,i) in item.answers" v-bind:key="i" v-html="letters[i]+'.'+answer"></p>
      <p style="margin-bottom: 0;text-align: left;font-size: small;font-weight: bold"> 解析:</p>
      <p style="margin-bottom: 0;text-align: left;font-size: small; " v-html="item.analyticDesc"></p>
    </div>
  </div>
</template>

<script>
import exam from '../../static/【押题卷1】私募股权投资基金基础知识'

export default {
  name: 'Home',
  mounted: function () {
    this.questionsDetail = exam.Topic
    this.answersDetail = exam.Answer
    for (let i of this.questionsDetail) {
      let object = Object()
      object.question = i.Topic
      object.answers = []
      object.analyticDesc = i.AnalyticDesc
      for (let j of this.answersDetail) {
        if (j.QuestionId === i.QuestionId) {
          object.answers.push(j.AnswerContent)
        }
      }
      this.showData.push(object)
    }
  },
  data () {
    return {
      msg: '',
      questionsDetail: [],
      answersDetail: [],
      total: {
        question: '',
        answers: []
      },
      showData: [],
      letters: ['A', 'B', 'C', 'D'
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
div{
  ;
}
</style>
