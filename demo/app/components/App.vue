<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <StackLayout>
          <Button @tap="openMaps('SHOW_CURRENT_LOCATION')" text="Maps with my current location" />
          <Button @tap="openMaps('ADD_MARKERS')" text="Maps with multiple Markers" />
          <Button @tap="openMaps('TRACK_ME')" text="Track my position" />
          <Button @tap="openMaps('ADD_POLYLINE')"  text="Add polyline" />
        </StackLayout>
    </Page>
</template>

<script>
  import MapsPage from '@/components/MapsPage'
  const Color = require('tns-core-modules/color')

  export default {
    components: {
      MapsPage
    },
    methods: {
      openMaps: function (command) {
        this.$navigateTo(
          MapsPage,
          {
            props: { command }
          }
        )
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
