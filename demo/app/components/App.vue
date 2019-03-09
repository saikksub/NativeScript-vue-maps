<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <StackLayout>
          <Mapbox
              accessToken="pk.eyJ1Ijoic2Fpa2tzdWIiLCJhIjoiY2pzd3gwZ3R6MGZ4MTQzczFkeDByamF0NiJ9.0rU2RC4Re00MvQ3ObLVVaA"
              mapStyle="traffic_day"
              latitude="28.614809"
              longitude="77.209086"
              hideCompass="true"
              zoomLevel="8"
              showUserLocation="false"
              disableZoom="false"
              disableRotation="false"
              disableScroll="false"
              disableTilt="false"
              @mapReady="onMapReady($event)">
          </Mapbox>
        </StackLayout>
    </Page>
</template>

<script>
  export default {
    data() {
      return {
        msg: 'Hello World!'
      }
    },
    methods: {
      onMapReady(args) {
          console.log(args.map.addMarkers)
          args.map.addMarkers([
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
          ]);
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
