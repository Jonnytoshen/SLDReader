<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [Methods][1]
    -   [Reader][2]
    -   [getLayerNames][3]
    -   [getLayer][4]
    -   [getStyleNames][5]
    -   [getStyle][6]
    -   [getRules][7]
    -   [getGeometryStyles][8]
    -   [OlStyler][9]
-   [Types][10]
    -   [StyledLayerDescriptor][11]
    -   [Layer][12]
    -   [FeatureTypeStyle][13]
    -   [Rule][14]
    -   [Filter][15]
    -   [LineSymbolizer][16]
    -   [PolygonSymbolizer][17]
    -   [PointSymbolizer][18]
    -   [GeometryStyles][19]

## Methods

All methods of this package. If you include the build directly they are props
of the global var SLDReader.


### Reader

Creates a object from an sld xml string,

**Parameters**

-   `sld` **[string][20]** xml string

Returns **[StyledLayerDescriptor][21]** object representing sld style

### getLayerNames

get all layer names in sld

**Parameters**

-   `sld` **[StyledLayerDescriptor][21]** 

Returns **[Array][22]&lt;[string][20]>** registered layernames

### getLayer

getlayer with name

**Parameters**

-   `sld` **[StyledLayerDescriptor][21]** [description]
-   `layername` **[string][20]** [description]

Returns **[Layer][23]** [description]

### getStyleNames

getStyleNames, notice name is not required for userstyle, you might get undefined

**Parameters**

-   `layer` **[Layer][23]** [description]

Returns **[Array][22]&lt;[string][20]>** [description]

### getStyle

get style from array layer.styles, if name is undefined it returns default style.
null is no style found

**Parameters**

-   `layer` **[Layer][23]** [description]
-   `name` **[string][20]** of style

Returns **[object][24]** the style from layer.styles matching the name

### getRules

get rules for specific feature after applying filters

**Parameters**

-   `featureTypeStyle` **[FeatureTypeStyle][25]** 
-   `feature` **[object][24]** geojson
-   `resolution` **[number][26]** m/px

**Examples**

```javascript
const style = getStyle(sldLayer, stylename);
getRules(style.featuretypestyles['0'], geojson,resolution);
```

Returns **[Array][22]&lt;[Rule][27]>** 

### getGeometryStyles

Get styling from rules per geometry type

**Parameters**

-   `rules` **[Array][22]&lt;[Rule][27]>** [description]

Returns **[GeometryStyles][28]** 

### OlStyler

Create openlayers style

**Parameters**

-   `GeometryStyles` **[GeometryStyles][28]** rulesconverter
-   `type` **[string][20]** geometry type, @see [geojson][29] (optional, default `'Polygon'`)

**Examples**

```javascript
OlStyler(getGeometryStyles(rules), geojson.geometry.type);
```

Returns **any** ol.style.Style or array of it

## Types

Types are the javascript representation of the ogc sld structure


### StyledLayerDescriptor

a typedef for StyledLayerDescriptor [xsd][30]

**Properties**

-   `version` **[string][20]** sld version
-   `layers` **[Array][22]&lt;[Layer][23]>** info extracted from NamedLayer element

### Layer

a typedef for Layer, the actual style object for a single layer

**Properties**

-   `name` **[string][20]** layer name
-   `styles` **[Array][22]&lt;[Object][24]>** See explanation at [Geoserver docs][31]
    -   `styles[].default` **[Boolean][32]** 
    -   `styles[].name` **[String][20]?** 
    -   `styles[].featuretypestyles` **[Array][22]&lt;[FeatureTypeStyle][25]>** Geoserver will draw multiple,
        libraries as openlayers can only use one definition!

### FeatureTypeStyle

a typedef for FeatureTypeStyle: [xsd][33]

**Properties**

-   `rules` **[Array][22]&lt;[Rule][27]>** 

### Rule

a typedef for Rule to match a feature: [xsd][33]

**Properties**

-   `name` **[string][20]** rule name
-   `filter` **[Filter][34]?** 
-   `elsefilter` **[boolean][32]?** 
-   `minscaledenominator` **integer?** 
-   `maxscaledenominator` **integer?** 
-   `polygonsymbolizer` **[PolygonSymbolizer][35]?** 
-   `linesymbolizer` **[LineSymbolizer][36]?** 
-   `pointsymbolizer` **[PointSymbolizer][37]?** 

### Filter

[ogc filters][38] should have only one prop

**Properties**

-   `featureid` **[Array][22]&lt;[string][20]>?** 
-   `or` **[object][24]?** filter
-   `and` **[object][24]?** filter
-   `not` **[object][24]?** filter
-   `propertyisequalto` **[Array][22]&lt;[object][24]>?** propertyname & literal
-   `propertyisnotequalto` **[Array][22]&lt;[object][24]>?** propertyname & literal
-   `propertyislessthan` **[Array][22]&lt;[object][24]>?** propertyname & literal
-   `propertyislessthanorequalto` **[Array][22]&lt;[object][24]>?** propertyname & literal
-   `propertyisgreaterthan` **[Array][22]&lt;[object][24]>?** propertyname & literal
-   `propertyisgreaterthanorequalto` **[Array][22]&lt;[object][24]>?** propertyname & literal
-   `propertyislike` **[Array][22]&lt;[object][24]>?** 

### LineSymbolizer

a typedef for [LineSymbolizer][39], see also
[geoserver docs][40]

**Properties**

-   `stroke` **[Object][24]** 
    -   `stroke.css` **[Array][22]&lt;[Object][24]>** one object per CssParameter with props name (camelcased) & value

### PolygonSymbolizer

a typedef for [PolygonSymbolizer][39], see also
[geoserver docs][41]

**Properties**

-   `fill` **[Object][24]** 
    -   `fill.css` **[array][22]** one object per CssParameter with props name (camelcased) & value
-   `stroke` **[Object][24]** 
    -   `stroke.css` **[Array][22]&lt;[Object][24]>** with camelcased name & value

### PointSymbolizer

a typedef for PointSymbolizer [xsd][39]
& [geoserver docs][42]

**Properties**

-   `graphic` **[Object][24]** 
    -   `graphic.externalgraphic` **[Object][24]** 
        -   `graphic.externalgraphic.onlineresource` **[string][20]** 
    -   `graphic.mark` **[Object][24]** 
        -   `graphic.mark.wellknownname` **[string][20]** 
        -   `graphic.mark.fill` **[Object][24]** 
        -   `graphic.mark.stroke` **[Object][24]** 
    -   `graphic.opacity` **[Number][26]** 
    -   `graphic.size` **[Number][26]** 
    -   `graphic.rotation` **[Number][26]** 

### GeometryStyles

contains for each geometry type the symbolizer from an array of rules

**Properties**

-   `polygon` **[Array][22]&lt;[PolygonSymbolizer][35]>** polygonsymbolizers
-   `line` **[Array][22]&lt;[LineSymbolizer][36]>** linesymbolizers
-   `point` **[Array][22]&lt;[PointSymbolizer][37]>** pointsymbolizers, same as graphic prop from PointSymbolizer

[1]: #methods

[2]: #reader

[3]: #getlayernames

[4]: #getlayer

[5]: #getstylenames

[6]: #getstyle

[7]: #getrules

[8]: #getgeometrystyles

[9]: #olstyler

[10]: #types

[11]: #styledlayerdescriptor

[12]: #layer

[13]: #featuretypestyle

[14]: #rule

[15]: #filter

[16]: #linesymbolizer

[17]: #polygonsymbolizer

[18]: #pointsymbolizer

[19]: #geometrystyles

[20]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[21]: #styledlayerdescriptor

[22]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

[23]: #layer

[24]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[25]: #featuretypestyle

[26]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number

[27]: #rule

[28]: #geometrystyles

[29]: http://geojson.org

[30]: http://schemas.opengis.net/sld/1.1/StyledLayerDescriptor.xsd

[31]: http://docs.geoserver.org/stable/en/user/styling/sld/reference/styles.html

[32]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[33]: http://schemas.opengis.net/se/1.1.0/FeatureStyle.xsd

[34]: #filter

[35]: #polygonsymbolizer

[36]: #linesymbolizer

[37]: #pointsymbolizer

[38]: http://schemas.opengis.net/filter/1.1.0/filter.xsd

[39]: http://schemas.opengis.net/se/1.1.0/Symbolizer.xsd

[40]: http://docs.geoserver.org/stable/en/user/styling/sld/reference/linesymbolizer.html#sld-reference-linesymbolizer

[41]: http://docs.geoserver.org/stable/en/user/styling/sld/reference/polygonsymbolizer.html

[42]: http://docs.geoserver.org/latest/en/user/styling/sld/reference/pointsymbolizer.html
