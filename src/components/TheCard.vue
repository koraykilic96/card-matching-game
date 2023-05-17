<template>
  <div class="card" :class="{ flipped: isFlipped, matched: isMatched }" @click="flipCard">
    <div class="front">
      <slot name="front"></slot>
    </div>
    <div class="back">
      <slot name="back"></slot>
    </div>
  </div>
</template>
  
<script>
export default {
  props:{
    flipped: {
      type: Boolean,
      default: false,
    },
    matched: {
      type: Boolean,
      default: false,
    },
    id: {
      type: Number,
    }
  },
  computed: {
    isFlipped(){
      return this.flipped;
    },
    isMatched(){
      return this.matched;
    }
  },
  methods: {
    flipCard() {
      //Kartlara tıklandığında döndürmeyi sağlar
      if (!this.isFlipped && !this.isMatched) {
        var card={
          flipped : true,
          matched : this.matched,
          id: this.id,
          ...this
        }
        console.log(card)
        this.$emit('card-flipped', card);
      }
    },
  },
};
</script>

  
<style scoped>
.card {
  width: 100px;
  height: 100px;
  perspective: 600px;
  position: relative;
  transform-style: preserve-3d;
  cursor: pointer;
  transition: transform 0.3s;
}

.card.flipped {
  transform: rotateY(180deg);
}

.card.matched {
  cursor: default;
}

.card>div {
  backface-visibility: hidden;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 1px solid #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
}

.front {
  transform: rotateY(0deg);
}

.back {
  transform: rotateY(180deg);
}
</style>
  