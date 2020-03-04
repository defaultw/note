一个shapfile必需有的文件：

- .shp    ——    存储地理要素的几何信息
- .shx    ——    存储要素几何图形的索引信息
- .dbf    ——    存储地理要素的属性信息（非几何信息）

​    可选文件包括：

- .prj    ——    存储空间参考信息，即地理坐标系统信息和投影坐标系统信息。使用well-known文本格式进行描述。

​    PostGIS shapefile工具将shapefile数据从二进制转换为一系列的SQL命令，然后在数据库中运行以加载数据，从而使shapefile数据在PostGIS中可用。



### 表示真实世界的对象

- **ST_GeometryType(geometry)**    ——    返回几何图形的类型

- **ST_NDims(geometry)**    ——    返回几何图形的维数

- **ST_SRID(geometry)**    ——    返回几何图形的空间参考标识码

针对**点**的一些特定**空间函数**包括：

- **ST_X(geometry)**    ——    返回X坐标
- **ST_Y(geometry)**    ——    返回Y坐标

用于处理**线串**的一些特定**空间函数**包括：

- **ST_Length(geometry)**    ——    返回线串的长度
- **ST_StartPoint(geometry)**    ——    将线串的第一个坐标作为点返回
- **ST_EndPoint(geometry）**    ——    将线串的最后一个坐标作为点返回
- **ST_NPoints(geometry)**    ——    返回线串的坐标数量

关于**多边形**图形的一些特定**空间函数**包括：

- **ST_Area(geometry)**    ——     返回多边形的面积
- **ST_NRings(geometry)**    ——    返回多边形中环的数量（通常为1个，其他是孔）
- **ST_ExteriorRing(geometry)**    ——    以线串的形式返回多边形最外面的环
- **ST_InteriorRingN(geometry, n)**    ——    以线串形式返回指定的内部环
- **ST_Perimeter(geometry)**    ——    返回所有环的长度

用于处理**集合**的一些特定**空间函数**：

- **ST_NumGeometries(geometry)**    ——    返回集合中的组成部分的数量
- **ST_GeometryN(geometry, n)**    ——    返回集合中指定的组成部分
- **ST_Area(geometry)**    ——    返回集合中所有多边形组成部分的总面积
- **ST_Length(geometry)**    ——    返回所有线段组成部分的总长度



### 几何图形输入和输出

PostGIS支持以多种格式进行**几何图形**的输入和输出。

​    ①Well-known text（[WKT](https://postgis.net/workshops/postgis-intro/glossary.html#term-wkt)）

- **ST_GeomFromText(text, srid)**    ——    返回geometry
- **ST_AsText(geometry)**    ——    返回text
- **ST_AsEWKT(geometry)**    ——    返回text

​    ②Well-known binary（[WKB](https://postgis.net/workshops/postgis-intro/glossary.html#term-wkb)）

- **ST_GeomFromWKB(bytea)**    ——    返回geometry
- **ST_AsBinary(geometry)**    ——    返回bytea
- **ST_AsEWKB(geometry)**    ——    返回bytea

​    ③Geographic Mark-up Language（[GML](https://postgis.net/workshops/postgis-intro/glossary.html#term-gml)）

- **ST_GeomFromGML(text)**    ——    返回geometry
- **ST_ASGML(geometry)**    ——    返回text

​    ④Keyhole Mark-up Language（[KML](https://postgis.net/workshops/postgis-intro/glossary.html#term-kml)）

- **ST_GeomFromKML(text)**    ——    返回geometry
- **ST_ASKML(geometry)**    ——     返回text

​    ⑤[GeoJson](https://postgis.net/workshops/postgis-intro/glossary.html#term-geojson)

- **ST_AsGeoJSON(geometry)**    ——    返回text

​    ⑥Scalable Vector Graphics([SVG](https://postgis.net/workshops/postgis-intro/glossary.html#term-svg)）

- **ST_AsSVG(geometry)**    ——    返回text