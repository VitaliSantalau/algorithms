<script setup lang="ts">
import { computed, ref, type Ref } from 'vue';


// NOTE: set initial variables
const initialArray: number[] = [2, 9, 0, 5, 1];

const initialItemsIndexPosition = () => initialArray.reduce((acc, item, index) => {
  acc[item] = index;
  return acc;
}, {} as { [index: number]: number });

const itemSize = 100;
const gap = 10;
const itemColor = '#d8ccbd';
const currentItemColor = '#daa666';

const delayDuration = 1000; // NOTE: ms


// NOTE: set refs
const currentItemValue = ref<number>(initialArray[0]);

const itemsIndexPosition: Ref<{ [index: number]: number }> = ref(initialItemsIndexPosition())

const isSorting = ref<boolean>(false);
const isCanStart = ref<boolean>(true);


// NOTE: set methods
const delay = (ms: number): Promise<unknown> => 
  new Promise(resolve => setTimeout(resolve, ms));

const toSort = async (arr: number[]): Promise<void> => {
  isSorting.value = true;

  // NOTE: implement bubble sort algorithm
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i; j++) {
      // NOTE: set current value to apply the style as a handled value
      currentItemValue.value = arr[j];
      await delay(delayDuration); // NOTE: for good look

      const isNeedSwap = arr[j] > arr[j+1];

      if (isNeedSwap) {
        [arr[j], arr[j+1]] = [arr[j+1], arr[j]]; // NOTE: swap

        // NOTE: change offset index, to implement moving
        itemsIndexPosition.value[arr[j]] = j;
        itemsIndexPosition.value[arr[j+1]] = j+1;

        await delay(delayDuration); // NOTE: for good look
      }
    }
  }
  isSorting.value = false;
};

const startSorting = () => {
  isCanStart.value = false;
  toSort([...initialArray]);
};

const resetSorting = () => {
  itemsIndexPosition.value = initialItemsIndexPosition();
  currentItemValue.value = initialArray[0];
  isCanStart.value = true;
}

const itemStyle = (item: number) => {
    const offset = itemsIndexPosition.value[item] * (itemSize + gap);
    const color = item === currentItemValue.value ? currentItemColor : itemColor;

    return {
      'translate': `${offset}px`,
      'background': color,
      'width': `${itemSize}px`,
      'height': `${itemSize}px`,
    }
};

const containerStyle = computed(
  () => {
    return {
      'width': `${(itemSize + gap) * initialArray.length}px`,
      'height': `${itemSize}px`,
    }
  }
)
</script>

<template>
  <div>
    <h1 class="title">Bubble Sort Algorithm</h1>
    <div class="wrapper">
      <section>
        <div class="code-example">
        <pre>
          <code>
for (let i = 0; i &lt; arr.length; i++) {
  for (let j = 0; j &lt; arr.length - i; j++) {
    
    const isNeedSwap = arr[j] > arr[j+1];

    if (isNeedSwap) {
      [arr[j], arr[j+1]] = [arr[j+1], arr[j]];
    }
  }
}
          </code>
        </pre>
  </div>
      </section>
      <section>
        <div class="container" :style="containerStyle">
          <div
            v-for="(item, index) in initialArray" 
            :key="index"
            class="arrayItem"
            :style="itemStyle(item)"
          >
            {{ item }}
          </div>
        </div>
        <button @click="startSorting" :disabled="!isCanStart">Start</button>
        <button @click="resetSorting" :disabled="isSorting">Reset</button>
      </section>
    </div>
  </div>
</template>

<style scoped>
  .title {
    text-align: center;
    margin: 1rem 0 3rem 0;
    font-size: 36px;
    font-weight: 600;
  }
  .wrapper {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }

  section {
    margin: 1rem auto;
  }

  .container {
    position: relative;
    margin-top: 2rem;
  }

  .arrayItem {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 46px;
    border-radius: 50%;
    transition: 1s;
  }

  button {
    margin-top: 1rem;
  }
</style>
