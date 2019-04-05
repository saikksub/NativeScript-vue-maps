<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <StackLayout>
          <Button @tap="openMaps('SHOW_CURRENT_LOCATION')" text="Maps with my current location" />
          <Button @tap="openMaps('ADD_MARKERS')" text="Maps with multiple Markers" />
          <Button @tap="openMaps('TRACK_ME')" text="Track my position" />
          <Button @tap="addPolyline"  text="Add polyline" />
        </StackLayout>
    </Page>
</template>

<script>
  import MapsPage from '@/components/MapsPage'
  const Color = require('tns-core-modules/color')
  const axios = require('axios')
  const googleDirectionsAPIToken = require('@/google-sdk-token.js').google_directions_token
  const decodePolyline = require('decode-google-map-polyline')

  export default {
    components: {
      MapsPage
    },
    methods: {
      openMaps: function (command, config) {
        this.$navigateTo(
          MapsPage,
          {
            props: { command, config },
          }
        )
      },
      addPolyline: function () {
        const self = this
        this.getDirections({
          origin: 'New Delhi',
          destination: 'Andhra Pradesh',
          token: googleDirectionsAPIToken
        }).then((directions) => {
          self.openMaps('ADD_POLYLINE', { directions })
        }).catch((err) => {
          console.error(err)
        })
      },
      getDirections: async function ({ origin, destination, token }) {
        return new Promise((resolve, reject) => {
          if (!(origin && destination && token)) {
            reject(new Error('Invalid data'))
          }
          console.log(`https://maps.googleapis.com/maps/api/directions/json?origin=${origin.replace(' ', '+')}&destination=${origin.replace(' ', '+')}&key=${token}`,)
          axios.get(
            `https://maps.googleapis.com/maps/api/directions/json?origin=${origin.replace(' ', '+')}&destination=${destination.replace(' ', '+')}&key=${token}`,
          ).then(response => {
            if (
              response && response.status === 200 && 'data' in response &&
              response.data && 'routes' in response.data && 'legs' in response.data.routes[0] && response.data.routes[0].legs[0] &&
              'steps' in response.data.routes[0].legs[0] && response.data.routes[0].legs[0].steps.constructor === [].constructor
            ) {
              const directions = []
              response.data.routes[0].legs[0].steps.forEach((step) => {
                if ('start_location' in step && 'end_location' in step) {
                  directions.push(...decodePolyline(step.polyline.points))
                }
              })
              resolve(directions)
            }
          }).catch((error) => {
            reject(error)
          })
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
