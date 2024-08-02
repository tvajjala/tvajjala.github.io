---
layout: post
title:  "Redis GeoHashing"
date:   2023-01-22
description: Redis geospatial indexes let you store coordinates and search for them. This data structure is useful for finding nearby points within a given radius or bounding box.
---
> Redis geospatial indexes let you store coordinates and search for them. 
> This data structure is useful for finding nearby points within a given radius or bounding box.


### Geo Spatial Indexes

There are two approaches for Geo Spatial indexing

- Hash based Indexing - divide world into group with unique hash value
  - Even Grid
  - GeoHash
  - Cartesian Tiers
- Tree based Indexing 
  - QuadTree
  - Google S2
  - RTree

#### How Redis GeoHashing Works

Redis support below command to add and search within given radius. These algorithms can be used in Proximity services such as Yelp/Uber to identify users within given radius.

- GEOADD adds a location to a given geospatial index (note that longitude comes before latitude with this command).
- GEOSEARCH returns locations with a given radius or a bounding box.

```shell
> redis-cli
127.0.0.1:6379>

# adding users
127.0.0.1:6379> GEOADD user:dasher -122.27652 37.805186 dasher1
(integer) 1
127.0.0.1:6379> GEOADD user:dasher -122.34 37.805183 dasher2
(integer) 1

#searching
127.0.0.1:6379> GEOSEARCH user:dasher FROMLONLAT -122.2612767 37.7936847 BYRADIUS 10 KM WITHDIST
1) 1) "dasher2"
   2) "7.0357"
2) 1) "dasher1"
   2) "1.8523"

# unique hash
GEOHASH user:dasher dasher1
1) "9q9p1d0znt0"

GEOADD key [NX | XX] [CH] longitude latitude member [longitude
  latitude member ...]

GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"

GEODIST Sicily Palermo Catania

# GEORADIUS
127.0.0.1:6379> GEORADIUS Sicily 15 37 200 km
1) "Palermo"
2) "Catania"
3) "Cataniaa"
```

##### References

-   <https://university.redis.com/courses/ru101/?_gl=1*19ud6xc*_gcl_au*NzIyNzE0MTMzLjE3MTY0NzU1NTI.>












