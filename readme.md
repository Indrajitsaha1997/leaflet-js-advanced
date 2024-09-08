For advanced Leaflet.js usage, you can explore features like custom layers, interactive elements, and advanced plugins. Here are some advanced examples to illustrate how to leverage Leaflet’s capabilities for more complex applications.

### **1. Custom Icons and Markers**

**Example: Custom Marker Icons**

This example demonstrates how to use custom images as markers and manage their interaction with the map.

#### **HTML Example:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Custom Marker Icons</title>
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    #map {
      height: 100vh;
      width: 100%;
    }
  </style>
</head>
<body>

  <!-- Map container -->
  <div id="map"></div>

  <!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    // Initialize the map
    const map = L.map('map').setView([51.505, -0.09], 13);

    // Add a tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    // Custom icon
    const customIcon = L.icon({
      iconUrl: 'https://example.com/path/to/icon.png', // Replace with your icon URL
      iconSize: [32, 32], // Size of the icon
      iconAnchor: [16, 32], // Point of the icon which will correspond to marker's location
      popupAnchor: [0, -32] // Point from which the popup should open relative to the iconAnchor
    });

    // Add marker with custom icon
    const marker = L.marker([51.5, -0.09], { icon: customIcon }).addTo(map);
    marker.bindPopup('<b>Custom Icon</b><br>This is a custom marker icon.').openPopup();
  </script>

</body>
</html>
```

### **2. Layer Groups and Control**

**Example: Managing Different Layer Groups**

This example shows how to manage multiple layers (e.g., markers, polygons) using Layer Groups and Layer Control.

#### **HTML Example:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Layer Groups and Control</title>
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    #map {
      height: 100vh;
      width: 100%;
    }
  </style>
</head>
<body>

  <!-- Map container -->
  <div id="map"></div>

  <!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    // Initialize the map
    const map = L.map('map').setView([51.505, -0.09], 13);

    // Add a tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    // Create marker layer group
    const markers = L.layerGroup().addTo(map);

    // Add markers to the group
    L.marker([51.5, -0.09]).bindPopup('Marker 1').addTo(markers);
    L.marker([51.51, -0.1]).bindPopup('Marker 2').addTo(markers);

    // Create polygon layer group
    const polygons = L.layerGroup().addTo(map);

    // Add polygons to the group
    L.polygon([
      [51.509, -0.08],
      [51.503, -0.06],
      [51.51, -0.047]
    ]).bindPopup('Polygon 1').addTo(polygons);

    // Add layer control
    const baseLayers = {};
    const overlays = {
      'Markers': markers,
      'Polygons': polygons
    };

    L.control.layers(baseLayers, overlays).addTo(map);
  </script>

</body>
</html>
```

### **3. Interactive Map with Drawing Tools**

**Example: Adding Drawing Tools for User Interaction**

This example uses the Leaflet Draw plugin to enable users to draw shapes on the map.

#### **HTML Example:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Leaflet Draw Example</title>
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <!-- Leaflet Draw CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet-draw@1.0.4/dist/leaflet.draw.css" />
  <style>
    #map {
      height: 100vh;
      width: 100%;
    }
  </style>
</head>
<body>

  <!-- Map container -->
  <div id="map"></div>

  <!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <!-- Leaflet Draw JS -->
  <script src="https://unpkg.com/leaflet-draw@1.0.4/dist/leaflet.draw.js"></script>
  <script>
    // Initialize the map
    const map = L.map('map').setView([51.505, -0.09], 13);

    // Add a tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    // Initialize Leaflet Draw
    const drawnItems = L.featureGroup().addTo(map);
    const drawControl = new L.Control.Draw({
      edit: {
        featureGroup: drawnItems
      }
    });
    map.addControl(drawControl);

    // Event handler for when a shape is drawn
    map.on(L.Draw.Event.CREATED, function (e) {
      const layer = e.layer;
      drawnItems.addLayer(layer);
    });
  </script>

</body>
</html>
```

### **4. Heatmap Layer**

**Example: Adding Heatmap Overlay**

This example uses the Leaflet.heat plugin to add a heatmap layer to the map, useful for visualizing density or intensity.

#### **HTML Example:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Leaflet Heatmap Example</title>
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <!-- Leaflet Heatmap CSS -->
  <style>
    #map {
      height: 100vh;
      width: 100%;
    }
  </style>
</head>
<body>

  <!-- Map container -->
  <div id="map"></div>

  <!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <!-- Leaflet Heatmap JS -->
  <script src="https://unpkg.com/leaflet-heatmap@0.2.0/dist/leaflet-heatmap.js"></script>
  <script>
    // Initialize the map
    const map = L.map('map').setView([51.505, -0.09], 13);

    // Add a tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    // Heatmap data
    const heatData = [
      [51.505, -0.09, 0.5], // [lat, lng, intensity]
      [51.515, -0.1, 0.8],
      [51.51, -0.12, 0.7],
      [51.52, -0.1, 0.9]
    ];

    // Add heatmap layer
    const heat = L.heatLayer(heatData, { radius: 25 }).addTo(map);
  </script>

</body>
</html>
```

### **5. Real-time Data with WebSocket

**

**Example: Displaying Real-time Data on the Map**

This example shows how to use WebSocket to update map markers in real time.

#### **HTML Example:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Real-time Data with WebSocket</title>
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    #map {
      height: 100vh;
      width: 100%;
    }
  </style>
</head>
<body>

  <!-- Map container -->
  <div id="map"></div>

  <!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    // Initialize the map
    const map = L.map('map').setView([51.505, -0.09], 13);

    // Add a tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    // Marker layer
    const markers = L.layerGroup().addTo(map);

    // Connect to WebSocket
    const socket = new WebSocket('wss://example.com/real-time-data');

    socket.onmessage = function(event) {
      const data = JSON.parse(event.data);

      // Clear existing markers
      markers.clearLayers();

      // Add new markers
      data.forEach(item => {
        L.marker([item.lat, item.lng]).bindPopup(`<b>${item.name}</b>`).addTo(markers);
      });
    };
  </script>

</body>
</html>
```

### **Summary**

- **Custom Icons and Markers**: Use custom images for markers to personalize map points.
- **Layer Groups and Control**: Manage different types of layers and control their visibility with Layer Groups and Layer Control.
- **Interactive Map with Drawing Tools**: Allow users to draw shapes on the map with Leaflet Draw.
- **Heatmap Layer**: Visualize data density using a heatmap overlay.
- **Real-time Data with WebSocket**: Update markers on the map in real time using WebSocket.

For more advanced functionality, you might also consider exploring additional Leaflet plugins, custom controls, and integration with other data sources or APIs. The [Leaflet documentation](https://leafletjs.com/reference-1.9.4.html) and the [Leaflet Plugins](https://leafletjs.com/plugins.html) page are great resources for further learning.