<template>
  <div>
    <h1 class="mt-3">Mapa</h1>
    <div class="container mt-3">
      <div class="row">
        <div class="col-6 mt-1 mb-3">
          <button class="btn btn-warning m-3" @click="Tomillo">¿Dónde está Fundación Tomillo?</button>
        </div>
        <div class="col-12 col-md-6 text-light mt-1 mb-3">secondary
          <button class="btn btn-warning m-3" @click="popUp">¿Dónde está La Nave?</button>
        </div>
      </div>
            <div class="row">
        <div class="col-6" id="mapid"></div>
      </div>
    </div>
  </div>
</template>

<script>
import L from "leaflet";
import { onMounted } from "vue";

export default {
  name: "Mapa",
  components: {},
  setup() {
    let mymap
    let marker
    onMounted(() => {
      mymap = L.map("mapid").setView([40.369623570006254, -3.673387171182979], 13);
      L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    id: 'mapbox/streets-v11',
    tileSize: 512,
    zoomOffset: -1,
    accessToken: 'pk.eyJ1IjoiYmxvcG1hciIsImEiOiJja2xhcTF5aXowNzRiMnVvMTN5bHdvYWt4In0.pHrpZhpoCwyB8g2e-1Xw4A'
    }).addTo(mymap);
    L.marker([40.347013456220374, -3.6946648409074503]).bindPopup("<b>La Nave</b><br>C/ Cifuentes, 5<br>28021 Madrid").openPopup().addTo(mymap);
    });

    
    function Tomillo (){
      L.marker([40.369623570006254, -3.673387171182979]).bindPopup("<b>Fundación Tomillo</b><br>C/ Albuñuelas, 15<br>28041 Madrid").openPopup().addTo(mymap);
    }

    function popUp(){
      var popup = L.popup()
    .setLatLng([40.347013456220374, -3.6946648409074503])
    .setContent("<b>La Nave</b> está aquí")
    .openOn(mymap);
    }


    return {
      Tomillo,
      popUp
    };
  },
}
</script>

<style lang=scss scope>
#mapid {
  width: 100%;
  height: 500px;
  border: solid 1px grey;
}
</style>