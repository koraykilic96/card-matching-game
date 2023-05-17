<template>
  <div class="board">
    
    <div class="deneme">
      <TheInput :scored="score" :key="componentKey"></TheInput>
      <div>
        <label for="pairCount">Kart Çifti Sayısı:</label>
        <input type="number" id="pairCount" v-model.number="pairCount" min="1" placeholder="Kart çifti sayısını girin">
      </div>
      <button class="generateCards" @click="generateCards">Kartları Oluştur</button>
    </div>
    <div class="card-grid" :style="gridStyle">
      <TheCard :flipped="card.flipped" :matched="card.matched" :id="card.id" v-for="(card, index) in cards" :key="index" @card-flipped="cardFlipped(card)">
        <template v-slot:back>
          <img :src="card.frontImage" alt="Card Front" />
        </template>
        <template v-slot:front>
          <img src="./../assets/back-image.jpg" alt="Card Back" />
        </template>
      </TheCard>
    </div>
  </div>
</template>
  
<script>
import TheCard from './TheCard.vue';
import TheInput from './TheInput.vue';

export default {
  components: {
    TheCard,
    TheInput
  },
  data() {
    return {
      pairCount: 0,
      cards: [],
      flippedCards: [],
      matchedCards: [],
      score: 0,
      componentKey: 0,
      columnCount: 4
    };
  },
  created() {
    this.shuffleCards();
    this.generateCards()
  },
  computed: {
    gridStyle() {
      return {
        'grid-template-columns': `repeat(${this.columnCount}, 1fr)`
      };
    }
  },
  methods: {
    shuffleCards() {
      // Fisher-Yates karıştırma algoritması
      for (let i = this.cards.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.cards[i], this.cards[j]] = [this.cards[j], this.cards[i]];
      }
    },
    generateCards() {
        this.cards = [];
        this.matchedCards = [];
        this.flippedCards = [];
        const values = [];

        if(this.pairCount>20){ //20 görsel kullanıldığı için 20 ile sınırlandırıldı.
          alert(`Girilen değer 20'den büyük olamaz`);
          return;
        }

        if(this.pairCount>=10){
          this.columnCount = this.pairCount/2
        }
        else {
          this.columnCount = 4
        }

        for (let i = 0; i < this.pairCount; i++) {
          values.push(i);
          values.push(i);
        }

        while (values.length > 0) {
          const randomIndex = Math.floor(Math.random() * values.length);
          const randomValue = values.splice(randomIndex, 1)[0];
          const id = this.cards.find(element => element.id == randomValue) ? randomValue+20 : randomValue
          this.cards.push({
            frontImage: require(`@/assets/card${randomValue+1}.jpg`),
            flipped: false,
            matched: false,
            id: id
          });
        }
    },
    cardFlipped(card) {
      this.cards = this.cards.map(item => {
        if (item.id == card.id) {
          item.flipped = true;
        }
        return item;
      })
      this.flippedCards.push(card);

      if (this.flippedCards.length === 2) {
        this.checkMatch();
      }
    },
    checkMatch() {
      const [card1, card2] = this.flippedCards;
      if (card1.frontImage === card2.frontImage) {
        // Eşleşme durumunda
        card1.matched = true;
        card2.matched = true;
        this.matchedCards.push(card1, card2);
        this.score += 10; // Puanı artır
      } else {
        // Eşleşme olmadığında
        setTimeout(() => {
          card1.flipped = false;
          card2.flipped = false;
        }, 1000);
        this.score -= 2; // Puanı azalt
      }

      this.flippedCards = [];

      // Tüm kartlar eşleşti mi kontrolü
      if (this.matchedCards.length === this.cards.length) {
        setTimeout(() => {
          alert(`Tebrikler! Tüm kartları eşleştirdiniz. Skorunuz: ${this.score}`);
          
          // Rekor alanı için kontrol
          if(this.score>localStorage.getItem('score'))
            {localStorage.setItem('score', this.score)
          }

          // Rekor alanını güncellemek için key değeri arttırılır
          this.componentKey += 1;
          this.resetGame();
        }, 500);
      }
    },
    resetGame() {
      // Kartları karıştır, oyunu sıfırla,  ve puanı sıfırla
      this.shuffleCards();
      this.generateCards();
      this.score = 0;
    },

  }
};
</script>
  
<style scoped>
.board {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80vh;
  background-image: url('./../assets/background.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

img {
  max-width: 100%;
  max-height: 100%;
}

.deneme {
  position: absolute;
  top: 110px;
  display: flex;
  justify-content: space-around;
  width: 100%;
}

.generateCards {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 8px;
}

#pairCount{
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
  