<template>
  <div id="app" class="hero">
    <div class="hero-body">
      <h1 class="title">URL分析</h1>

      <p>输入：</p>
      <textarea class="textarea" placeholder="http://xx.cn/?type=0&a=b" rows="5" v-model="input"></textarea>

      <hr>
      <p>输出：</p>

      <div class="field is-horizontal" v-for="item in output" :key="item.key">
        <div class="field-label is-normal">
          <label class="label">{{item.key}}</label>
        </div>
        <div class="field-body">
          <div class="field">
            <p class="control is-expanded">
              <input class="input" type="text" v-model="item.val" style="width:500px" @keyup="getNewUrl">
              <input class="input" type="text" style="width:200px" placeholder="可填备注">
            </p>
          </div>
        </div>
      </div>



      <hr>
      <p>output new url：</p>
      <textarea class="textarea" placeholder="?type=0&a=b" rows="5" v-model="newUrl"></textarea>

    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      input: '',
      output: [],
      newUrl: '',
    }
  },
  methods: {
    analysis(url) {
      if (!url) return;

      const startIndex = url.indexOf('?');

      if (startIndex === -1) return;

      const params = url.slice(startIndex + 1).split('&');
      this.output = params.map(item => ({
        key: item.split('=')[0],
        val: item.split('=')[1],
      }));
    },

    getNewUrl() {
      const params = this.output.map((item) => (item.key + '=' + item.val));

      this.newUrl = '?' + params.join('&');
    }
  },
  watch: {
    input: function (newVal, oldVal) {
      this.analysis(newVal);
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}

h1, h2 {
  font-weight: normal;
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
