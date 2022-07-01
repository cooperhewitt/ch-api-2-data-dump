### Exhibition

#### Fields
These are all the fields you can query on the Exhibition entity. 
```
{
  exhibition {
    category
    collectionsOnlineId
    id
    identifier
    label
    location
    summary
    title
    date
    object {
        id 
        summary
    }
  }
}
```
* For the nested queries you can use all the fields available for that entity. For simplicity we have limited this to `id` and `summary` for the docs.
#### Arguments
These are all the possible arguments for an department query:
```
page: int
size: int
sort: [{arg1: order}, {arg2: order}] 

general: string

category: string
collectionsOnlineId: string
id: string
identifier: string
label: string
location: string
locationId: string
summary: string
```

#### Sorting
The available sorting terms are:
```
id
summary
```
#### Aggregations
You can create aggregations across different fields: 
```
{
exhibition(aggregations:["label"]) {
     id    
  }
}
```
You can currently aggregate across these exhibition fields:
```
label
location
locationId
```

#### Example request and its response

##### Request
```
{
  exhibition (identifier:"2318806315") {
    category
    collectionsOnlineId
    id
    identifier
    label
    location
    summary
    title
    date
    object {
        id 
        summary
    }
  }
}
```

##### Response
```
{
  "data": {
    "exhibition": [
      {
        "category": null,
        "collectionsOnlineId": "2318806315",
        "id": "exhibition-1652",
        "identifier": [
          {
            "value": "1652",
            "type": "tms id"
          },
          {
            "value": "2318806315",
            "type": "legacy collections online id"
          }
        ],
        "label": [
          {
            "value": "Mounts"
          },
          {
            "value": "Framing"
          },
          {
            "value": "Lighting"
          }
        ],
        "location": [
          {
            "datatype": {
              "base": "location"
            },
            "description": [
              {
                "type": "general description",
                "value": "3rd floor gallery"
              }
            ],
            "id": "location-13515",
            "onDisplay": true,
            "site": {
              "room": {
                "value": "302"
              },
              "value": "Carnegie Mansion"
            },
            "summary": {
              "title": "CHSDM, Carnegie Mansion, 302"
            },
            "title": [
              {
                "type": "default title",
                "value": "CHSDM, Carnegie Mansion, 302"
              }
            ]
          }
        ],
        "summary": {
          "title": "Designing Peace"
        },
        "title": [
          {
            "value": "Designing Peace"
          }
        ],
        "date": [
          {
            "from": "2022",
            "to": "2023",
            "value": "2022-06-10-2023-09-04"
          }
        ],
        "object": [
          {
            "id": "object-293964",
            "summary": {
              "title": "Cactus Wall/Muro de Pitayo Dulce, from the project Borderwall as Architecture (Print)"
            }
          },
          {
            "id": "object-296130",
            "summary": {
              "title": "Body Mapping (Project)"
            }
          },
          {
            "id": "object-296136",
            "summary": {
              "title": "Startblok Elzenhagen (Project)"
            }
          },
          {
            "id": "object-296135",
            "summary": {
              "title": "New World Summit - Rojava (Project)"
            }
          },
          {
            "id": "object-296133",
            "summary": {
              "title": "Designing for Dignity (Project)"
            }
          },
          {
            "id": "object-296158",
            "summary": {
              "title": "Black Lives Matter Street Mural Census (Project)"
            }
          },
          {
            "id": "object-296151",
            "summary": {
              "title": "Regreening Africa (Project)"
            }
          },
          {
            "id": "object-296137",
            "summary": {
              "title": "Stone Garden (Project)"
            }
          },
          {
            "id": "object-296155",
            "summary": {
              "title": "Papers, Please (Project)"
            }
          },
          {
            "id": "object-296157",
            "summary": {
              "title": "Black Lives Matter Harlem Street Mural (Project)"
            }
          }
        ]
      }
    ]
  },
  "extensions": {
    "pagination": {
      "hits": 1,
      "per_page": 10,
      "current_page": 0,
      "number_of_pages": 1
    }
  }
}
```
