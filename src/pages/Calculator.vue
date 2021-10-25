<template>
  <div>
    <div class="title">
      <h1>Le/Tip</h1>
    </div>

    <!-- Em Dolar -->

    <div v-on="calculateTip" v-if="enabled" class="calculator-content">
      <section class="calculator-content__entrance">
        <div class="calculator-content__entrance__convert">
          <p>EUR</p>
          <switches
            v-model="enabled"
            class="calculator-content__entrance__convert__switches"
          ></switches>
          <p>USD</p>
        </div>

        <!-- Valores de entrada -->
        <div class="calculator-content__entrance__total">
          <label>Valor</label>
          <div class="calculator-content__entrance__total__lbl">
            <span>$ </span>
            <input type="number" step="0.01" v-model="conta" />
          </div>
        </div>
        <div class="calculator-content__entrance__sliders">
          <div>
            <label>Gorjeta: </label>
            <span>{{ gorjeta }}%</span>
          </div>
          <div>
            <label>10 </label>
            <input
              type="range"
              min="10"
              max="20"
              step="1"
              value="10"
              v-model="gorjeta"
            />
            <label> 20</label>
          </div>
        </div>
        <div class="calculator-content__entrance__sliders">
          <div>
            <label for="">Pessoas: </label>
            <span>{{ pessoas }}</span>
          </div>
          <div>
            <label>2 </label>
            <input
              type="range"
              min="2"
              max="16"
              step="1"
              value="2"
              v-model="pessoas"
            />
            <label> 16</label>
          </div>
        </div>
      </section>

      <!-- Valores de saída -->
      <section class="calculator-content__exit">
        <div class="calculator-content__exit__result">
          <label>Conta:</label>
          <span>
            {{
              conta.toLocaleString("en", {
                style: "currency",
                currency: "USD",
              })
            }}</span
          >
        </div>

        <div class="calculator-content__exit__result">
          <label>Gorjeta: </label>
          <span>
            {{
              gorjetaCalculada.toLocaleString("en", {
                style: "currency",
                currency: "USD",
              })
            }}</span
          >
        </div>

        <div class="calculator-content__exit__result">
          <label>Total com Gorjeta: </label>
          <span>
            {{
              total.toLocaleString("en", {
                style: "currency",
                currency: "USD",
              })
            }}</span
          >
        </div>

        <div class="calculator-content__exit__result">
          <label>por Pessoa: </label>
          <span>
            {{
              porPessoa.toLocaleString("en", {
                style: "currency",
                currency: "USD",
              })
            }}</span
          >
        </div>

        <ConvertDolar :value="convertValueDolar" />
      </section>
    </div>

    <!-- Em Euro -->
    <div v-on="calculateTip" v-if="!enabled" class="calculator-content">
      <section class="calculator-content__entrance">
        <div class="calculator-content__entrance__convert">
          <p>EUR</p>
          <switches
            v-model="enabled"
            class="calculator-content__entrance__convert__switches"
          ></switches>
          <p>USD</p>
        </div>

        <!-- Valores de entrada -->
        <div class="calculator-content__entrance__total">
          <label>Valor</label>
          <div class="calculator-content__entrance__total__lbl">
            <span>€ </span>
            <input type="number" step="0.01" v-model="conta" />
          </div>
        </div>
        <div class="calculator-content__entrance__sliders">
          <div>
            <label>Gorjeta: </label>
            <span>{{ gorjeta }}%</span>
          </div>
          <div>
            <label>10 </label>
            <input type="range" min="10" max="20" step="1" v-model="gorjeta" />
            <label> 20</label>
          </div>
        </div>
        <div class="calculator-content__entrance__sliders">
          <div>
            <label for="">Pessoas: </label>
            <span>{{ pessoas }}</span>
          </div>
          <div>
            <label>2 </label>
            <input type="range" min="2" max="16" step="1" v-model="pessoas" />
            <label> 16</label>
          </div>
        </div>
      </section>

      <!-- Valores de saída -->
      <section class="calculator-content__exit">
        <div class="calculator-content__exit__result">
          <label>Conta:</label>
          <span>
            {{
              conta.toLocaleString("ue", {
                style: "currency",
                currency: "EUR",
              })
            }}
          </span>
        </div>

        <div class="calculator-content__exit__result">
          <label>Gorjeta: </label>
          <span>
            {{
              gorjeta.toLocaleString("ue", {
                style: "currency",
                currency: "EUR",
              })
            }}</span
          >
        </div>

        <div class="calculator-content__exit__result">
          <label>Total com Gorjeta: </label>
          <span>
            {{
              total.toLocaleString("ue", {
                style: "currency",
                currency: "EUR",
              })
            }}</span
          >
        </div>

        <div class="calculator-content__exit__result">
          <label>por Pessoa: </label>
          <span>
            {{
              porPessoa.toLocaleString("ue", {
                style: "currency",
                currency: "EUR",
              })
            }}</span
          >
        </div>

        <ConvertEuro :value="convertValueEuro" />
      </section>
    </div>
  </div>
</template>

<script>
import Switches from "vue-switches";
import ConvertDolar from "@/components/ConvertDolar.vue";
import ConvertEuro from "@/components/ConvertEuro.vue";

export default {
  components: {
    Switches,
    ConvertDolar,
    ConvertEuro,
  },

  data() {
    return {
      enabled: false,
      conta: 0,
      gorjeta: 10,
      gorjetaCalculada: 0,
      total: 0,
      porPessoa: 0,
      pessoas: 2,
      convertValueDolar: 0,
      convertValueEuro: 0,
    };
  },

  computed: {
    calculateTip() {
      let gorjetaCalculada = Number(this.conta) * Number(this.gorjeta / 100);
      this.gorjetaCalculada = gorjetaCalculada;

      let total = gorjetaCalculada + Number(this.conta);
      this.total = total;

      let porPessoa = total / Number(this.pessoas);
      this.porPessoa = porPessoa;

      let convertValueDolar = gorjetaCalculada * 5.65;
      this.convertValueDolar = convertValueDolar;

      let convertValueEuro = gorjetaCalculada * 6.5;
      this.convertValueEuro = convertValueEuro;

      return gorjetaCalculada;
    },
  },
};
</script>

<style lang="scss" scoped>
.title {
  display: flex;
  justify-content: center;
  padding: 35px 0;
  margin-bottom: 30px;

  h1 {
    font-weight: normal;
    font-size: 60px;
  }
}

.calculator-content {
  display: flex;
  justify-content: center;

  width: 100%;
  margin: 0 auto;
  max-width: 1170px;
  &__entrance {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 600px;
    font-size: 30px;

    &__convert {
      display: flex;
      align-items: center;
      padding: 20px 0;
      p {
        font-size: 18px;
        font-weight: 600;
      }
      &__switches {
        margin: 0 7px;
      }
    }
    &__total {
      display: flex;
      align-items: center;
      padding: 20px 0;
      label {
        font-size: 14px;
        font-weight: 600;
      }
      &__lbl {
        display: flex;
        align-items: center;
        margin-left: 5px;
        input {
          margin-left: 5px;
          padding: 7px 0;
          font-size: 20px;
          text-align: center;
          font-weight: 600;
          font-family: "Architects Daughter", cursive;
        }
      }
    }
    &__sliders {
      display: flex;
      flex-direction: column;
      padding: 20px 0;
      label {
        font-size: 14px;
        font-weight: 600;
      }
      span {
        font-size: 22px;
        font-weight: 600;
      }
      input[type="range"] {
        -wekit-appearance: none;
        appearance: none;
        width: 11em;
        height: 0.1em;
        display: inline-block;
        background-color: #000000;
      }
      input::-webkit-slider-thumb {
        -webkit-appearance: none;
        appearance: none;
        width: 25px;
        height: 25px;
        border-radius: 50%;
        background: #000000;
        cursor: pointer;
      }

      .estilo::-moz-range-thumb {
        width: 25px;
        height: 25px;
        border-radius: 50%;

        background: #2796ee;
        cursor: pointer;
      }
    }
  }
  &__exit {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 600px;
    font-size: 30px;

    &__result {
      display: flex;
      align-items: center;
      flex-direction: column;
      padding: 20px 0;
      label {
        font-size: 14px;
        font-weight: 600;
      }
      span {
        margin: 0 7px;
        font-size: 22px;
        font-weight: 600;
      }
    }
  }
}
</style>
