
# COMunity MApping GeoJSON Specification  (CommaGeoJson)

**Author:** Peter Brownell (greenman@the-organization.com)

## Abstract

A specification commaGeoJSON, a simple extension to GeoJSON for creating and sharing community maps.
*Very much beta, with a reference browser implementation (https://community-atlas.github.io/) and a set of "atlasses" available at http://community-atlas.net* 

## Introduction

CommaGeoJSON is a format for adding additional information, classification and relationship data to "community" created maps.

CommaGeoJSON defines:

* a standard set of properties for features
* a simple structure for taxonomnic categorisation
* a basic inter-feature relationship structure
* a format for addition, non-geometrical features relevant to the map
* a set of properties for the overall map

### Examples

A CommaGeoJSON document containing a minimal set of features, categorisation and relationships. 

```JSON

{
    "type": "FeatureCollection",
    "features": [        
        {
            "type": "Feature",
            "properties": {
                "title": "Community Centre",
                "type": "Place",
                "start_date": "1969-12-31T15:00:00.000-08:00",
                "end_date": "",
            "description": "The Community Centre is committed to working in partnership with local people by providing a hub of activities where everyone can feel welcome and safe to come together, build friendships, learn new skills and reduce feelings of isolation. Originally built around 1890, the place served as an electricity generating station for the North London tram network. Abandoned in the course of the XXst century, it was converted into a community centre, named the Mayville Community Centre back then, by residents of the Mayville Estate in the 1970s. In 2004, Mildmay Community Partnership took over the responsibility and management of the centre. Closed for a few years for renovation, the centre re-opened in 2011, as the first Passive House (an energy-efficient building) of the UK. Today, it hosts many charities and events organized for and with local residents. ",
                "image": "https://upload.wikimedia.org/wikipedia/commons/b/b1/Limehouse_Town_Hall_-_geograph.org.uk_-_788445.jpg",
                "category": "Venues",
                "sub-category": "",
                "tags": [
                    "Events",
                    "youths",
                    "architecture",
                    "office",
                    "workspace",
                    "commons",
                    "Social inclusion",
                    "gardening",
                    "Public space",
                    "Urban regeneration",
                    "collective",
                    "charity"
                ],
                "category-description": "Spaces to hire or use in the neighbourhood",
                "links": [
                    {
                        "url": "http://limehousetownhall.co.uk",
                        "title": "",
                        "description": "",
                        "type": "website"
                    }
                ],
                "relationships": [
                    "atlas#100"                    
                ],
                "created_date": "2020-07-07T08:53:55.274-07:00",
                "updated_date": "2020-09-01T01:47:13.027-07:00",                
                "image_credit": ""
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -0.0314,
                    51.5121
                ]
            },
            "id": "atlas#001"
        }        
    ],
    "nonGeoFeatures": [
        {
            "type": "Feature",
            "properties": {
                "title": "Dance Class",
                "type": "Class",
                "start_date": "2020-08-14T03:03:42.860-07:00",
                "end_date": "",
                "description": "A regular dance class at the community centre",
                "image": "https://upload.wikimedia.org/wikipedia/commons/thumb/6/63/Zumba_%288158431916%29.jpg/220px-Zumba_%288158431916%29.jpg",
                "category": "Activities and events",
                "sub-category": "",
                "tags": [],
                "category-description": "What’s on at our centre?",
                "links": [
                    {
                        "url": "https://en.wikipedia.org/wiki/Zumba",
                        "title": "Wikipedia page",
                        "description": "",
                        "type": "website"
                    }
                ],
                "relationships": [
                    "atlas#001"
                ],
                "created_date": "2020-07-14T03:03:42.860-07:00",
                "updated_date": "2020-11-11T09:08:14.944-08:00",
                "image_credit": ""
            },
            "id": "atlas#100"
        }     
    ],
    "properties": {
        "comma-version": 0.5,
        "title": "Community Map",
        "url": "https://playground.community-atlas.net",
        "id": "atlas",
        "description": "An example atlas",
        "image": "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/OrteliusWorldMap1570.jpg/640px-OrteliusWorldMap1570.jpg",
        "published": "2020-11-12T07:37:00.214Z",
        "links": [
            {
                "title": "The Comensi project",
                "url": "http://community-atlas.net",
                "description": "The Comensi Project homepage",
                "lang": "en",
                "type": "homepage"
            }
        ],
        "version": 94,
        "taxonomy": [
            {
                "category": "Activities and events",
                "description": "What’s on in Mildmay and Newington Green?",
                "sub-categories": [],
                "weight": 0,
                "id": 3
            },            
            {
                "category": "Venues",
                "description": "Spaces to hire or use in the neighbourhood",
                "sub-categories": [],
                "weight": 0,
                "id": 1
            }
        ]
    },
    "relationships": [
        {
            "from": "atlas#001",
            "to": "atlas#100"
        },
        {
            "from": "atlas#100",
            "to": "atlas#001"
        }
    ]
}

```

## CommaGeoJson Objects and Standard Properties

### Feature properties

CommaGeoJSON defines a standard set of feature properties.

* id 
  * (string) A unique identifier for this feature, used for relationships.
* title
  * (string) Feature title
* type
  * (string) Feature type
* description
  * (string) Feature description
* category
  * (string) Feature Category  
* category-description
  * (string) Category description 
* sub-category
  * (string) Category Sub-category
* tags
  * (array of strings) A set of tags for this feature
* image
  * (url) The url of a "cover image" for this feature
* links
  * (array of link objects) An array of link objects defining external links relevant to this feature
* relationships
  * (array of string) An array of feature Ids
* start_date
  * (date) The "start date" for this feature
* end_date
  * (date) The "end date" for this feature  
* created_date
  * (date) The date when the entry for this feature was created
* updated_date
  * (date) The date when the entry for this feature was updated

### Top level object extensions

CommaGeoJSON defines a set of new, top level properties for a GeoJSON object.

* Top level properties
  * These create an object structure that provides information on the dataset.
* nonGeoFeatures
  * A top level property containing feature objects that don't have geo data. Objects in this property conform to the standard feature format, but exclude geometry.
* relationships
  * A simple array of objects defining from->to relationships between features. Relationships can also be expressed within each feature.

#### Top level properties object

The top level "atlas" properties object provides meta-data on the atlas content.

```JSON

 "properties": {
        "title": "Community Map",
        "url": "https://playground.community-atlas.net",
        "id": "atlas",
        "description": "An example atlas",
        "image": "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/OrteliusWorldMap1570.jpg/640px-OrteliusWorldMap1570.jpg",
        "published": "2020-11-12T07:37:00.214Z",
        "links": [
            {
                "title": "The Comensi project",
                "url": "http://community-atlas.net",
                "description": "The Comensi Project homepage",
                "lang": "en",
                "type": "homepage"
            }
        ],
        "version": 94,
        "taxonomy": [
            {
                "category": "Activities and events",
                "description": "What’s on in Mildmay and Newington Green?",
                "sub-categories": [],
                "weight": 0,
                "id": 3
            },            
            {
                "category": "Venues",
                "description": "Spaces to hire or use in the neighbourhood",
                "sub-categories": [],
                "weight": 0,
                "id": 1
            }
        ]
    },

```

##### Properties

* id
  * (string) An id for this atlas
* version  
  * (integer) The version of the atlas defined in this document 
* title
  * (string) Atlas title
* url
  * (url) The default url where this atlas can be viewed
* description
  * (string) A top level description of this atlas
* image
  * (url) The url of a cover image  
* published
  * (date) The published date for this version of the atlas
* links
  * (array of objects) An array of top level links for the atlas, defined as link objects
* taxonomy
  * (array of category objects) An array of objects defining the taxonomy used to categorise the atlas features

#### Relationships

Relationship data for features is defined both within each feature and in a dedicated top level property. 

Relationships are defined as an array of relationship objects. 

### CommaGeoJson Objects

Custom object structures used in this standard

#### Link object

The link object defines a link to an online hyperlinkable entity. 

```JSON
{
   "url": "https://en.wikipedia.org/wiki/Zumba",
   "title": "Wikipedia page",
   "description": "What is Zumba",
   "type": "website"
}
```

#### Category object

CommaGeoJSON provides a method of defining a simple taxonomy for features. The category object makes it possible to provide additional information on relationships between items in the taxonomy.

```JSON

{
  "category": "Activities and events",
  "description": "What’s on?",
  "sub-categories": [],  
  "id": 3
}, 

```

* id
  * (integer) A numeric identifier, uniqe to this atlas, for this category. Used for relationship definition.
* category
  * (string) The category name
* description
  * (string) A description of the category
* sub-categories
  * (array of integer) An array of category ids for categories that should be regarded as sub-categories of this category.

#### Relationship object

Feature to feature relationships are defined (at the top level) using the relationship object. 

```JSON

{
  "from": "atlas#001",
   "to": "atlas#100"
}

```

* from
  * (string) The id of the source feature
* to
  * (string) The id of the target feature
