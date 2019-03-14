<template>
  <Mapbox
      ref="appMapBox"
      :accessToken="token"
      :mapStyle="mapStyle"
      latitude="0"
      longitude="0"
      :hideCompass="hideCompass"
      :zoomLevel="zoomLevel"
      :showUserLocation="showUserLocation"
      :disableZoom="disableZoom"
      :disableRotation="disableRotation"
      :disableScroll="disableScroll"
      :disableTilt="disableTilt"
      @mapReady="onMapReady($event)">
  </Mapbox>
</template>

<script>
const geolocation = require("nativescript-geolocation")

export default {
  props: {
    onMapReady: {
      type: Function,
      required: true,
      default: () => {}
    }
  },
  data () {
    return {
      title: '',
      subtitle: '',
      mapStyle: 'traffic_day',
      token: 'pk.eyJ1Ijoic2Fpa2tzdWIiLCJhIjoiY2pzd3gwZ3R6MGZ4MTQzczFkeDByamF0NiJ9.0rU2RC4Re00MvQ3ObLVVaA',
      hideCompass: false,
      zoomLevel: '8',
      showUserLocation: true,
      disableZoom: false,
      disableRotation: false,
      disableScroll: false,
      disableTilt: false
    }
  }/* ,
  mounted () {
    const self = this
    this.$root.$on('fixCurrentLocation', (options) => {
      // Options are must to get current location of the user. Please visit: https://docs.nativescript.org/hardware/location#getcurrentlocation
      if (options && options.constructor === {}.constructor) {
        geolocation.getCurrentLocation(options).then((location) => {
          self.$root.$emit('viewLocation', {
            lat: location.latitude,
            lng: location.longitude
          })
        }).catch((error) => {
          console.log(error)
        })
      }
    })
    this.$root.$on('viewLocation', ({ lat, lng, zoomLevel }) => {
      self.$refs.appMapBox.nativeView.animateCamera({
        target: {
          lat,
          lng,
        },
        zoomLevel: zoomLevel || 20,
        altitude: 2000, // iOS (meters from the ground)
        bearing: 270, // Where the camera is pointing, 0-360 (degrees)
        tilt: 50,
        duration: 5000
      })
    })
    this.$root.$on('addMarker', function (data) {
      if (data && data.constructor === [].constructor) {
        self.$refs.appMapBox.nativeView.addMarkers(data)
      }
    })
    this.$root.$on('startFollowingUser', function ({ mode, animated }) {
      self.$refs.appMapBox.nativeView.trackUser({
        mode: mode || 'FOLLOW_WITH_HEADING',
        animated: animated && typeof animated === 'boolean' ? animated : true
      })
    }),
    this.$root.$on('removeMarkers', function () {
      self.$refs.appMapBox.nativeView.removeMarkers()
    }),
    this.$root.$on('addPolygon', function (data) {
      self.$refs.appMapBox.nativeView.addPolygon(data)
      .then(() => {
        self.$root.$emit('viewLocation', data.points[0])
      })
      .catch((error) => console.log("mapbox addPolygon error: " + error));
    })
    this.$root.$on('addPolyline', function (data) {
      self.$refs.appMapBox.nativeView.addPolyline(data)
      .then(() => {
        self.$root.$emit('viewLocation', Object.assign({}, { zoomLevel: 10 }, data.points[0]))
      })
      .catch((error) => console.log("mapbox addPolygon error: " + error));
    })
  } */
}
</script>

