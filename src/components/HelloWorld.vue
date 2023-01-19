<template>
  <div id="input">
    Please select a GeoJson file:
    <input type="file" @change="handleFileChange" />
    <button @click="submit">Submit</button>
  </div>
  <div id="map" style="height: 600px; width: 800px">
    <l-map
      ref="map"
      :center="[17.35146324412854, 78.44722884470269]"
      v-model:zoom="zoom"
    >
      <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        layer-type="base"
        name="OpenStreetMap"
        :center="center"
      ></l-tile-layer>
      <l-geo-json v-if="isData" :geojson="geojson" />
      <l-polygon :lat-lngs="polygon.latlngs" :color="polygon.color" />
    </l-map>
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import { isProxy, toRaw } from "vue";
import {
  LMap,
  LTileLayer,
  LPolygon,
  // LPolyline,
  LGeoJson,
} from "@vue-leaflet/vue-leaflet";
export default {
  components: {
    LMap,
    LTileLayer,
    // LPolyline,
    LPolygon,
    LGeoJson,
  },
  data() {
    return {
      isData: false,
      zoom: 12,
      center: [17.35146324412854, 78.44722884470269],
      polygon: {
        latlngs: [
          [47.2263299, -1.6222],
          [47.21024000000001, -1.6270065],
          [47.1969447, -1.6136169],
          [47.18527929999999, -1.6143036],
          [47.1794457, -1.6098404],
          [47.1775788, -1.5985107],
          [47.1676598, -1.5753365],
          [47.1593731, -1.5521622],
          [47.1593731, -1.5319061],
          [47.1722111, -1.5143967],
          [47.1960115, -1.4841843],
          [47.2095404, -1.4848709],
          [47.2291277, -1.4683914],
          [47.2533687, -1.5116501],
          [47.2577961, -1.5531921],
          [47.26828069, -1.5621185],
          [47.2657179, -1.589241],
          [47.2589612, -1.6204834],
          [47.237287, -1.6266632],
          [47.2263299, -1.6222],
        ],
        color: "green",
      },
      geojson: {},
    };
  },
  methods: {
    handleFileChange(event) {
      this.isData = false;
      var file = event.target.files[0];
      var reader = new FileReader();
      reader.onload = () => {
        var content = reader.result;
        let temp = JSON.parse(content);
        let temp2 = JSON.parse(content);
        this.geojson = temp2;
        this.polygon.latlngs = temp.features[0].geometry.coordinates[0];
        this.center = temp.features[0].geometry.coordinates[0][0];
        // console.log(this.polygon.latlngs);
      };
      reader.readAsText(file);
    },
    submit() {
      this.isData = true;
    },
    getData(data) {
      let rawData = data;
      if (isProxy(data)) {
        rawData = toRaw(data);
      }
      console.log(rawData);
      return rawData;
    },
    getCenter(data) {
      let rawData = data;
      if (isProxy(data)) {
        rawData = toRaw(data);
      }
      console.log(rawData);
      return rawData;
    },
  },
};
</script>

<style scoped>
#input {
  margin: 2rem 1rem;
}
#map {
  display: flex;
  justify-content: center;
  margin: auto;
}
</style>
  
  <style scoped></style>
  <!-- latlngs: [
  [ 78.43695402145386, 17.352440721296134 ],
  [ 78.43751192092896, 17.351478107288564 ],
  [ 78.43815565109253, 17.351887730888155 ],
  [ 78.43862771987915, 17.351437144878282 ],
  [ 78.43873500823975, 17.350556450843957 ],
  [ 78.4407091140747,  17.348180603982684 ],
  [ 78.44276905059814, 17.346869778746957 ],
  [ 78.44538688659668, 17.346542070974312 ],
  [ 78.446524143219,   17.3457330399038   ],
  [ 78.44825148582458, 17.345651112507827 ],
  [ 78.4507405757904,  17.345333643502823 ],
  [ 78.45109462738037, 17.346296289760616 ],
  [ 78.45216751098633, 17.35063837604883  ],
  [ 78.45388412475586, 17.355144205949756 ],
  [ 78.45012903213501, 17.35522612910484  ],
  [ 78.45094442367552, 17.35700794867062  ],
  [ 78.44924926757812, 17.357499482054763 ],
  [ 78.44882011413574, 17.355717667266557 ],
  [ 78.44806909561157, 17.35590199373743  ],
  [ 78.44463586807251, 17.35489843626487  ],
  [ 78.44382047653198, 17.352973229001694 ],
  [ 78.44311237335205, 17.35442737678127  ],
  [ 78.44259738922119, 17.354550261980627 ],
  [ 78.44161033630371, 17.354140644329117 ],
  [ 78.44064474105835, 17.354529781119787 ],
  [ 78.44100952148438, 17.355164686741958 ],
  [ 78.43899250030518, 17.35590199373743  ],
  [ 78.43817710876465, 17.353669582898544 ],
  [ 78.43695402145386, 17.352440721296134 ]
], -->