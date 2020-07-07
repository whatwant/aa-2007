# aa-2007
Associate Architect


## Install

- based on Ubuntu 18.04 LTS

### Node.JS

- reference
  - https://soojae.tistory.com/25

- install
```
$ sudo apt install curl build-essential
$ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
$ sudo apt install nodejs
```

- check
```
$ node -v
```

### MongoDB

- reference
  - https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/

- install
```
$ wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
$ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
$ sudo apt update
$ sudo apt install -y mongodb-org
```

- run
```
$ sudo systemctl start mongod
```

- check
```
$ sudo systemctl status mongod
```

### minikube

- reference
  - https://minikube.sigs.k8s.io/docs/start/
  - http://blog.naver.com/PostView.nhn?blogId=isc0304&logNo=221879359568

- install
```
$ sudo apt install -y docker.io
$ sudo usermod -aG docker $USER && newgrp docker
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
$ minikube start
$ minikube kubectl -- get po -A
$ minikube dashboard
```

- check
```
http://127.0.0.1:37501/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/
```



## Google Map

### HTTP Server

- install
```
$ sudo npm install http-server -g
$ mkdir http
$ cd http
$ http-server
```

### Sample 

```
<html>

<head>
  <title>Google Maps Test....</title>
  <script>
    function initMap() {
      var seoul = { lng: 126.9706673, lat: 37.5547787 };

      var options = {
        center: seoul,
        zoom: 15,
      };
      var map = new google.maps.Map(document.getElementById('map'), options);

      //var marker = new google.maps.Marker({position: seoul, map: map});

      var locations = [
        { lng: 126.97081750370484, lat: 37.55506788676746 },
        { lng: 126.97714751697998, lat: 37.56547786297515 },
        { lng: 126.98303263797399, lat: 37.57004847771681 },
      ];

      //var markers = [];
      //for (var i=0; i < locations.length; i++) {
      //  markers[i] = new google.maps.Marker({position: locations[i], map: map});
      //}

      var markers = locations.map( function(location, i) {
        return new google.maps.Marker( {position: location, map: map} );
      });

      var markerCluster = new MarkerClusterer(map, markers,
        { imagePath: 'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m' } );
    }
  </script>
  <script src="https://unpkg.com/@google/markerclustererplus@4.0.1/dist/markerclustererplus.min.js"></script>
  <script async defer src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDT7sSTMO5sgyqu_1l0KuaIK_QAyv0U44c&callback=initMap">
  </script>
  <style type="text/css">
    #map {
      height: 100%;
    },
    body {
      height: 100%;
      margin: 0;
      padding: 0;
    }
  </style>
</head>

<body>
  <div id="map"></div>
</body>
```

### Sample - Marker Click
```<html>

<head>
  <title>Google Maps Test....</title>
  <script>
    function initMap() {
      var seoul = { lng: 126.9706673, lat: 37.5547787 };

      var options = {
        center: seoul,
        zoom: 15,
      };
      var map = new google.maps.Map(document.getElementById('map'), options);

      //var marker = new google.maps.Marker({position: seoul, map: map});

      var locations = [
        { lng: 126.97081750370484, lat: 37.55506788676746 },
        { lng: 126.97714751697998, lat: 37.56547786297515 },
        { lng: 126.98303263797399, lat: 37.57004847771681 },
      ];

      var infowindow = new google.maps.InfoWindow();

      var markers = locations.map( function(loc, i) {
        var marker = new google.maps.Marker({position: loc, map: map});
        marker.addListener( 'click', function(e) {
          var position = marker.getPosition();
          infowindow.setPosition(position);
          infowindow.setContent("{ lng: "+position.lng() + ", lat: "+position.lat() + "}");
          infowindow.open(map);
        });

        return marker;
      });



      //var markers = locations.map( function(location, i) {
      //  return new google.maps.Marker( {position: location, map: map} );
      //});

      var markerCluster = new MarkerClusterer(map, markers,
        { imagePath: 'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m' } );
    }
  </script>
  <script src="https://unpkg.com/@google/markerclustererplus@4.0.1/dist/markerclustererplus.min.js"></script>
  <script async defer src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDT7sSTMO5sgyqu_1l0KuaIK_QAyv0U44c&callback=initMap">
  </script>
  <style type="text/css">
    #map {
      height: 100%;
    },
    body {
      height: 100%;
      margin: 0;
      padding: 0;
    }
  </style>
</head>

<body>
  <div id="map"></div>
</body>
</html>
```


### Sample - icon (html 형식으로 마커 
```
<html>

<head>
  <title>Google Maps Test....</title>
  <script>
    function initMap() {
      var seoul = { lng: 126.9706673, lat: 37.5547787 };

      var options = {
        center: seoul,
        zoom: 15,
      };
      var map = new google.maps.Map(document.getElementById('map'), options);


      var locations = [
        { lng: 126.97081750370484, lat: 37.55506788676746 },
        { lng: 126.97714751697998, lat: 37.56547786297515 },
        { lng: 126.98303263797399, lat: 37.57004847771681 },
      ];

      var geodata = {
        "type": "FeatureCollection",
        "features": [
         { "type": "Feature", "geometry": { "type": "Point", "coordinates": [126.97081750370484, 37.55506788676746] },
                              "properties": { "name": "서울역" } },
         { "type": "Feature", "geometry": { "type": "Point", "coordinates": [126.97714751697998, 37.56547786297515 ] },
                              "properties": { "name": "시청역" } },
         { "type": "Feature", "geometry": { "type": "Point", "coordinates": [126.98303263797399, 37.57004847771681 ]},
                              "properties": { "name": "종각역" } },
         ]
      };

      map.data.addGeoJson(geodata);

      const infowindow = new google.maps.InfoWindow();

      map.data.addListener( 'click', function(e) {
        const feature = e.feature;
        const name = feature.getProperty("name");
        const position = e.latLng;

        infowindow.setPosition(position);
        infowindow.setContent("<div aligh=center><img src=/icons/subway-24px.svg /><br><b>"
                              + name + "</b><br>(" + position.lng() + "," + position.lat() + ")</div>");
        infowindow.open(map);
      });

      map.data.setStyle(function(feature) {
        return {
          icon: {
            url: "/icons/subway-24px.svg",
            anchor: {x: 12, y:12 },
            labelOrigin: { x: 12, y: 30 },
          },
          label: {
            color: "#FF0000",
            text: feature.getProperty("name"),
          },
          title: feature.getProperty("name"),
        };
      });
    }
  </script>
  <script async defer src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDT7sSTMO5sgyqu_1l0KuaIK_QAyv0U44c&callback=initMap">
  </script>
  <style type="text/css">
    #map {
      height: 100%;
    },
    body {
      height: 100%;
      margin: 0;
      padding: 0;
    }
  </style>
</head>

<body>
  <div id="map"></div>
</body>

</html>
```

### Sample - idle (화면에 있는 부분만 처리)
```
<html>

<head>
  <title>Google Maps Test....</title>
  <script>
    function initMap() {
      var seoul = { lng: 126.9706673, lat: 37.5547787 };

      var options = {
        center: seoul,
        zoom: 15,
      };
      var map = new google.maps.Map(document.getElementById('map'), options);


      var locations = [
        { lng: 126.97081750370484, lat: 37.55506788676746 },
        { lng: 126.97714751697998, lat: 37.56547786297515 },
        { lng: 126.98303263797399, lat: 37.57004847771681 },
      ];

      var geodata = {
        "type": "FeatureCollection",
        "features": [
         { "type": "Feature", "geometry": { "type": "Point", "coordinates": [126.97081750370484, 37.55506788676746] },
                              "properties": { "name": "서울역" } },
         { "type": "Feature", "geometry": { "type": "Point", "coordinates": [126.97714751697998, 37.56547786297515 ] },
                              "properties": { "name": "시청역" } },
         { "type": "Feature", "geometry": { "type": "Point", "coordinates": [126.98303263797399, 37.57004847771681 ]},
                              "properties": { "name": "종각역" } },
         ]
      };

      map.data.addGeoJson(geodata);

      const infowindow = new google.maps.InfoWindow();

      map.data.addListener( 'click', function(e) {
        const feature = e.feature;
        const name = feature.getProperty("name");
        const position = e.latLng;

        infowindow.setPosition(position);
        infowindow.setContent("<div aligh=center><img src=/icons/subway-24px.svg /><br><b>"
                              + name + "</b><br>(" + position.lng() + "," + position.lat() + ")</div>");
        infowindow.open(map);
      });

      map.data.setStyle(function(feature) {
        return {
          icon: {
            url: "/icons/subway-24px.svg",
            anchor: {x: 12, y:12 },
            labelOrigin: { x: 12, y: 30 },
          },
          label: {
            color: "#FF0000",
            text: feature.getProperty("name"),
          },
          title: feature.getProperty("name"),
        };
      });

      map.addListener('idle', function() {
        map.data.forEach(function(feature){
          map.data.remove(feature);
        });

        var count = 0;
        const bounds = map.getBounds();
        const features = geodata.features;

        for(var i=0; i < features.length; i++) {
          const coordinates = features[i].geometry.coordinates;
          if( bounds.contains(new google.maps.LatLng( {lng: coordinates[0], lat: coordinates[1]} ))) {
            map.data.addGeoJson( features[i] );
            count++;
          }
        }
        console.log(count + " data added!!!");

      });

    }
  </script>
  <script async defer src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDT7sSTMO5sgyqu_1l0KuaIK_QAyv0U44c&callback=initMap">
  </script>
  <style type="text/css">
    #map {
      height: 100%;
    },
    body {
      height: 100%;
      margin: 0;
      padding: 0;
    }
  </style>
</head>

<body>
  <div id="map"></div>
</body>

</html>
```


### MongoDB import
```
$ mongoimport -d yelp -c business --file yelp_academic_dataset_business.json --jsonArray --port 27017
```

### MongoDB Client & createIntex
```
$ mongo
```
```
> use yelp
> db.business.createIndex( { name: "text", categories: "text" } );
```

### MongoDB - Compass
- 원격에서 연결할 때, SSH Tunnel 이용하여 접속하면 가능
- 이때, DB Host는 localhost로 지정

### MongoDB - create geodata
```
db.business.find().forEach(function(biz){
  db.geodata.insert({ "geometry": { "type": "Point", "coordinates": [ biz.longitude, biz.latitude ] },
    "properties": { "business_id": biz.business_id,
    "name": biz.name,
    "stars": biz.stars,
    "review_count": biz.review_count,
    "categories": biz.categories } });
});
```
