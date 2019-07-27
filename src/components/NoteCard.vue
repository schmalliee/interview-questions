<template>
  <div class="notecard" @click="flipped = !flipped">
    <transition name="flip">
      <div class="card_front" v-if="!flipped" key="card_front">
        <slot name="front"></slot>
      </div>
      <div class="card_back" v-else key="card_back">
        <slot name="back"></slot>
      </div>
    </transition>
  </div>
</template>

<script>
  export default {
    name: "NoteCard",
    data() {
      return {
        flipped: false
      }
    },
  }
</script>

<style scoped>
.notecard {
  pointer-events: all;
  cursor: pointer;
}

.card_front, .card_back {
  height: 300px;
  padding: 20px;
  box-sizing: border-box;
  text-align: center;
  background:#2d3058;
  color: white;
}

.card_front {
  z-index: 1;
  font-size: inherit;
  font-family: inherit;
  padding: 0.5em 1em;
  outline: none;
  border: none;
}

.card_front:hover {
  animation: jelly 0.5s;
}

@keyframes jelly {
  0%,
  100% {
    transform: scale(1, 1);
  }
  25% {
    transform: scale(0.9, 1.1);
  }
  50% {
    transform: scale(1.1, 0.9);
  }
  75% {
    transform: scale(0.95, 1.05);
  }
}

.flip-enter-active, .flip-leave-active {
  transition: rotate(180deg);
}
.flip-enter, .flip-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>