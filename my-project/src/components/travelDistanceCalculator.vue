<template>
  <div>
  <MapContainer :center="mapCenter" :zoom="mapZoom">
    <TileLayer :url="mapTileUrl" :attribution="mapTileAttribution" />
    <Marker :lat-lng="directionsResponse?.startLatLng">
      <Popup>{{ directionsResponse?.start }}</Popup>
    </Marker>
    <Marker :lat-lng="directionsResponse?.endLatLng">
      <Popup>{{ directionsResponse?.end }}</Popup>
    </Marker>
  </MapContainer>
</div>
</template>

<script>
//import "leaflet/dist/leaflet.css";
//import L from 'leaflet';

import { MapContainer, TileLayer, Marker, Popup } from 'vue3-leaflet';


import { MapQuest } from '@mapquest/mapquest-sdk-v1';




  export default {
    name: 'travelDistanceCalculator',

    components:{
     MapContainer,TileLayer,Marker,Popup
    },

    data() {
      return {
        mapCenter: [0, 0],
        mapZoom: 7,
        mapTileUrl: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        mapTileAttribution: '&copy; OpenStreetMap contributors',
        directionsService: null,
        directionsResponse: null,
      };
    },
    methods: {
      async getDirections() {
        const mq = new MapQuest({
          key: 'pnUH96ywSmESijiHTfKUDP7cuZio3lZC',
        });
        this.directionsService = new mq.Directions();
        const options = {
          timeOverage: 25,
          maxRoutes: 3,
        };
        const start = '350 5th Ave, New York, NY 10118';
        const end = 'One Liberty Plaza, New York, NY 10006';
        const response = await this.directionsService.route({
          start: start,
          end: end,
          options: options,
        });
        this.directionsResponse = response;
      },
    },
    mounted() {
      this.getDirections();
    },
  };
</script>
