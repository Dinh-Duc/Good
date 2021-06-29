<template>
  <b-card>
    <b-card-header style="padding: 0 0 1em 0">
      <b-card-title>Bản đồ phân bổ khoáng sản</b-card-title>
    </b-card-header>
    <div
      id="map"
      style="height: 500px; width: 100%; border-radius: 6px"
    />
  </b-card>
</template>

<script>
import dataAQ from './dataAQ.json'
import MapPopup from "./MapPopup.vue";
export default {
  name: 'MapAQ',
  data() {
    return {
      fullscreen: false,
      dataAQ,
      popupHTML: '',
      geojson: null,
      map: null,
      layers: [],
      value: [],
      mapboxgl: null,
      isShowClearBtn: false,
      isShowSearchBar: true,
      dataSelected: {},
      data: null,
      accessToken:
        'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5UZG1aak00WkRrM05qWTBZemM1TW1abU9EZ3dNVEUzTVdZd05ERTVNV1JsWkRnNE56YzRaQT09In0.eyJhdWQiOiJodHRwOlwvXC9vcmcud3NvMi5hcGltZ3RcL2dhdGV3YXkiLCJzdWIiOiJhZG1pbkBjYXJib24uc3VwZXIiLCJhcHBsaWNhdGlvbiI6eyJvd25lciI6ImFkbWluIiwidGllclF1b3RhVHlwZSI6InJlcXVlc3RDb3VudCIsInRpZXIiOiJVbmxpbWl0ZWQiLCJuYW1lIjoiTWFwIFNlcnZpY2UiLCJpZCI6MywidXVpZCI6bnVsbH0sInNjb3BlIjoiYW1fYXBwbGljYXRpb25fc2NvcGUgZGVmYXVsdCIsImlzcyI6Imh0dHBzOlwvXC9hbS52aWV0bWFwcy52bjo0NDNcL29hdXRoMlwvdG9rZW4iLCJ0aWVySW5mbyI6eyJVbmxpbWl0ZWQiOnsidGllclF1b3RhVHlwZSI6InJlcXVlc3RDb3VudCIsInN0b3BPblF1b3RhUmVhY2giOnRydWUsInNwaWtlQXJyZXN0TGltaXQiOjAsInNwaWtlQXJyZXN0VW5pdCI6bnVsbH19LCJrZXl0eXBlIjoiUFJPRFVDVElPTiIsInN1YnNjcmliZWRBUElzIjpbeyJzdWJzY3JpYmVyVGVuYW50RG9tYWluIjoiY2FyYm9uLnN1cGVyIiwibmFtZSI6InJvdXRlIiwiY29udGV4dCI6Ilwvcm91dGVcL3YxIiwicHVibGlzaGVyIjoiYWRtaW4iLCJ2ZXJzaW9uIjoidjEiLCJzdWJzY3JpcHRpb25UaWVyIjoiVW5saW1pdGVkIn0seyJzdWJzY3JpYmVyVGVuYW50RG9tYWluIjoiY2FyYm9uLnN1cGVyIiwibmFtZSI6InNlYXJjaCIsImNvbnRleHQiOiJcL3NlYXJjaFwvdjEuMC4wIiwicHVibGlzaGVyIjoiYWRtaW4iLCJ2ZXJzaW9uIjoidjEuMC4wIiwic3Vic2NyaXB0aW9uVGllciI6IlVubGltaXRlZCJ9LHsic3Vic2NyaWJlclRlbmFudERvbWFpbiI6ImNhcmJvbi5zdXBlciIsIm5hbWUiOiJNYXJrZXIiLCJjb250ZXh0IjoiXC9tYXJrZXJcLzEuMCIsInB1Ymxpc2hlciI6ImFkbWluIiwidmVyc2lvbiI6IjEuMCIsInN1YnNjcmlwdGlvblRpZXIiOiJVbmxpbWl0ZWQifV0sImNvbnN1bWVyS2V5IjoiYVJWbm1UUUhRbWxydXRwQ1RLNVdmdVdXV0E0YSIsImV4cCI6MzczNjMyNTYxMSwiaWF0IjoxNTg4ODQxOTY0LCJqdGkiOiIyMDI2NWY5NC1mOWZlLTQ0NGItYWQ2Ni1hM2Q3NDk0YzkwZTkifQ.ZE63gv6YTsxqXN3OorriRnG49zGMIWoXF5phsf__IDz6yPPf0u9qCDng6hK7dE27sl7C3N2TtCrranc8iOC2p7t7pV-7tdRh0sgmI8qrl_2_xCAdikXzs2e69_WnI8C11ObDGz_i6T6ypiYWUSb9eqi833MabegPY6BlZp0FRBBsB1ssDClDllzXiYf7RbppdAl4bDa-So1Jq6cWAUk9GTeTw53LsF6FriijShLPm-RmN0fgzBoKsDTuTbYIHy_x4GRpTamheAyiFLBEJvyzh5CR_ARUip7nfQLVafFsQ83T8mmuHoEhBpMMzFCJKmJ4paqD1bA4hc9ThsPOxr9iNg',
      markerEvents: [
        {
          properties: {
            type: 'aqi',
            name: 'Than',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 28,
            svg: require('@/assets/icons/charcoal.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.8336553, 21.006951],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Sắt',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 68,
            svg: require('@/assets/icons/beam.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.7937755, 21.0244343],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Than',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 23,
            svg: require('@/assets/icons/charcoal.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.62961816332538, 22.391953380976794],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Đồng',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 55,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.7795346, 21.0513376],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Sắt',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 68,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [106.27630361538014, 22.139743050753864],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Dầu',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 14,
            svg: require('@/assets/icons/oil-drum.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [106.0407253435602, 22.601069310802018],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Dầu',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 4,
            svg: require('@/assets/icons/oil-drum.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.14460407428432, 22.028455628055077],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Dầu',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 9,
            svg: require('@/assets/icons/oil-drum.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.7700387, 20.734085],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Đồng',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 52,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.575109, 20.8993653],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Than',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 23,
            svg: require('@/assets/icons/charcoal.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [107.02459560682402, 20.96363101623907]
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Than',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 23,
            svg: require('@/assets/icons/charcoal.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [103.9061434612067, 21.342647117771975]
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Đồng',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 52,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [103.36082093977143, 21.30487733499979]
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Đồng',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 52,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [104.58106387882904, 21.15226793118224]
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Sắt',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 68,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [103.07521061190153, 22.21246040995893],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Dầu',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 9,
            svg: require('@/assets/icons/oil-drum.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [103.84199479076645, 21.93422096683616],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Đồng',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 52,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [104.41477333401497, 21.805618552326365]
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Sắt',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 68,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.10303143808079, 22.728943049456166],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Than',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 23,
            svg: require('@/assets/icons/charcoal.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [104.07295388078603, 22.293688176213955]
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Đồng',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 52,
            svg: require('@/assets/icons/wire.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [106.8537013559002, 21.642556301728874],
          },
        },
        {
          properties: {
            type: 'aqi',
            name: 'Than',
            img: 'aqi',
            width: '30',
            height: '36',
            value: 23,
            svg: require('@/assets/icons/charcoal.svg'),
          },
          geometry: {
            type: 'Point',
            coordinates: [105.09622294234762, 20.21077087369526]
          },
        },
      ],
    }
  },
  mounted() {
    // this.MapboxGeocoder = require("vietmaps-gl-geocoder/dist/vietmap-gl-geocoder.min");
    // this.MapboxDirections = require("vietmaps-gl-directions/dist/vietmap-gl-directions");
    this.mapboxgl = require('vietmaps-gl/dist/vietmap-gl')
  },
  async created() {
    this.loading = true
    const url = 'https://raw.githubusercontent.com/daohoangson/dvhcvn/master/data/gis/01.json'
    const response = await fetch(url)
    this.data = await response.json()
    this.featureCollection = {
      type: 'FeatureCollection',
      features: this.data.level2s.map(item => ({
        type: 'Feature',
        id: item.level2_id,
        properties: {
          level2_id: item.level2_id,
          name: item.name,
        },
        geometry: {
          type: item.type,
          coordinates: item.coordinates,
        },
        bbox: item.bbox,
      })),
    }
    this.loading = false
    this.geojson = {
      type: 'geojson',
      data: this.featureCollection,
    }
    // this.renderPopupHTMLTemplate("");
    this.init()

    // this.lstLayer();
  },
  methods: {
    async init() {
      // this.MapboxGeocoder = require("vietmaps-gl-geocoder/dist/vietmap-gl-geocoder.min");
      // this.MapboxDirections = require("vietmaps-gl-directions/dist/vietmap-gl-directions");
      this.mapboxgl = require('vietmaps-gl/dist/vietmap-gl')
      const $this = this

      this.mapboxgl.accessToken = this.accessToken
      this.map = new this.mapboxgl.Map({
        container: 'map',
        style: 'vietmap://styles/default/style.json',
        hash: true,
        center: [105.83527627764447, 21.02306227926392],
        zoom: 12,
        // maxBounds: bounds,
        attributionControl: false,
      })

      let hoveredStateId = null
      // Create a popup, but don't add it to the map yet.
      const popup = new this.mapboxgl.Popup({
        closeButton: false,
      })

      this.map.on('load', () => {
        $this.map.addSource('states', this.geojson)
        // The feature-state dependent fill-opacity expression will render the hover effect
        // when a feature's hover state is set to true.
        $this.map.addLayer({
          id: 'state-fills',
          type: 'fill',
          source: 'states',
          layout: {},
          paint: {
            'fill-color': '#e4ce7f',
            'fill-opacity': [
              'case',
              ['boolean', ['feature-state', 'hover'], false],
              0.5,
              0.5,
            ],
          },
        })

        $this.map.addLayer({
          id: 'state-borders',
          type: 'line',
          source: 'states',
          layout: {},
          paint: {
            'line-color': '#fff',
            'line-width': 2,
          },
        })

        function renderPopupHTMLTemplate(huyen) {
          console.log(huyen)
          // const data = JSON.parse(reports);
          let report = ''
          // const sumValues = obj => Object.values(obj).reduce((a, b) => a + b);
          // const tmp = $this.dataAQ.filter(e => e.locale.includes(huyen))
          const tmp = [
            {
              svg: require('@/assets/icons/oil-drum.svg'),
              name: 'Dầu',
            },
            {
              svg: require('@/assets/icons/charcoal.svg'),
              name: 'Than',
            },
            {
              svg: require('@/assets/icons/beam.svg'),
              name: 'Sắt',
            },
            {
              svg: require('@/assets/icons/wire.svg'),
              name: 'Đồng',
            },
          ]
          tmp.forEach(el => {
            // let color = el.color;
            // let lightColor = HEXtoRGB(color);
            console.log(el)
            report
              += `<div class="chu_giai">
              <div class="item-chu-giai">
              <span class="svg_icon"><img src="${el.svg}" /></span><span class="text_name">${el.name}</span> 
              </div>
              </div>`
          })

          return (
            `${'<div class="report-block">\n'
              + '<div class="report-title">Chú giải'}</div>\n`
              + '<div class="report-content">\n'
              + `<div  class="wemap--report">\n${report}</div>\n`
              + '</div>\n'
              + '</div>'
          )
        }
        // When the user moves their mouse over the state-fill layer, we'll update the
        // feature state for the feature under the mouse.
        // $this.map.on('mousemove', 'state-fills', e => {
        //   if (e.features.length > 0) {
        //     if (hoveredStateId) {
        //       $this.map.setFeatureState(
        //         { source: 'states', id: hoveredStateId },
        //         { hover: false },
        //       )
        //     }

        //     // Display a popup with the name of the county. setHTML
        //     const content = renderPopupHTMLTemplate(
        //       e.features[0].properties.name,
        //     )
        //     // popup
        //     //   .setLngLat(e.lngLat)
        //     //   .setText(e.features[0].properties.name)
        //     //   .addTo($this.map);
        //     popup
        //       .setLngLat(e.lngLat)
        //       .setHTML(content)
        //       .addTo($this.map)
        //   }
        //   hoveredStateId = e.features[0].properties.level2_id
        //   $this.map.setFeatureState(
        //     { source: 'states', id: hoveredStateId },
        //     { hover: true },
        //   )
        // })

        // $this.map.on('mouseleave', 'state-fills', () => {
        //   if (hoveredStateId) {
        //     $this.map.setFeatureState(
        //       { source: 'states', id: hoveredStateId },
        //       { hover: false },
        //     )
        //   }
        //   hoveredStateId = null
        //   popup.remove()
        // })

        if (this.markerEvents && this.markerEvents.length > 0) {
          this.markerEvents.forEach(element => {
            const el = document.createElement('div')
            el.className = 'marker-events'
            const nodeText = document.createElement('span')
            // nodeText.innerHTML = element.properties.value
            const nodeImage = document.createElement('img')
            if (element.properties.value > 1 && element.properties.value < 20) {
              // eslint-disable-next-line import/no-dynamic-require
              nodeImage.src = `${require('@/assets/icons/oil-drum.svg')}`
            } else if (element.properties.value > 20 && element.properties.value < 40) {
              // eslint-disable-next-line import/no-dynamic-require
              nodeImage.src = `${require('@/assets/icons/charcoal.svg')}`
            } else if (element.properties.value > 40 && element.properties.value < 60) {
              // eslint-disable-next-line import/no-dynamic-require
              nodeImage.src = `${require('@/assets/icons/wire.svg')}`
            } else {
              // eslint-disable-next-line import/no-dynamic-require
              nodeImage.src = `${require('@/assets/icons/beam.svg')}`
            }
            nodeImage.className = 'el-animate'
            el.appendChild(nodeImage)
            // el.style.width = `${element.properties.width}px`
            // el.style.height = `${element.properties.height}px`
            el.style.width = '15px'
            el.style.height = '15px'
            el.appendChild(nodeText)

            // let htmlPopup = $vm.renderPopupHTMLTemplate(element);
            new $this.mapboxgl.Marker(el)
              .setLngLat(element.geometry.coordinates)
              .setPopup(new $this.mapboxgl.Popup({ offset: 25 }).setHTML('<div id="vue-popup-content"></div>'))
              .addTo($this.map)

            el.addEventListener("click", () => {
              setTimeout(() => {
                new MapPopup({
                  propsData: { feature: element },
                }).$mount("#vue-popup-content")
              }, 100)
            })
          })
        }
        this.map.fitBounds(this.data.bbox)
      })
    },
  },
}
</script>

<style lang="scss">
.mapboxgl-popup{
    z-index: 999999;
    *{
      background: #b6f19e !important;
      z-index: 999999;
    }
    .mapboxgl-popup-content{
      width: 150px;
    }
    .report-block{
      .report-title{
        text-align: center !important;
      }
    }
    .item-chu-giai{
      .svg_icon{
        img{
          width: 15px;
          height: 15px;
        }
      }
      .text_name{
        padding-left: 10px;
      }
    }
}
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
