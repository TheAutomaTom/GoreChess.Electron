<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div
    class="square"
    :class="`${square!.color}`"
    @click="handleClick"
  >
    <span
      :class="`${square!.piece?.color} ${isPickedUp ? 'is-picked-up' : ''}`"
    >
      {{ square!.piece?.icon }}
    </span>
  </div>
</template>

<script setup lang="ts">
import type { PropType} from "vue";
import { computed, ref } from "vue";
import type { Square } from "/@/models/GameboardModel";
import { useGameState } from "/@/state/Game.state";
const game$ = useGameState();
const props = defineProps({
  // eslint-disable-next-line vue/require-default-prop
  square: Object as PropType<Square>
});

const square = ref(props.square);

const handleClick = () => {
  console.log(`[Square.handleClick] Origin: ${square.value?.coordinate.file}${square.value?.coordinate.row}`);
    game$.HandleSelectSquare(square.value!);
};

const isPickedUp = computed((): boolean => {
  return game$.OriginSquare?.coordinate == square.value!.coordinate;
});

</script>
<style scoped lang="scss">

.square {
  text-align: center;
  vertical-align: middle;
  padding-top:15%;
}
.light-square {
  background-color: orangered;
}
.dark-square {
  background-color: darkslategrey;
}
.white-piece {
  color: white;
  // -webkit-text-stroke-width: 1px;
  // -webkit-text-stroke-color: gold;
  text-shadow: 2px 3px 2px black;
}
.black-piece {
  color: black;
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: grey;
  text-shadow: -2px -4px 2px white;
}
.is-picked-up {
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: gold;
}

</style>


