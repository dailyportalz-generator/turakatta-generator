<template>
  <form class="select-question" @submit.prevent="handleSubmit">
    <dl>
      <dt>{{message}}</dt>
      <dd> 
      <template v-for="(choice, index) in choices">
        <div :key="choice">
          <div v-if="choice === '自由記入'">自由に書いてください</div>
          <input v-model="stringValue" v-if="choice === '自由記入'">
          <input
            v-else 
            required
            type="radio"
            v-model="selectedValue" 
            :value="index + 1"
          >
          <label v-if="!image && choice !== '自由記入'">{{ choice }}</label>
          <img :src="kibunImages[index]" v-if="image">
        </div>
      </template>
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
export default {
  props: {
    message: String,
    choices: Array,
    value: [Number, String],
    image: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      selectedValue: null,
      stringValue: ''
    }
  },
  computed: {
    kibunImages() {
      return [
        require("@/assets/s02.jpg"),
        require("@/assets/s03.jpg"),
        require("@/assets/s01.jpg"),
        require("@/assets/s04.jpg")
      ]
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('input', this.stringValue ? this.stringValue : this.selectedValue)
      this.$emit('next', this.selectedValue)
    },
    typeCheck(choice) {
      if (choice === '自由記入') {
        return null
      }
      return 'radio'
    }
  }
}
</script>

<style scoped>
.select-question {
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: dotted 1px #c6c6c6;
}

h3 {
  font-size: 1em;
}

dd {
  margin: 16px 0 0;
  padding: 0 0 8px 0;
}

button {
  width: 60px;
}

input[type='text'] {
  margin-right: 20px;
}

dt {
  color: #f60;
  font-weight: bold;
}
</style>