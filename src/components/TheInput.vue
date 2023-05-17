<template>
  <div>
    <label for="">Rekorunuz: </label>
    <input type="number" class="highestScore" v-model.number="score" @input="saveToLocalStorage" />
  </div>
</template>

<script>
export default {
  props: ['scored'],
  data() {
    return {
      score: ''
    };
  },
  mounted() {
    // Sayfa yenilendiğinde localStorage'dan değeri alır
    const storedData = localStorage.getItem('score');
    if(storedData) {
      this.score = storedData;
    }
  },
  methods: {
    saveToLocalStorage() {
      // Değer her güncellendiğinde localStorage'a kaydeder
      localStorage.setItem('score', this.score);
    }
  },
  watch: {
    score(newValue) {
      // score'da herhangi bir değişiklik olduğunda local storage'a kaydeder
      localStorage.setItem('score', newValue);
    }
  }
};
</script>

<style scoped>

  .highestScore{
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    border-radius: 8px;
    border: none;
  }

  label{
    color: #FFF;
    font-size: 16px;
    font-weight: bold;
  }

</style>