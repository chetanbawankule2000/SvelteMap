<script>
  import { browser } from "$app/environment";
    import { onMount,onDestroy } from "svelte";
    let mapElement;
    let map;
    let L;
onMount(async () => {
        if(browser) {
            L = await import('leaflet');

            map = L.map(mapElement).setView([51.505, -0.09], 13);

           let osm = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
            }).addTo(map);


    

            L.marker([51.5, -0.09]).addTo(map)
                .bindPopup('A pretty CSS3 popup.<br> Easily customizable.')
                .openPopup();
        }
    });

    onDestroy(async () => {
        if(map) {
            console.log('Unloading L map.');
            map.remove();
        }
    });
</script>


<main>
    <div bind:this={mapElement}></div>
</main>

<style>
     @import 'leaflet/dist/leaflet.css';
    main div {
        height: 800px;
    }
</style>