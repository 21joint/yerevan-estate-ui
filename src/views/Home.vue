<template>
  <div class="home">
      <div id="courts-map" style="width: 1000px;height: 1000px;"></div>
  </div>
</template>

<script>
    export default {
        data() {
            return {
                markers: {
                    position: {
                        latitude: 59.93,
                        longitude: 30.32
                    },
                    position: {
                        latitude: 59.928,
                        longitude: 30.32
                    }
                },
            }
        },
        methods: {
            hideBlueMarkers() {
                $('.map_content_left').addClass('hidden')
            }
        },
        created() {
        },
        mounted () {
            // function initialize () {
            // }
            var mapOptions = {
                // How zoomed in you want the map to start at (always required)
                zoom: 14,

                // The latitude and longitude to center the map (always required)
                center: new google.maps.LatLng(59.93, 30.32),

                // How you would like to style the map.
                // This is where you would paste any style found on Snazzy Maps.
                styles: [
                    {
                        "featureType": "landscape",
                        "stylers": [
                            {"hue": "#FFBB00"},
                            {"saturation": 43.400000000000006},
                            {"lightness": 37.599999999999994},
                            {"gamma": 1}
                        ]
                    },
                    {
                        "featureType": "road.highway",
                        "stylers": [
                            {"hue": "#FFC200"},
                            {"saturation": -61.8},
                            {"lightness": 45.599999999999994},
                            {"gamma": 1}
                        ]
                    },
                    {
                        "featureType": "road.arterial",
                        "stylers": [
                            {"hue": "#FF0300"},
                            {"saturation": -100},
                            {"lightness": 51.19999999999999},
                            {"gamma": 1}
                        ]
                    },
                    {
                        "featureType": "road.local",
                        "stylers": [
                            {"hue": "#FF0300"},
                            {"saturation": -100},
                            {"lightness": 52},
                            {"gamma": 1}
                        ]
                    },
                    {
                        "featureType": "water",
                        "stylers": [
                            {"hue": "#0078FF"},
                            {"saturation": -13.200000000000003},
                            {"lightness": 2.4000000000000057},
                            {"gamma": 1}
                        ]
                    },
                    {
                        "featureType": "poi",
                        "stylers": [
                            {"hue": "#00FF6A"},
                            {"saturation": -1.0989010989011234},
                            {"lightness": 11.200000000000017},
                            {"gamma": 1}, {
                                "visibility": "off"
                            }
                        ]
                    },
                    {
                        "featureType": "poi.business",
                        "stylers": [
                            {
                                "visibility": "off"
                            }
                        ]
                    },
                    {
                        "featureType": "poi.park",
                        "elementType": "labels.text",
                        "stylers": [
                            {
                                "visibility": "off"
                            }
                        ]
                    }
                ]
            }
            var map = new google.maps.Map(document.getElementById('courts-map'), mapOptions);
            var htmlMarker = createHtmlMarker(59.93, 30.32,{
                markerType: 'club',
                markerText: 'Club',
                markerColor: 'blue'
            });

            htmlMarker.setMap(map);


            function createHtmlMarker(lat, lng, locationInfo){
                function HTMLMarker(){
                    this.lat = lat;
                    this.lng = lng;
                    this.pos = new google.maps.LatLng(lat,lng);
                }
                // device: $rootScope.device.device_tag,
                // dateTime: $scope.locations[0].datetime,
                // address: $scope.locations[0].address,
                // status: $scope.locations[0].status
                switch (locationInfo.markerType) {
                    case 'club':
                        locationInfo.statusText = locationInfo.markerText;
                        break;
                    case 'center':
                        locationInfo.statusText = locationInfo.markerText;
                        break;
                    case 'leisure':
                        locationInfo.statusText = locationInfo.markerText;
                        break;
                }
                HTMLMarker.prototype = new google.maps.OverlayView();
                HTMLMarker.prototype.onRemove= function(){}
                HTMLMarker.prototype.onAdd= function(){
                    var div = document.createElement('DIV');
                    div.className = "map_message_contcontainer";
                    div.innerHTML = '<div class="map_content_left" style="background: #3a9ff1; display: inline-block; width: 120px; height: 36px; border-radius: 8px; border: 3px solid #fff">' +
                        '<div class="map_content_left_content">' +
                        '<div class="map_text" style="color: #fff; padding-top: 7px; font-size: 14px;text-align: center;">' +  locationInfo.statusText + '</div>' + '</div>' +
                        '<div class="map_down_arrow">' + '</div>' + '</div>' +
                        '</div>' +
                        '<div class="map_content_right">' +
                        '<div class="map_content_right_container">' +
                        '</div>' +
                        '</div>';
                    var panes = this.getPanes();

                    panes.overlayImage.appendChild(div);
                }

                HTMLMarker.prototype.draw = function(){
                    var overlayProjection = this.getProjection();
                    var position = overlayProjection.fromLatLngToDivPixel(this.pos);
                    var panes = this.getPanes();
                    panes.overlayImage.style.left = position.x + 'px';
                    panes.overlayImage.style.top = position.y - 30 + 'px';
                }
                return new HTMLMarker();
            }
        }
    }
</script>
