<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <StackLayout>
          <maps
            :onMapReady="onMapReady" />
        </StackLayout>
    </Page>
</template>

<script>
  import Maps from '@/components/Maps'
  const Color = require('tns-core-modules/color')

  export default {
    components: {
      Maps
    },
    data() {
      return {
        msg: 'Hello World!'
      }
    },
    mounted () {
      this.$root.$emit('add')
    },
    methods: {
      onMapReady(args) {
          // Add Marker
          /* this.$root.$emit('addMarker', ([
              {
                  lat: 28.614809,
                  lng: 77.209086,
                  title: "Rajpath Area",
                  subtitle: "New Delhi is an urban district of Delhi which serves as the capital of India."
              },
              {
                  lat: 28.714809,
                  lng: 77.209086,
                  title: "Rajpath Area",
                  subtitle: "New Delhi is an urban district of Delhi which serves as the capital of India."
              },
              {
                  lat: 28.724809,
                  lng: 77.309086,
                  title: "Rajpath Area",
                  subtitle: "New Delhi is an urban district of Delhi which serves as the capital of India."
              }
          ])) */
          // Fix current location
          /* this.$root.$emit('fixCurrentLocation', {
            desiredAccuracy: 3,
            updateDistance: 10,
            maximumAge: 20000,
            timeout: 20000
          }) */
          // Add Polygon
          /* this.$root.$emit('addPolygon', {
            id: 1, // optional, can be used in 'removePolygons'
            fillOpacity: 0.7,

            // stroke-related properties are only effective on iOS
            strokeWidth: 8,
            strokeOpacity: 0.5,

            points: [
              {
                lat: 52.3923633970718,
                lng: 4.902648925781249
              },
              {
                lat: 52.35421556258807,
                lng: 4.9308013916015625
              },
              {
                lat: 52.353796172573944,
                lng: 4.8799896240234375
              },
              {
                lat: 52.3864966440161,
                lng: 4.8621368408203125
              },
              {
                lat: 52.3923633970718,
                lng: 4.902648925781249
              }
            ]
          }) */
          this.$root.$emit('addPolyline', {
            id: 1, // optional, can be used in 'removePolylines'
            color: '#000000', // Set the color of the line (default black)
            width: 5, // Set the width of the line (default 5)
            opacity: 1, //Transparency / alpha, ranging 0-1. Default fully opaque (1).
            points: [
                {
                    'lat': 52.3833160, // mandatory
                    'lng': 4.8991780 // mandatory
                },
                {
                    'lat': 52.3834160,
                    'lng': 4.8991880
                },
                {
                    'lat': 52.3835160,
                    'lng': 5.8991980
                },
                {
                    'lat': 52.3835160,
                    'lng': 6.8991980
                },
                {
                    'lat': 52.3835160,
                    'lng': 7.8991980
                }
            ]
          })
      }
    }
  }
</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
