<template>
  <div class="hello">
    <h1>{{ quiz.title }}</h1>
    <div v-for="(question, index) in quiz.questions" v-bind:key="question.id">
      <div v-show="index === questionIndex">
        <h2>{{ question.text }}</h2>
        <ol>
          <li v-for="response in question.responses" v-bind:key="response.id">
            <label>
              <input type="radio" 
                     v-bind:value="response.choice"
                     v-bind:name="index"
                     v-model="picked"> {{ response.text }}
            </label>
          </li><br>
        </ol>
        <button v-on:click="check(question.correct, picked)">
          Selanjutnya
        </button>
      </div>
    </div>
    <div v-show="questionIndex === quiz.questions.length">
      <h2>
        Kuis Selesai
      </h2>
      <p>
        Jawaban benar : {{ score }} / {{ quiz.questions.length }}
      </p>
      <p>
        Nilai : {{ nilai() }}
      </p>
    </div>
  </div>
</template>

<script>
  var quiz = {
    title: "Kuis !!",
    questions : [
      {
        text: "Simbol Huruf yang ada pada topi mario di seri game Mario Bros adalah....",
        responses: [
          { text: 'S', choice: 'a' },
          { text: 'M', choice: 'b' },
          { text: 'L', choice: 'c' },
          { text: 'XL', choice: 'd' }
        ],
        correct: 'b'
      },
      {
        text: "Spiderman memanjat gedung dengan.... ",
        responses: [
          { text: 'Tangga', choice: 'a' },
          { text: 'Bapa Cleaning Service', choice: 'b' },
          { text: 'Tanganya yang lengket', choice: 'c' },
          { text: 'Lem Nasi', choice: 'd' }
        ],
        correct: 'c'
      },
      {
        text: "Gedung yang terkenal di Bandung adalah....",
        responses: [
          { text: 'Gedung Sate', choice: 'a' },
          { text: 'Gedung Lotek', choice: 'b'},
          { text: 'Gedung Petis', choice: 'c'},
          { text: 'Gedung Telkom', choice: 'd'}
        ],
        correct: 'a'
      },
      {
        text: "Batman adalah seseorang pahlawan yang ingin memiliki kemampuan yang sama dengan....",
        responses: [
          { text: 'Semut', choice: 'a'},
          { text: 'Babi Hutan', choice: 'b'},
          { text: 'Kucing', choice: 'c'},
          { text: 'Kelelawar', choice: 'd' }
        ],
        correct: 'd'
      },
      {
        text: "Menembak dalam KBBI berarti....",
        responses: [
          { text: 'melepaskan nafsu dan sebagainya dari hati', choice: 'a'},
          { text: 'melepaskan keinginan dan sebagainya dari perut', choice: 'b'},
          { text: 'melepaskan peluru dan sebagainya dari senjata api', choice: 'c' },
          { text: 'melepaskan aspirasi dan sebagainya dari pikiran', choice: 'd' }
        ],
        correct: 'c'
      },
    ]
  }


export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: function() {
    return {
      picked: '',
      show: true,
      quiz: quiz,
      questionIndex: 0,
      score: 0,
      userResponses: Array(quiz.questions.length).fill(false)
    }
  },
  methods: {
    check(correct, picked) {
      if (correct === picked) this.score++;
      this.questionIndex++;
      this.picked = null;
    },
    nilai: function() {
      return (100 / quiz.questions.length) * this.score;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
