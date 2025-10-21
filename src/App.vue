<script setup lang="ts">
import { ref, computed } from "vue";
import Beverage from "./components/Beverage.vue";
import { temps, currentTemp, creamers, bases, syrups } from "./stores/beverage";

const currentBase = ref(bases.value[0].name);
const currentCreamer = ref(creamers.value[0].name);
const currentSyrup = ref(syrups.value[0].name);

const selectedBaseColor = computed(() => 
  bases.value.find((b) => b.name === currentBase.value)?.color || "#8B4513" );
const selectedCreamerColor = computed(() => 
  creamers.value.find((c) => c.name === currentCreamer.value)?.color || "transparent"
);
const selectedSyrupColor = computed(() => 
  syrups.value.find((s) => s.name === currentSyrup.value)?.color || "#c6c6c6"
);
</script>

<template>
  <div>
    <Beverage
      :isIced="currentTemp === 'Cold'"
      :selectedBaseColor="selectedBaseColor"
      :selectedCreamerColor="selectedCreamerColor"
      :selectedSyrupColor="selectedSyrupColor"
    />

    <ul>
      <li>
        <template v-for="temp in temps" :key="temp">
          <label>
            <input type="radio" name="temperature" v-model="currentTemp" :value="temp" />
            {{ temp }}
          </label>
        </template>
      </li>

      <li>
        <template v-for="cream in creamers" :key="cream.id">
          <label>
            <input type="radio" name="creamer" v-model="currentCreamer" :value="cream.name" />
            {{ cream.name}}
          </label>
        </template>
      </li>

      <li>
        <template v-for="base in bases" :key="base.id">
          <label>
            <input type="radio" name="base" v-model="currentBase" :value="base.name" />
            {{ base.name }}
          </label>
        </template>
      </li>

      <li>
        <template v-for="syrup in syrups" :key="syrup.id">
          <label>
            <input type="radio" name="syrup" v-model="currentSyrup" :value="syrup.name" />
            {{ syrup.name }}
          </label>
        </template>
      </li>
    </ul>
  </div>
</template>


<style lang="scss">
body,
html {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  background-color: #6e4228;
  background: linear-gradient(to bottom, #6e4228 0%, #956f5a 100%);
}
ul {
  list-style: none;
}
</style>
