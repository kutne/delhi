<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="initial-scale=1,user-scalable=no,maximum-scale=1,width=device-width">
        <meta name="mobile-web-app-capable" content="yes">
        <meta name="apple-mobile-web-app-capable" content="yes">
        <link rel="stylesheet" href="css/leaflet.css">
        <link rel="stylesheet" href="css/qgis2web.css"><link rel="stylesheet" href="css/fontawesome-all.min.css">
        <link rel="stylesheet" href="css/leaflet-measure.css">
        <style>
        
        html {
          -webkit-box-sizing: border-box;
          -moz-box-sizing: border-box;
          box-sizing: border-box;
        }

        *, *:before, *:after {
          -webkit-box-sizing: inherit;
          -moz-box-sizing: inherit;
          box-sizing: inherit;
        }

        html, body {
          height: 100%;  
          padding: 0;
          margin: 0;
          display: block;
        }
        .container {
         height: 100%;
         display: -webkit-box;
         display: -ms-flexbox;
         display: flex;
         -webkit-box-orient: vertical;
         -webkit-box-direction: normal;
             -ms-flex-direction: column;
                 flex-direction: column;
        }

        .header {
          -webkit-box-flex: 0;
              -ms-flex: 0 0 auto;
                  flex: 0 0 auto;
          padding: 0 1rem;
        }

        .title {
          /* Fallback for calc / vmin */
          font-size: 2rem;
          font-size: calc( 2vmin + 1rem);
        }


        .map-container {
          height: 100%;
          /* Fallback for vmin */
          padding: 0px 1rem 1rem 1rem;
          padding: 0px 1vmin 1vmin 1vmin;
        }

        .map-frame {
          height: 100%;
          width: 100%;
        /*   We use outline over border as has issues in some cases */
          outline: 1px solid black;
        }

        #map { 
          height: 100%;
          width: 100%;
        }
        </style>
        <title>Persisting in Place: Representation and Resilience of Delhi Graveyards</title>
    </head>
    <body>
      <div class="map-container">
        <div class="map-frame">
          <div id="map">
            
        </div>
      </div>
    </div>
        <script src="js/qgis2web_expressions.js"></script>
        <script src="js/leaflet.js"></script>
        <script src="js/leaflet-svg-shape-markers.min.js"></script>
        <script src="js/leaflet.rotatedMarker.js"></script>
        <script src="js/leaflet.pattern.js"></script>
        <script src="js/leaflet-hash.js"></script>
        <script src="js/Autolinker.min.js"></script>
        <script src="js/rbush.min.js"></script>
        <script src="js/labelgun.min.js"></script>
        <script src="js/labels.js"></script>
        <script src="js/leaflet-measure.js"></script>
        <script src="data/delhi_1922_polygons_11.js"></script>
        <script src="data/delhi_1922_points_12.js"></script>
        <script src="data/delhi_1912_points_13.js"></script>
        <script src="data/delhi_1939_points_14.js"></script>
        <script src="data/delhi_1939_polygons_15.js"></script>
<script>

function highlightFeature(e) {
    highlightLayer = e.target;
    if (e.target.feature.geometry.type === 'LineString') {
      highlightLayer.setStyle({
        color: '#ffff00',
      });
    } else {
      highlightLayer.setStyle({
        fillColor: '#ffff00',
        fillOpacity: 1
      });
    }
    
    highlightLayer.openPopup();
}



var map = L.map('map', {
    zoomControl:true, maxZoom:28, minZoom:1
}).fitBounds([[28.546822961068656,77.13104782243265],[28.666436621980846,77.28404899752655]]);        

var hash = new L.Hash(map);
map.attributionControl.setPrefix('<a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');
var autolinker = new Autolinker({truncate: {length: 30, location: 'smart'}});
var measureControl = new L.Control.Measure({
    position: 'topleft',
    primaryLengthUnit: 'meters',
    secondaryLengthUnit: 'kilometers',
    primaryAreaUnit: 'sqmeters',
    secondaryAreaUnit: 'hectares'
});
measureControl.addTo(map);

document.getElementsByClassName('leaflet-control-measure-toggle')[0]
.innerHTML = '';
document.getElementsByClassName('leaflet-control-measure-toggle')[0]
.className += ' fas fa-ruler';
var bounds_group = new L.featureGroup([]);


function setBounds() {
}  




// // adding maps starts here:
// // ADD 1922 NORTHEAST
// map.createPane('pane_delhi_1922_NE_0');
// map.getPane('pane_delhi_1922_NE_0').style.zIndex = 300;
// var img_delhi_1922_NE_0 = 'data/delhi_1922_NE_0.png';
// var img_bounds_delhi_1922_NE_0 = [[28.61913574390048,77.20122676318451],[28.764511233031556,77.32588059191323]];
// var layer_delhi_1922_NE_0 = new L.imageOverlay(img_delhi_1922_NE_0,
//                                       img_bounds_delhi_1922_NE_0,
//                                       {pane: 'pane_delhi_1922_NE_0'});
// bounds_group.addLayer(layer_delhi_1922_NE_0);
// // map.addLayer(layer_delhi_1922_NE_0);

// // ADD 1912  MAP
// map.createPane('pane_delhi_1912_MAP_4');
// map.getPane('pane_delhi_1912_MAP_4').style.zIndex = 304;
// var img_delhi_1912_MAP_4 = 'data/delhi_1912_MAP_4.png';
// var img_bounds_delhi_1912_MAP_4 = [[28.4887951815074,77.08418642528135],[28.75455756631503,77.29357530049151]];
// var layer_delhi_1912_MAP_4 = new L.imageOverlay(img_delhi_1912_MAP_4,
//                                       img_bounds_delhi_1912_MAP_4,
//                                       {pane: 'pane_delhi_1912_MAP_4'});
// bounds_group.addLayer(layer_delhi_1912_MAP_4);
// // map.addLayer(layer_delhi_1912_MAP_4);


// // ADD 1939 MAP
// map.createPane('pane_delhi_19391942_modified_10');
// map.getPane('pane_delhi_19391942_modified_10').style.zIndex = 410;
// var img_delhi_19391942_modified_10 = 'data/delhi_19391942_modified_10.png';
// var img_bounds_delhi_19391942_modified_10 = [[28.526870525966174,77.0794020434214],[28.76143207028693,77.28305300632314]];
// var layer_delhi_19391942_modified_10 = new L.imageOverlay(img_delhi_19391942_modified_10,
//                                       img_bounds_delhi_19391942_modified_10,
//                                       {pane: 'pane_delhi_19391942_modified_10'});
// bounds_group.addLayer(layer_delhi_19391942_modified_10);
// // map.addLayer(layer_delhi_19391942_modified_10);


map.createPane('pane_OpenStreetMapmonochrome');
map.getPane('pane_OpenStreetMapmonochrome').style.zIndex = 1;
var layer_OpenStreetMapmonochrome_16 = L.tileLayer('http://a.tiles.wmflabs.org/bw-mapnik/{z}/{x}/{y}.png', {
    pane: 'pane_OpenStreetMapmonochrome',
    opacity: 1.0,
    attribution: '',
    minZoom: 1,
    maxZoom: 28,
    minNativeZoom: 0,
    maxNativeZoom: 18
});

layer_OpenStreetMapmonochrome_16;
map.addLayer(layer_OpenStreetMapmonochrome_16);

var baseMaps = {};

//  START 1922 POLYGONS
function pop_delhi_1922_polygons_11(feature, layer) {
    layer.on({
        mouseout: function(e) {
            for (i in e.target._eventParents) {
                e.target._eventParents[i].resetStyle(e.target);
            }
            if (typeof layer.closePopup == 'function') {
                layer.closePopup();
            } else {
                layer.eachLayer(function(feature){
                    feature.closePopup()
                });
            }
        },
        mouseover: highlightFeature
    });
}

function style_delhi_1922_polygons_11_0() {
    return {
        pane: 'pane_delhi_1922_polygons_11',
        opacity: 1,
        color: 'rgba(35,35,35,1.0)',
        dashArray: '',
        lineCap: 'butt',
        lineJoin: 'miter',
        weight: 0.50, 
        fill: true,
        fillOpacity: .5,
        fillColor: 'rgba(11,248,148,1.0)',
        interactive: true,
    }
}

map.createPane('pane_delhi_1922_polygons_11');
map.getPane('pane_delhi_1922_polygons_11').style.zIndex = 21;
map.getPane('pane_delhi_1922_polygons_11').style['mix-blend-mode'] = 'normal';
var layer_delhi_1922_polygons_11 = new L.geoJson(json_delhi_1922_polygons_11, {
    attribution: '',
    interactive: true,
    dataVar: 'json_delhi_1922_polygons_11',
    layerName: 'layer_delhi_1922_polygons_11',
    pane: 'pane_delhi_1922_polygons_11',
    style: style_delhi_1922_polygons_11_0,
    // onEachFeature: pop_delhi_1922_polygons_11, 
    onEachFeature: function (feature, layer) {
        layer.bindPopup(feature.properties.type);
    }
});
bounds_group.addLayer(layer_delhi_1922_polygons_11);
map.addLayer(layer_delhi_1922_polygons_11);

//  START 1922 POINTS
function pop_delhi_1922_points_12(feature, layer) {
    layer.on({
        mouseout: function(e) {
            for (i in e.target._eventParents) {
                e.target._eventParents[i].resetStyle(e.target);
            }
            if (typeof layer.closePopup == 'function') {
                layer.closePopup();
            } else {
                layer.eachLayer(function(feature){
                    feature.closePopup()
                });
            }
        },
        mouseover: highlightFeature,
    });
}
function style_delhi_1922_points_12_0(feature) {
    var context = {
        feature: feature,
        variables: {}
    };
    // Start of if blocks and style check logic
    if (exp_delhi_1922_points_12rule0_eval_expression(context)) {
          return {
        pane: 'pane_delhi_1922_points_12',
        shape: 'square',
        radius: 5.0,
        opacity: .5,
        color: 'rgba(35,35,35,1.0)',
        dashArray: '',
        lineCap: 'butt',
        lineJoin: 'miter',
        weight: 1,
        fill: true,
        fillOpacity: .5,
        fillColor: 'rgba(11,248,148,1.0)',
        interactive: true,
    };
        }
    else {
        return {fill: false, stroke: false};
    }
}
map.createPane('pane_delhi_1922_points_12');
map.getPane('pane_delhi_1922_points_12').style.zIndex = 412;
map.getPane('pane_delhi_1922_points_12').style['mix-blend-mode'] = 'normal';
var layer_delhi_1922_points_12 = new L.geoJson(json_delhi_1922_points_12, {
    attribution: '',
    interactive: true,
    dataVar: 'json_delhi_1922_points_12',
    layerName: 'layer_delhi_1922_points_12',
    pane: 'pane_delhi_1922_points_12',
    onEachFeature: pop_delhi_1922_points_12,
    pointToLayer: function (feature, latlng) {
        var context = {
            feature: feature,
            variables: {}
        };
        return L.shapeMarker(latlng, style_delhi_1922_points_12_0(feature));
    },
});
bounds_group.addLayer(layer_delhi_1922_points_12);
map.addLayer(layer_delhi_1922_points_12);

// START 1912 POINTS
function pop_delhi_1912_points_13(feature, layer) {
    layer.on({
        mouseout: function(e) {
            for (i in e.target._eventParents) {
                e.target._eventParents[i].resetStyle(e.target);
            }
            if (typeof layer.closePopup == 'function') {
                layer.closePopup();
            } else {
                layer.eachLayer(function(feature){
                    feature.closePopup()
                });
            }
        },
        mouseover: highlightFeature,
    });
}


function style_delhi_1912_points_13_0(feature) {
    var context = {
        feature: feature,
        variables: {}
    };
    // Start of if blocks and style check logic
    if (exp_delhi_1912_points_13rule0_eval_expression(context)) {
          return {
        pane: 'pane_delhi_1912_points_13',
        shape: 'triangle',
        radius: 5,
        opacity: 1,
        color: 'rgba(50,87,128,1.0)',
        dashArray: '',
        lineCap: 'butt',
        lineJoin: 'miter',
        weight: 1,
        fill: true,
        fillOpacity: .6,
        fillColor: 'rgba(236,205,93,1.0)',
        interactive: true,
    };
        }
    else {
        return {fill: false, stroke: false};
    }
}
map.createPane('pane_delhi_1912_points_13');
map.getPane('pane_delhi_1912_points_13').style.zIndex = 413;
map.getPane('pane_delhi_1912_points_13').style['mix-blend-mode'] = 'normal';
var layer_delhi_1912_points_13 = new L.geoJson(json_delhi_1912_points_13, {
    attribution: '',
    interactive: true,
    dataVar: 'json_delhi_1912_points_13',
    layerName: 'layer_delhi_1912_points_13',
    pane: 'pane_delhi_1912_points_13',
    onEachFeature: pop_delhi_1912_points_13,
    pointToLayer: function (feature, latlng) {
        var context = {
            feature: feature,
            variables: {}
        };
        return L.shapeMarker(latlng, style_delhi_1912_points_13_0(feature));
    },
});
bounds_group.addLayer(layer_delhi_1912_points_13);
map.addLayer(layer_delhi_1912_points_13);

// START 1939 POINTS
function pop_delhi_1939_points_14(feature, layer) {
    layer.on({
        mouseout: function(e) {
            for (i in e.target._eventParents) {
                e.target._eventParents[i].resetStyle(e.target);
            }
            if (typeof layer.closePopup == 'function') {
                layer.closePopup();
            } else {
                layer.eachLayer(function(feature){
                    feature.closePopup()
                });
            }
        },
        mouseover: highlightFeature,
    });
}



function style_delhi_1939_points_14_0() {
    return {
        pane: 'pane_delhi_1939_points_14',
        radius: 5,
        opacity: 1,
        color: 'rgba(35,35,35,1.0)',
        dashArray: '',
        lineCap: 'butt',
        lineJoin: 'miter',
        weight: 1,
        fill: true,
        fillOpacity: .5,
        fillColor: 'rgba(152,125,183,1.0)',
        interactive: true,
    }
}
map.createPane('pane_delhi_1939_points_14');
map.getPane('pane_delhi_1939_points_14').style.zIndex = 414;
map.getPane('pane_delhi_1939_points_14').style['mix-blend-mode'] = 'normal';
var layer_delhi_1939_points_14 = new L.geoJson(json_delhi_1939_points_14, {
    attribution: '',
    interactive: true,
    dataVar: 'json_delhi_1939_points_14',
    layerName: 'layer_delhi_1939_points_14',
    pane: 'pane_delhi_1939_points_14',
    onEachFeature: pop_delhi_1939_points_14,
    pointToLayer: function (feature, latlng) {
        var context = {
            feature: feature,
            variables: {}
        };
        return L.circleMarker(latlng, style_delhi_1939_points_14_0(feature));
    },
});
bounds_group.addLayer(layer_delhi_1939_points_14);
map.addLayer(layer_delhi_1939_points_14);

// START 1939 POLYGONS
function pop_delhi_1939_polygons_15(feature, layer) {
    layer.on({
        mouseout: function(e) {
            for (i in e.target._eventParents) {
                e.target._eventParents[i].resetStyle(e.target);
            }
            if (typeof layer.closePopup == 'function') {
                layer.closePopup();
            } else {
                layer.eachLayer(function(feature){
                    feature.closePopup()
                });
            }
        },
        mouseover: highlightFeature,
    });
}

function style_delhi_1939_polygons_15_0() {
    return {
        pane: 'pane_delhi_1939_polygons_15',
        opacity: .7,
        color: 'rgba(35,35,35,1.0)',
        dashArray: '',
        lineCap: 'butt',
        lineJoin: 'miter',
        weight: 1.0, 
        fill: true,
        fillOpacity: .5,
        fillColor: 'rgba(152,125,183,1.0)',
        interactive: true,
    }
}
map.createPane('pane_delhi_1939_polygons_15');
map.getPane('pane_delhi_1939_polygons_15').style.zIndex = 315;
map.getPane('pane_delhi_1939_polygons_15').style['mix-blend-mode'] = 'normal';
var layer_delhi_1939_polygons_15 = new L.geoJson(json_delhi_1939_polygons_15, {
    attribution: '',
    interactive: true,
    dataVar: 'json_delhi_1939_polygons_15',
    layerName: 'layer_delhi_1939_polygons_15',
    pane: 'pane_delhi_1939_polygons_15',
    onEachFeature: pop_delhi_1939_polygons_15,
    style: style_delhi_1939_polygons_15_0,
});
bounds_group.addLayer(layer_delhi_1939_polygons_15);
map.addLayer(layer_delhi_1939_polygons_15);


L.control.layers(baseMaps,{

  '<img src="legend/delhi_1912_points_13_19120.png" />1912': layer_delhi_1912_points_13,
  
  '<img src="legend/delhi_1922_points_12_19220.png" />1922 points': layer_delhi_1922_points_12,
  
  '<img src="legend/delhi_1922_polygons_11.png" /> 1922 polygons': layer_delhi_1922_polygons_11,
  
  '<img src="legend/delhi_1939_polygons_15.png" /> 1939 polygons': layer_delhi_1939_polygons_15,
  
  '<img src="legend/delhi_1939_points_14.png" /> 1939 points': layer_delhi_1939_points_14,
  
//   "1912 map": layer_delhi_1912_MAP_4,
  
//   "1922 map": layer_delhi_1922_NE_0,
  
//   "1939 map": layer_delhi_19391942_modified_10,
  
  "present day baselayer": layer_OpenStreetMapmonochrome_16,
  
},{collapsed:false}).addTo(map);
        setBounds();
        var i = 0;
        layer_delhi_1922_points_12.eachLayer(function(layer) {
            var context = {
                feature: layer.feature,
                variables: {}
            };
            layer.bindTooltip((layer.feature.properties['desc'] !== null?String('<div style="color: #000000; font-size: 10pt; font-family: \'MS Shell Dlg 2\', sans-serif;">' + layer.feature.properties['desc']) + '</div>':''), {permanent: true, offset: [-0, -16], className: 'css_delhi_1922_points_12'});
            labels.push(layer);
            totalMarkers += 1;
              layer.added = true;
              addLabel(layer, i);
              i++;
        });
        var i = 0;
        layer_delhi_1912_points_13.eachLayer(function(layer) {
            var context = {
                feature: layer.feature,
                variables: {}
            };
            layer.bindTooltip((layer.feature.properties['desc'] !== null?String('<div style="color: #000000; font-size: 10pt; font-family: \'MS Shell Dlg 2\', sans-serif;">' + layer.feature.properties['desc']) + '</div>':''), {permanent: true, offset: [-0, -16], className: 'css_delhi_1912_points_13'});
            labels.push(layer);
            totalMarkers += 1;
              layer.added = true;
              addLabel(layer, i);
              i++;
        });
        L.ImageOverlay.include({
            getBounds: function () {
                return this._bounds;
            }
        });
        resetLabels([layer_delhi_1922_points_12,layer_delhi_1912_points_13]);
        map.on("zoomend", function(){
            resetLabels([layer_delhi_1922_points_12,layer_delhi_1912_points_13]);
        });
        map.on("layeradd", function(){
            resetLabels([layer_delhi_1922_points_12,layer_delhi_1912_points_13]);
        });
        map.on("layerremove", function(){
            resetLabels([layer_delhi_1922_points_12,layer_delhi_1912_points_13]);
        });
        </script>
    </body>
</html>
