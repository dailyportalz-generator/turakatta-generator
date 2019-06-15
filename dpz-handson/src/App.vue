<template>
  <div id="app">
    <template>
      <InputQuestion
        key="start"
        v-if="step === 0"
        @start="handleStart"
      />

      <SelectQuestion
        key="question1"
        v-if="step === 1"
        v-model="questions.q1"
        @next="handleNext"
        :message="messageList[0]"
        :choices="choicesList[0]"
      />

      <SelectQuestion
        key="question2"
        v-if="step === 2"
        v-model="questions.q2"
        @next="handleNext"
        :message="messageList[1]"
        :choices="choicesList[1]"
      />

      <SelectQuestion
        key="question3"
        v-if="step === 3"
        v-model="questions.q3"
        @next="handleNext"
        :message="messageList[2]"
        :choices="choicesList[2]"
      />

      <SelectQuestion
        key="question4"
        v-if="step === 4"
        v-model="questions.q4"
        @next="handleNext"
        :message="messageList[3]"
        :choices="choicesList[3]"
      />

      <SelectQuestion
        key="question5"
        v-if="step === 5"
        v-model="questions.q5"
        @next="handleNext"
        :message="messageList[4]"
        :choices="choicesList[4]"
      />

      <SelectQuestion
        key="question6"
        v-if="step === 6"
        v-model="questions.q6"
        @next="handleNext"
        :message="messageList[5]"
        :choices="choicesList[5]"
      />

      <SelectQuestion
        key="question7"
        v-if="step === 7"
        v-model="questions.q7"
        @next="handleNext"
        :message="messageList[6]"
        :choices="choicesList[6]"
      />

      <SelectQuestion
        key="question8"
        v-if="step === 8"
        v-modelz="questions.q8"
        @next="handleNext"
        :message="messageList[7]"
        :choices="choicesList[7]"
      />

      <SelectQuestion
        key="question9"
        v-if="step === 9"
        :image="true"
        v-model="questions.q9"
        @next="handleNext"
        :message="messageList[8]"
        :choices="choicesList[8]"
      />
    </template>

    <OyasumiResult
      :step="step"
      :questions="questions"
      v-if="step === 10"
    />
  </div>
</template>

<script>
import InputQuestion from './components/InputQuestion.vue'
import SelectQuestion from './components/SelectQuestion.vue'
import OyasumiResult from './components/OyasumiResult.vue'
import { parse } from 'querystring'

export default {
  name: 'app',
  data() {
    return {
      step: 0,
      questions: {
        name: '',
        title: 1,
        q1: 1,
        q2: 1,
        q3: 1,
        q4: 1,
        q5: 1,
        q6: 1,
        q7: 1,
        q8: 1,
        q9: 1
      }
    }
  },
  components: {
    InputQuestion,
    SelectQuestion,
    OyasumiResult
  },
  mounted() {
    const params = parse(location.search.replace('?', ''))
    const isValid = ['name', 'title', 'q1', 'q2', 'q3', 'q4', 'q5', 'q6', 'q7', 'q8', 'q9'].every((val) => {
      if (!params[val]) {
        return false
      }
      if (val != 'name' && parseInt(params[val]) < 1) {
        return false
      }
      return true
    })
    if (isValid) {
      const questions = {
        name: params.name,
        title: parseInt(params.title),
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: params.q5,
        q6: parseInt(params.q6),
      }
      this.questions = questions
      this.step = 10
    }
  },
  methods: {
    handleNext(value) {
      if (this.step === 4 && value === 2) {
        this.step = 10
        return
      }
      if (this.step < 5 &&  this.step !== 0 && value === 1) {
        this.step = 5
        return
      }
      this.step ++
    },
    handleStart(startData) {
      this.questions.name = startData.name
      this.step++
    }
  },
  computed: {
    messageList() {
      return [
        '辛かった話を聞かせてくれませんか',
        'そんなこと言わずに教えてくださいよ',
        'えー、いいじゃないですか。教えてよー',
        'ほんと、教えてくれないとこの企画が成り立たないので頼みますよ',
        this.step6Message,
        'それはいつのことですか',
        'それはおぼえていますか？思い出しますか',
        'そのときあなたはどうしましたか',
        'そのときの気分に近い写真を選んでください'
      ]
    },
    step6Message() {
      return this.questions.q2 === 1 ? '具体的になにが辛かったのか教えてください' : 'ご協力ありがとうございます。ではお聞きします。辛かったことは？'
    },
    choicesList() {
      return [
        ['いいよ', 'やだ'],
        ['わかったよ', 'やだ'],
        ['しょうがないな', 'やだってば'],
        ['じゃあ、いいか', 'やだって言ってんだろ！'],
        ['カップ焼きそばのお湯を捨てること', '口内炎が痛いこと', '財布を落としたこと', '自由記入'],
        ['きょう', '今年', 'もっと前', '思い出したくもない'],
        ['昨日のことのように覚えている', '思い出すけど言いたくない', 'いまじゃいい冗談ですよ', '思い出したくないって言ってるじゃないか'],
        ['泣いた', '平静を装ったけどショックを受けた', '笑った', '踊った'],
        ['s02.jpg', 's03.jpg', 's01.jpg', 's04.jpg']
      ]
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}
</style>