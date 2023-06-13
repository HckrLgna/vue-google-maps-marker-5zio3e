<template>
  <div>
    <div ref="googleMap" class="google-map"></div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      mapOptions: {
        center: { lat: -34.397, lng: 140.644 },
        zoomControl: true,
        zoom: 8,
        gestureHandling: 'cooperative',
      },
      locations: {
        imgClusterUrl:
          'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m',
        locations: [
          {
            id: 1,
            lat: -31.563944,
            lng: 147.154355,
            name_point: 'A',
            title: 'text on hover',
          },
          {
            id: 2,
            lat: -33.718234,
            lng: 150.363181,
            name_point: 'B',
            title: 'text on hover',
          },
          {
            id: 3,
            lat: -33.727111,
            lng: 150.371124,
            name_point: 'C',
            title: 'text on hover',
          },
          {
            id: 4,
            lat: -33.848588,
            lng: 151.209834,
            name_point: 'D',
            title: 'text on hover',
          },
          {
            id: 5,
            lat: -34.853202,
            lng: 150.55,
            name_point: 'E',
            title: 'text on hover',
          },
        ],
      },
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      const { imgClusterUrl, locations } = this.locations;
      const map = new google.maps.Map(this.$refs.googleMap, {
        ...this.mapOptions,
      });
      let markers = locations.map((location) => {
        const setLocations = new google.maps.LatLng(location.lat, location.lng);
        return new google.maps.Marker({
          position: setLocations,
          map: map,
          label: location.name_point,
          title: location.title,
        });
      });
      new MarkerClusterer(map, markers, { imagePath: imgClusterUrl });
    },
  },
};
</script>

<style>
.google-map {
  width: 500px;
  height: 500px;
}
</style>
