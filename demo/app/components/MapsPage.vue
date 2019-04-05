<template>
  <Page>
    <ActionBar title="nsvue-maps">
      <NavigationButton text="Go back" android.systemIcon="ic_menu_back" @tap="$navigateBack" />
    </ActionBar>
    <GridLayout>
      <maps
        :onMapReady="onMapReady" />
    </GridLayout>
  </Page>
</template>

<script>
import Maps from '@/components/Maps'

const geolocation = require("nativescript-geolocation")

export default {
  props: {
    command: {
      type: String,
      required: true,
      default: () => { return ''}
    },
    config: {
      type: Object,
      required: true,
      default: () => { return {} }
    }
  },
  components: {
    Maps
  },
  methods: {
    onMapReady(args) {
      switch (this.command) {
        case 'SHOW_CURRENT_LOCATION':
          geolocation.getCurrentLocation({desiredAccuracy: 3, updateDistance: 10, maximumAge: 20000, timeout: 20000})
          .then((location) => {
            args.map.animateCamera({
              target: {
                lat: location.latitude,
                lng: location.longitude
              },
              zoomLevel: 20,
              altitude: 2000, // iOS (meters from the ground)
              bearing: 270, // Where the camera is pointing, 0-360 (degrees)
              tilt: 50,
              duration: 5000
            })
          })
          break
        case 'ADD_MARKERS':
          // 15.283217, 73.985397
          // 15.288601, 73.990299
          // 15.281529, 73.991818
          // 15.283677, 73.995149
          args.map.addMarkers([
            {
              lat: 15.283217,
              lng: 73.985397,
              title: 'Location 1',
              subtitle: 'Description of this location',
              selected: true, // makes the callout show immediately when the marker is added (note: only 1 marker can be selected at a time)
              onCalloutTap: function(){console.log("'Nice location' marker callout tapped");}
            },
            {
              lat: 15.288601,
              lng: 73.990299,
              title: 'Location 2',
              subtitle: 'Description of this location',
              selected: true, // makes the callout show immediately when the marker is added (note: only 1 marker can be selected at a time)
              onCalloutTap: function(){console.log("'Nice location' marker callout tapped");}
            },
            {
              lat: 15.281529,
              lng: 73.991818,
              title: 'Location 3',
              subtitle: 'Description of this location',
              selected: true, // makes the callout show immediately when the marker is added (note: only 1 marker can be selected at a time)
              onCalloutTap: function(){console.log("'Nice location' marker callout tapped");}
            },
            {
              lat: 15.283677,
              lng: 73.995149,
              title: 'Location 4',
              subtitle: 'Description of this location',
              selected: true, // makes the callout show immediately when the marker is added (note: only 1 marker can be selected at a time)
              onCalloutTap: function(){console.log("'Nice location' marker callout tapped");}
            }
          ]).then(() => {
            args.map.animateCamera({
              target: {
                lat: 15.283217,
                lng: 73.985397
              },
              zoomLevel: 50,
              altitude: 2000, // iOS (meters from the ground)
              bearing: 0, // Where the camera is pointing, 0-360 (degrees)
              tilt: 0,
              duration: 5000
            })
          })
          break
        case 'TRACK_ME':
          geolocation.getCurrentLocation({desiredAccuracy: 3, updateDistance: 10, maximumAge: 20000, timeout: 20000})
          .then((location) => {
            args.map.animateCamera({
              target: {
                lat: location.latitude,
                lng: location.longitude
              },
              zoomLevel: 30,
              altitude: 2000, // iOS (meters from the ground)
              bearing: 270, // Where the camera is pointing, 0-360 (degrees)
              tilt: 50,
              duration: 5000
            }).then(() => {
              args.map.trackUser({
                mode: "FOLLOW_WITH_HEADING", // "NONE" | "FOLLOW" | "FOLLOW_WITH_HEADING" | "FOLLOW_WITH_COURSE"
                animated: true
              })
            })
          })
          break
        case 'ADD_POLYLINE':
          console.log('ADD_POLYLINE')
          let directions = []
          if ('directions' in this.config && this.config.directions.constructor === [].constructor) {
            directions = Object.assign([], this.config.directions)
          }
          const data = {
            id: 1, // optional, can be used in 'removePolylines'
            color: '#336699', // Set the color of the line (default black)
            width: 7, // Set the width of the line (default 5)
            opacity: 0.6, //Transparency / alpha, ranging 0-1. Default fully opaque (1).
            points: directions
          }
          args.map.addPolyline(data)
            .then(() => {
              args.map.animateCamera({
                target: {
                  lat: data.points[0].lat,
                  lng: data.points[0].lng
                },
                zoomLevel: 10,
                altitude: 2000, // iOS (meters from the ground)
                bearing: 0, // Where the camera is pointing, 0-360 (degrees)
                tilt: 0,
                duration: 5000
              })
            })
            .catch((error) => console.log("mapbox addPolygon error: " + error));
          break
        default: break
      }
    }
  }
}
</script>

