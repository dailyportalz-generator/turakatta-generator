<template>
  <div class="oyasumi-result">
    <div class="oyasumi-result_main">
      <div>
        <div class="oyasumi-result__message">
          <div class="border-box">
            <p>
              <p class="orange-text"> 
                {{questions.name}} インタビュー「「辛かったこと、もしくはそうでないこと」
              </p>
              <span class="head">多忙を極める {{questions.name}}氏 に奇跡的にインタビューのアポイントメントをとることができた。しかし我々に与えられた時間は30分。
                <br>
                そのあいだに {{questions.name}}氏の根幹をなしていると思われる過去の体験、しかもネガティブな面について質問をぶつけてみたい。これまで語られなかった意外な一面を見ようという狙いである。（収録：2008年11月6日 都内某所にて）
              </span>
            </p>
          </div>
          
          <template v-if="questions.q4 !== 2">
            <div class="border-box">
              <div class="box">
                <div class="question">
                  －－－これまでのちょっと思い出したくない、辛かったことについてお話しを聞きたいのですが
                </div>
                <div class="answer"> {{ firstQuestion }} </div>
              </div>
              <div class="box">
                <div class="question">
                  －－－ありがとうございます。具体的にはどんなことでしょうか。
                </div>
                <div class="answer"> ………。いざとなると言いにくいね。ストレートに言ってしまうと{{ secondQuestion }}ことかな。 </div>
              </div>
              <div class="box">
                <div class="question">
                  －－－それは大変でしたね。いつごろのお話ですか？
                </div>
                <div class="answer"> {{ thirdQuestion }}</div>
              </div>
              <div class="box">
                <div class="question">
                  －－－ そのことはいまでも思い出しますか？
                </div>
                <div class="answer"> {{ fourthQuestion }}</div>
              </div>
            </div>
            <div class="border-box">
              <div class="box">
                <div class="question">
                  －－－ 実際、その場の{{ questions.name }}さんはどうされたんでしょうか？
                </div>
                <div class="answer"> {{ fifthQuestion }}</div>
              </div>
              <div class="box">
                <div class="question">
                  －－－ では最後に、どうやって立ち直ったかを教えてください。
                </div>
                <div class="answer"> {{ sixthQuestion }}</div>
              </div>
              <div class="box">
                <div class="question">
                  －－－今日はどうもありがとうございました。 
                </div>
                <div class="answer"> こちらこそ。</div>
              </div>
            </div>
            
          </template>
          <template v-else> 
            <div class="question">
              －－－辛かったことを教えてください
            </div>
            <div class="answer">やっぱりこのインタビューはなかったことにしてもらえますか。どうしても話したくないので。プンスカ</div>
            <div class="question">{{ questions.name }}氏は怒って帰ってしまった。インタビューは失敗です。やりなおしてください。</div>
          </template>
          <p class="oyasumi-result_build">
            <button type="button" @click="handleClickRestart">もう一度つくる</button>
          </p>
          <p class="oyasumi-result_share">
            <input type="text" class="oyasumi-result_shareurl" readonly :value="shareUrl">
            <a target="_blank" :href="twitterUrl">つぶやく</a>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { stringify } from 'querystring'

export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    firstQuestion() {
      if (this.questions.q1 === 1) {
        return 'いいですよ。お話しします。辛いと思ってひとりでためこむよりも人に話すと楽になるものですしね。'
      }
      if (this.questions.q2 === 1) {
        return '辛かった話ですか…。あまり乗り気がしないけど、わかりました。みんなをどんよりさせるようなことを言っちゃおうかな（笑）'
      }
      if (this.questions.q3 === 1) {
        return '辛かったことか（遠くを見ながら）。あるにはあるんだけど、これは言わないといけないんだよね。よし、覚悟を決めました。'
      }
      if (this.questions.q4 === 1) {
        return 'いや、やっぱり辛かったのでちょっとお話しできないです。（帰ろうとするのを10分かけて説得）…わかりました。そこまで言われるとお話ししないわけにはいかないですね。'
      }
      return ''
    },
    secondQuestion() {
      switch (this.questions.q5) {
        case 1:
          return 'カップ焼きそばを作るときにお湯と一緒に麺を流してしまった'
        case 2:
          return '口内炎が痛い'
        case 3:
          return '財布を落とした'
        default: 
          return this.questions.q5
      }
    },
    thirdQuestion() {
      switch (this.questions.q6) {
        case 1:
          return '遠い昔の話のように話をしているけど、実は今日のことなんです。こうやって折り合いをつけようとしているのかもしれませんね。'
        case 2:
          return '最近の話ですよ。たぶん今年に入ってからのことじゃないかな。まだ１年経ってないです。'
        case 3:
          return '結構むかしのはなしですね。前のワールドカップやってるころです。だけど、妙に鮮明に覚えてるな。脳に刻みこまれているのかな。'
        case 4:
          return 'まったくいつのことか覚えてないんだ。昨日のことだった気もするし、10年前かもしれない…。思い出したくないという無意識の働きがあるんだと思う。'
      }
    },
    fourthQuestion() {
      switch (this.questions.q7) {
        case 1:
          return '毎日、とまではいかないけどかなり頻繁に思い出すよ。忘れようとしているけど、忘れたくないって気持ちもあるのかもしれない。人間はアンビバレンツな生き物だから。'
        case 2:
          return '……。実はしょっちゅう思い出すし、そのときの様子は鮮明に覚えている。うまく言えないんだけど、内蔵がひっくりがえるような衝撃だった。うまく言えてないね（笑）'
        case 3:
          return '実はきょう、こうやって話をするまで正直忘れかけていたよ。人に話をするときだけ思い出すってことか……。すっかり昇華していい話のネタになってくれているってことじゃないかな。'
        case 4:
          return '思い出さない！すっかり忘れた！ 思い出させないでくださいよ。まったく覚えてないって言ってるじゃないですか！ ♪ラララー'
      }
    },
    fifthQuestion() {
      switch (this.questions.q8) {
        case 1:
          return '平然としていたけどいつのまにか目に涙がたまっていました。ありていに言えば泣いたってことになるのかな。恥ずかしいな。これ秘密にしておいてよ。'
        case 2:
          return 'そのときは「あーあ」ぐらいの気持ちだったんですが、あとから徐々にダメージが来ましたね。やっぱりショックだったのかもしれません。'
        case 3:
          return 'とっさにどうしたと思いますか？声を出して笑っていたんですよ。人間、辛いことも一線を越えるとひっくり返るのだなと思いました。うひゃひゃひゃ。'
        case 4:
          return '不思議なことにいつの間にか踊ってました。無意識に体を動かして耐えようとしたのかもしれません。ほら、高校時代ずっとダンスをやっていたからさ。 ♪ラララー'
      }
    },
    sixthQuestion() {
      switch (this.questions.q9) {
        case 1:
          return 'ひたすら食べてごまかしました。どんなに辛いことがおきてもカレーはうまい。そう思いました。裏切らりませんね。スパイスは。'
        case 2:
          return '我を忘れて体を動かしました。トランス状態でした。ふだんは人の目を気にして生きているのに、あのときだけは気にならなかった。逆に言えば、それだけショックだったってことですよね。逆に。'
        case 3:
          return '人に助けてもらいました。その人とどういう関係かってことはこの場では言えないのですが。例えて言うなら長い棒を持った影みたいな人でした。人という字は助け合いですね。あ、いまくさいこと言っちゃった。'
        case 4:
          return 'しばらくぼんやりしていましたね。暗いトンネルを眺めていたような気持ちです。時間が解決するというのは本当ですね。おかげでツタヤの延滞金が大変で（と言って机を叩く） 思い出させないでくださいよ。'
      }
    },
    shareUrl() {
      const shareData = {
        ...this.questions.target,
        ...this.questions,
        target: null,
        share: 1
      }
      delete shareData.target
      return `https://dailyportalz.jp/kiji/turakatta-hanashi-generator?${stringify(
        shareData
      )}`
    },
    twitterUrl() {
      return `https://twitter.com/intent/tweet?text=辛かった話ジェネレーター&url=${encodeURIComponent(
        this.shareUrl
      )}`
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, '')
    }
  }
}
</script>

<style scoped>
img {
  user-select: none;
}

.orange-text {
  font-weight: bold;
  color: #f60;
}

.head {
  color: #600;
}

.box {
  margin: 1em;
}

.border-box {
  border: 1px solid #222;
  padding: 10px;
  margin-bottom: 10px;
}

.oyasumi-result {
  width: 526px;
  margin: 0 auto;
}

.oyasumi-result_main {
  font-size: 0;
}

.oyasumi-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
}

.answer {
  color: #c00;
}

.oyasumi-result__message p:first-child {
  margin-top: 0;
}

.oyasumi-result_build {
  text-align: right;
}

.oyasumi-result_share {
  font-size: 12px;
}

.oyasumi-result_shareurl {
  width: 100%;
}

.oyasumi-result_share {
  display: flex;
  align-items: center;
}

input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>