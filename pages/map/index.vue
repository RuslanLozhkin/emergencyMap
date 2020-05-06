<template>
  <v-card class="mt-4 mx-auto" max-width="90%">
    <v-toolbar color="info" dark flat dense cad>
      <v-toolbar-title class="mx-auto">
        <h2>
          Emergency Map
        </h2>
      </v-toolbar-title>
    </v-toolbar>
    <v-card-text>
      <v-row>
        <v-col id="map" />
      </v-row>
      <div class="calculation-box">
        <p><strong ref="calculatedarea">{{ showAnswer }}</strong></p><p>(square meters)</p>
      </div>
    </v-card-text>
  </v-card>
</template>

<script>
import mapboxgl from 'mapbox-gl'
import 'mapbox-gl/dist/mapbox-gl.css'
import MapboxDraw from '@mapbox/mapbox-gl-draw/dist/mapbox-gl-draw'
import * as turf from '@turf/turf'

export default {
  data () {
    return {
      access_token: 'pk.eyJ1IjoicnVzbGFubG96aGtpbiIsImEiOiJjazl0c2hocXcxZ3plM2xxY29xOHN5amZ0In0.HTWe6TJtqZxtJ9IzihaUbA',
      map: {},
      draw: {},
      answer: null
    }
  },
  mounted () {
    this.createMap()
  },
  //   updated () {
  //     this.map.on('draw.create', updateArea)
  //     this.map.on('draw.delete', updateArea)
  //     this.map.on('draw.update', updateArea)
  //   },
  methods: {
    createMap () {
      mapboxgl.accessToken = this.access_token
      this.map = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/streets-v11',
        zoom: 11,
        center: [32.6178000, 46.6558100]
      })
      this.draw = new MapboxDraw({
        displayControlsDefault: false,
        controls: {
          line_string: true,
          polygon: true,
          point: true,
          trash: true
        }
      })
      this.map.addControl(new mapboxgl.NavigationControl(), ['top-left'])
      this.map.addControl(this.draw, ['top-left'])
    },
    showAnswer () {
      const data = this.draw.getAll()
      if (data.features.length > 0) {
        const area = turf.area(data)
        this.answer = Math.round(area * 100) / 100
      }
      return this.answer
    }
  }
}
</script>

<style scoped>
     .mapboxgl-ctrl.mapboxgl-ctrl-attrib {
        display: none;
     }
     #map {
        width: 100%;
        min-height: 70vh;
        position: relative;
    }
    .calculation-box {
        color: black;
        height: 90px;
        width: 150px;
        position: absolute;
        bottom: 40px;
        left: 10px;
        background-color: rgba(255, 255, 255, 0.7);
        padding: 15px;
        text-align: center;
    }
    p {
        font-family: 'Open Sans';
        margin: 0;
        font-size: 13px;
    }
</style>
