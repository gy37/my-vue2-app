<template>
  <div class="computed">
    <input v-model="message" />
    <div>{{ reversedMessage }}</div>
    <span>{{ fullName }}</span>
    <button v-on:click="updateFirstName">Update</button>
    <p>
      Ask a yes/no question:
      <input v-model="question" />
    </p>
    <p>{{ answer }}</p>
  </div>
</template>

<script>
import _ from 'lodash';
import axios from 'axios';
export default {
  name: 'ComputedWatch',
  data: function () {
    return {
      message: 'Hello World',
      firstName: 'Foo',
      lastName: 'Bar',
      question: '',
      answer: 'I cannot give you an answer until you ask a question!'
    }
  },
  computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('');
    },
    fullName: function () {
      return this.firstName + ' ' + this.lastName;
    }
  },
  watch: {
    question: function (newQ) {
      console.log('new question', newQ);
      this.answer = 'Waiting for you to stop typing...';
      this.debouncedAndGetAnswer();
    }
  },
  created: function () {
    console.log('created');
    // `_.debounce` 是一个通过 Lodash 限制操作频率的函数。
    // 在这个例子中，我们希望限制访问 yesno.wtf/api 的频率
    // AJAX 请求直到用户输入完毕才会发出。想要了解更多关于
    // `_.debounce` 函数 (及其近亲 `_.throttle`) 的知识，
    // 请参考：https://lodash.com/docs#debounce
    this.debouncedAndGetAnswer = _.debounce(this.getAnswer, 500);
  },
  methods: {
    updateFirstName: function () {
      this.firstName = 'Foo123';
    },
    getAnswer: function () {
      if (this.question.indexOf('?') === -1) {
        this.answer = 'Question must contain a question mark. ;-)';
        return;
      }
      this.answer = 'Thinking...';
      let that = this;
      axios.get('https://yesno.wtf/api')
        .then(function (response) {
          console.log(response);
          that.answer = _.capitalize(response.data.answer);
        })
        .catch(function (error) {
          console.error(error);
          that.answer = 'Error! Could not reach the API. ' + error;
        })
    },
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.computed {}

button {
  margin-left: 8px;
}
</style>
