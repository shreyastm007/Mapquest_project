<template>
  <div>
    <form>

      <!-- <input type="search" id="place-search-input" placeholder="Start Searching..."/> -->

      <label>Starting Address:</label>
      <input type="text" v-model="startAddress">
      <label>Ending Address:</label>
      <input type="text" v-model="endAddress">
      <button type="button" @click="calculateDistance">Calculate Distance</button>
    </form>
    <p v-if="distance">Distance: {{ distance }} miles</p>
  </div>
</template>

<script>
import { reactive } from 'vue';
import { route } from 'mapquest-api';


//import MapQuestAPI from 'mapquest-api';

export default {

  setup() {
    const state = reactive({
      startAddress: '',
      endAddress: '',
      distance: null
    });

    const calculateDistance = () => {
  route({
    key: 'pnUH96ywSmESijiHTfKUDP7cuZio3lZC',
    from: state.startAddress,
    to: state.endAddress
  }).then(response => {
    state.distance = response.route.distance;
  }).catch(error => {
    console.log("error");
    console.error(error);
  });
};




    return {
      ...state,
      calculateDistance
    };
  }
}
</script>
