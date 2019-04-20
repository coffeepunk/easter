<template>
  <div>
    <form action="/" v-if="!codesValid">
      <h1>The codes</h1>
      <span>{{result}}</span>
      <div class="input-cards">
        <div v-for="(hunter, index) in hunters" :key="hunter.name+index" class="input-card">
          <h2>{{hunter.name}}</h2>
          <input type="text" maxlength="1" v-model="hunters[index].code" v-on:input="allCodes">
        </div>
      </div>
      <div v-if="validatingCodes">
        <loader/>
      </div>
    </form>
    <div v-if="codesValid">
      <h1>Välkommna till högkvarteret!</h1>

    </div>
  </div>
</template>

<script>
import loader from '../components/loader'
export default {
  name: 'home',
  components: {
    loader
  },
  data () {
    return {
      hunters: [
        {
          name: 'Elis',
          code: null
        },
        {
          name: 'Elna',
          code: null
        },
        {
          name: 'Elliot',
          code: null
        },
        {
          name: 'Cornelia',
          code: null
        }
      ],
      result: '',
      codesValid: false,
      validatingCodes: false
    }
  },
  methods: {
    allCodes: function () {
      const codes = this.hunters.map((hunter) => {
        return hunter.code
      })

      this.result = codes.join('')

      if (this.result === '1234') {
        this.validatingCodes = true
        const timeoutID = window.setTimeout(() => {
          this.codesValid = true
          this.validatingCodes = false
          window.clearTimeout(timeoutID)
        }, 2000)
      }
    }
  }
}
</script>

<style lang="scss">
  input {
    display: inline-block;
    border: 1px solid gray;
    border-radius: 7px;
    width: 80px;
    padding: 20px;
    font-size: 64px;
    text-align: center;
  }

  .input-cards {
    display: flex;
    flex-direction: row;
  }

  .input-card {

  }

  svg {
    width: 100px;
    height: 100px;
    margin: 20px;
    display:inline-block;
  }
</style>
