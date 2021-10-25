<template>
  <div>
    <div class="title">
      <h1>Le/Tip</h1>
    </div>

    <div class="container-content">
      <section class="container-content__entrance">
        <div class="container-content__entrance__convert">
          <p>EUR</p>
          <switches
            v-model="enabled"
            class="container-content__entrance__convert__switches"
          ></switches>
          <p>USD</p>
        </div>
        <div class="container-content__entrance__total">
          <label>Valor</label>
          <div class="container-content__entrance__total__lbl">
            <span>$</span>
            <input type="number" value="0.00" v-model="bill" />
          </div>
        </div>
        <div class="container-content__entrance__sliders">
          <div>
            <label>Gorjeta: </label>
            <span>{{ tipPercent }}%</span>
          </div>
          <div>
            <label>10 </label>
            <input
              type="range"
              min="10"
              max="20"
              step="1"
              value="10"
              v-model="tipPercent"
            />
            <label> 20</label>
          </div>
        </div>
        <div class="container-content__entrance__sliders">
          <div>
            <label for="">Pessoas: </label>
            <span>{{ numPeople }}</span>
          </div>
          <div>
            <label>2 </label>
            <input
              type="range"
              min="2"
              max="16"
              step="1"
              value="2"
              v-model="numPeople"
            />
            <label> 16</label>
          </div>
        </div>
      </section>

      <section class="container-content__exit">
        <div class="container-content__exit__result">
          <label for="bill">Conta:</label>
          <span>${{ bill }}</span>
        </div>

        <div class="container-content__exit__result">
          <label>Gorjeta: </label>
          <span>${{ totalTip }}</span>
        </div>

        <div class="container-content__exit__result">
          <label>Total com Gorjeta: </label>
          <span>${{ totalAmount }}</span>
        </div>

        <div class="container-content__exit__result">
          <label>por Pessoa: </label>
          <span>${{ totalPerPeson }}</span>
        </div>
        <!-- <button @click="calculateTip">add</button> -->
        <Convert />
      </section>
    </div>
  </div>
</template>

<script>
import Switches from "vue-switches";
import Convert from "@/components/Convert.vue";

export default {
  components: {
    Switches,
    Convert,
  },
  data() {
    return {
      enabled: false,
      bill: "",
      billTotal: "",
      tipPercent: "",
      totalTip: "",
      numPeople: "",
      totalAmount: "",
      totalPerPeson: "",
      numPeople: "",
      noOfPeople: "",
    };
  },

  watch: {
    billTotal() {
      totalAmount = this.totalTip + this.bill;
      console.log("aqui");
    },
  },

  // mounted:{
  // calculateTip()
  // },
  computed: {
    calculateTip() {
      totalTip = this.bill * (this.tipPercent / 100);
      // return totalTip;
      console.log(tip);
    },
    calculateTipPerson() {
      totalPerPeson = this.totalTip / this.noOfPeople;
      return;
    },
    calculateTotalPerson() {
      totalPerPeson = this.totalAmount / this.noOfPeople;
      return;
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

.container-content {
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
