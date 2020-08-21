<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
     <!--整个题目+答案-->
    <div style="display: block" v-for="(item,key) in showData" v-bind:key="key">
      <p style="margin-bottom: 0;text-align: left;font-size: medium;font-weight: bold"
         v-html="(key+1)+'. '+item.question"></p>
      <p style="margin-bottom: 1px;margin-top: 1px;text-align: left; font-size: small" v-for="(answer,i) in item.answers" v-bind:key="i" v-html="letters[i]+'.'+answer"></p>
      <p style="margin-bottom: 0;text-align: left;font-size: small;font-weight: bold"> 正确答案:</p>
      <p style="margin-bottom: 0;text-align: left;font-size: small; " v-html="item.realAnswer.toString()"></p>
      <p style="margin-bottom: 0;text-align: left;font-size: small;font-weight: bold"> 解析:</p>
      <p style="margin-bottom: 0;text-align: left;font-size: small; " v-html="item.analyticDesc"></p>
    </div>
  </div>
</template>

<script>
import exam from '../../static/2020年《经济法》押题卷（五）'

export default {
  name: 'Home',
  mounted: function () {
    this.questionsDetail = exam.Topic
    this.answersDetail = exam.Answer
    // 遍历所有题目
    for (let i of this.questionsDetail) {
      let object = Object()
      object.question = i.Topic
      object.answers = []
      object.analyticDesc = i.AnalyticDesc
      object.realAnswer = []
      // 拿到正确答案,如果多选,按逗号分开
      let answerIds = i.AnswersIds.split(',')
      let answerEntities = []
      // 循环所有答案,匹配当前题目的questionId
      for (let j of this.answersDetail) {
        if (j.QuestionId === i.QuestionId) {
          object.answers.push(j.AnswerContent)
          answerEntities.push(j)
        }
      }
      // 遍历正确答案,从待选答案中匹配出下标,再从letters数组中取选项
      for (let l of answerIds) {
        for (let k = 0; k < answerEntities.length; k++) {
          if (answerEntities[k].AnswerID === l) {
            object.realAnswer.push(this.letters[k])
          }
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
