<template>
  <div>
    <form action="/" v-if="!codesValid">
      <h1>Bokstavskoden</h1>
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
      <p>Ni har löst första gåtan! Ni borde få ett lösenord skickat till er. Detta är inte det riktiga lösenordet utan till för att lura tjuvarna.</p>
      <p>Använd kodschemat för att få fram den riktiga koden som är lösenordet. Glöm inte att skriva ner det!!</p>
      <form action="">
        <h2 class="lbl-password-code">Lösenordskod</h2>
        <div class="input-codes">
          <div v-for="(code, index) in passCodes" :key="'ps'+index" class="input-code">
            <input type="text" maxlength="2" v-model="passCodes[index]" v-on:input="validatePassCodes">
          </div>
        </div>
        <div v-if="validatingPassCodes">
          <loader/>
        </div>
      </form>
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
      passCodes: new Array(8),
      hunters: [
        {
          name: 'Cornelia',
          code: null
        },
        {
          name: 'Elliot',
          code: null
        },
        {
          name: 'Elna',
          code: null
        },
        {
          name: 'Elis',
          code: null
        }
      ],
      result: '',
      codesValid: false,
      validatingCodes: false,
      validatingPassCodes: false,
      passCodesValid: false
    }
  },
  methods: {
    allCodes: function () {
      const codes = this.hunters.map((hunter) => {
        return hunter.code
      })

      this.result = codes.join('')

      if (this.result === 'izew') {
        this.validatingCodes = true
        const timeoutID = window.setTimeout(() => {
          this.codesValid = true
          this.validatingCodes = false
          window.clearTimeout(timeoutID)
        }, 5000)
      }
    },
    validatePassCodes: function () {
      const codes = this.passCodes.map((code) => {
        return code
      })

      this.result = codes.join('')
      if (this.result === '162719111011120') {
        this.validatingPassCodes = true
        const timeoutID = window.setTimeout(() => {
          this.passCodesValid = true
          this.validatingPassCodes = false
          this.$router.push({ path: '/about' })
          window.clearTimeout(timeoutID)
        }, 2000)
      }
    }
  }
}
</script>

<style lang="scss">
  body {
    margin: 0;
    font-size: 100%;
    line-height: 1.4;
    font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
    text-align: center;
  }

  .input-cards {
    display: flex;
    flex-direction: row;
    max-width: 700px;
    justify-content: space-around;
    align-items: center;
    margin: 0 auto;
  }

  .input-card > input {
    display: inline-block;
    border: 1px solid gray;
    border-radius: 7px;
    width: 80px;
    padding: 20px;
    font-size: 64px;
    text-align: center;
  }

  .input-codes {
    display: flex;
    flex-direction: row;
    max-width: 900px;
    justify-content: space-around;
    align-items: center;
    margin: 0 auto;
  }

  .input-code > input {
    display: inline-block;
    border: 1px solid gray;
    border-radius: 7px;
    width: 60px;
    padding: 10px;
    font-size: 52px;
    text-align: center;
  }

  svg {
    width: 100px;
    height: 100px;
    margin: 20px;
    display:inline-block;
  }

  .lbl-password-code {
    display: block;
  }

  .ipt-password-code {
    display: inline-block;
    padding: 10px 16px;
    font-size: 64px;
    letter-spacing: 12px;
    width: 400px;
  }
</style>
