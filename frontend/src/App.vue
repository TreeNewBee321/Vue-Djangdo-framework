<template>
<div>
  <toggle-button :initial-status="shouldHint" ref="toggleButton"></toggle-button>
  <div>
    <input type="text" v-model.number="celsius" :class="tempClasses">℃<br>
    <button @click="increment()">+</button><button @click="decrement()">-</button><br>
    <input type="text" :value="fahrenheit" :class="tempClasses" readonly>℉<br>
    <button @click="log()">记录</button>
  </div>
  <div class="hint" v-if="shouldHint && danger">温度过高</div>
  <ol>
    <li v-for="(log, id) in logs" :key="log" :class="isDanger(log) ? 'danger' : ''">{{ isDanger(log) ? `过热${log}` : log }}℃</li>
  </ol>
</div>
</template>

<script>
import ToggleButton from './components/ToggleButton'
const THRESHOLD = 5

export default {
  components: {
    ToggleButton
  },
  data() {
    return {
      celsius: 0,
      logs: [],
      shouldHint: false
    }
  },
  computed: {
    tempClasses() {
      return this.danger() ? ['danger'] : []
    },
    fahrenheit() {
      return this.celsius * 8 / 5 + 32
    }
  },
  methods: {
    danger() {
      return this.celsius > THRESHOLD
    },
    increment() {
      this.celsius++
    },
    decrement() {
      this.celsius--
    },
    log() {
      this.logs.push(this.celsius)
    },
    isDanger(temp) {
      return temp > THRESHOLD
    }
  },
  mounted() {
    this.$refs.toggleButton.$on('toggle', (status) => {
      this.shouldHint = status
    })
  }
}
</script>

<style scoped>
div {
  text-align: center;
  font-size: 60px;
}

input {
  font-size: 60px;
}

button {
  font-size: 30px;
}

ol {
  width: 500px;
  margin: 0 auto;
}

.danger {
  background-color: red;
}

.hint {
  color: red;
}
</style>
