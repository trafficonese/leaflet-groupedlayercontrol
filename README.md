leaflet-groupedlayercontrol
===========================

Leaflet layer control with support for grouping overlays together.
Also supports making groups exclusive (radio instead of checkbox).

> This project is looking for a maintainer. Interested? Open an issue.

![preview](preview.png)

Demos: [Basic](http://ismyrnow.github.io/leaflet-groupedlayercontrol/example/basic.html) |
[Advanced](http://ismyrnow.github.io/leaflet-groupedlayercontrol/example/advanced.html)

## Installation

Include the compressed JavaScript and CSS files located in the `/dist` folder.

This project is also available via bower and jspm:

```
bower install leaflet-groupedlayercontrol
```

## Usage

### Initialization

Add groupings to your overlay layers object, and swap out the default layer
control with the new one.

```javascript
var groupedOverlays = {
  "Landmarks": {
    "Motorways": motorways,
    "Cities": cities
  },
  "Points of Interest": {
    "Restaurants": restaurants
  }
};

L.control.groupedLayers(baseLayers, groupedOverlays).addTo(map);
```

### Options

For added functionality, pass options when creating the layer control.

```javascript
var options = {
  // Make the "Landmarks" group exclusive (use radio inputs)
  exclusiveGroups: ["Landmarks"],
  // Show a checkbox next to non-exclusive group labels for toggling all
  groupCheckboxes: true,
  sortLayers: true,
  sortGroups: true,
  sortBaseLayers: false,
  collapsed: true,
  position: "topright",
  autoZIndex: true,
  exclusiveGroups: [],
  // enable basic collapsability
  groupsCollapsable: true,
  groupsCollapsed: true,
  // (Optional) The css class(es) used to indicated the group is expanded
  groupsExpandedClass: "glyphicon glyphicon-chevron-down", 
  // (Optional) The css class(es) used to indicated the group is collapsed
  groupsCollapsedClass: "glyphicon glyphicon-chevron-right"
  sortFunction: function (nameA, nameB) {
    if (nameA < nameB) {
      return -1;
    } else if (nameB < nameA) {
      return 1;
    } else {
      return 0;
    }
  }
};

L.control.groupedLayers(baseLayers, groupedOverlays, options).addTo(map);
```

![advanced preview](preview-advanced.png)
![collapsable preview](preview-collapsable.png)

### Methods

#### Adding a layer

Adding a layer individually works similarly to the default layer control,
except that you can also specify a group name, along with the layer and layer name.

```javascript
layerControl.addOverlay(cities, "Cities", "Landmarks");
```

#### Adding a baselayer

```javascript
layerControl.addBaseLayer(newbaselayer, "Baselayer");
```

#### Removing a layer

```javascript
layerControl.removeLayer(cities);
layerControl.removeLayer(newbaselayer);
```

## Note

This plugin only affects how the layers are displayed in the layer control,
and not how they are rendered or layered on the map.

Grouping base layers is not currently supported, but adding exclusive layer
groups is. Layers in an exclusive layer group render as radio inputs.

## License

leaflet-groupedlayercontrol is free software, and may be redistributed under
the MIT-LICENSE.
