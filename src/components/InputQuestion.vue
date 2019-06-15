<template>
  <form class="input-question" @submit.prevent="handleSubmit()">
    <dl>
      <dt>まず、お名前をいれてください</dt>
      <dd>
        <input type="text" v-model="name">
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      title: 1
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('start', {
        name: this.name,
      })
    }
  }
}
</script>

<style scoped>
.input-question {
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