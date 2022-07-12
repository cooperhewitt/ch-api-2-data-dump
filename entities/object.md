
### Object

#### Fields
These are the fields you can query on the object entity:

```
{
  object {
    classification
    collectionsOnlineId
    culture 
    colors
    date 
    department 
    description 
    exhibition
    identifier
    id
    inscription 
    geography
    legal
    loaned
    location
    material 
    medium 
    measurements
    multimedia 
    name 
    note 
    period 
    provenance 
    status
    summary
    title

    agent {
        id
        summary
    }

    collector {
        id
        summary
    }

    maker {
        id
        summary
    }

    subject {
        id
        summary
    }

    tag {
        id
        summary
    }   
  }
}

```
* For the nested queries you can use all the fields available for that entity. For simplicity we have limited this to `id` and `summary` for the docs.

##### Color
Here are two examples of color searching.

###### Example 1
Request:
```
{
  object(colors:"#8eabae") {
    id
    colors    
    multimedia
  }
}
```

Response:
```{
  "data": {
    "object": [
      {
        "id": "object-284370",
        "colors": [
          "#8eabae",
          "#9dbabc",
          "#a0b9bd",
          "#92abaf",
          "#e5e6e6"
        ],
        "multimedia": [
          {
            "datatype": {
              "actual": "image",
              "base": "media"
            },
            "gvision": {
              "colors": [
                {
                  "confidence": "58.85",
                  "fraction": 0.37141976,
                  "hex": "#8eabae",
                  "rgb": {
                    "blue": 174,
                    "green": 171,
                    "red": 142,
                    "value": "142, 171, 174"
                  }
                },
                {
                  "confidence": "36.05",
                  "fraction": 0.22679013,
                  "hex": "#9dbabc",
                  "rgb": {
                    "blue": 188,
                    "green": 186,
                    "red": 157,
                    "value": "157, 186, 188"
                  }
                },
                {
                  "confidence": "2.63",
                  "fraction": 0.13487655,
                  "hex": "#a0b9bd",
                  "rgb": {
                    "blue": 189,
                    "green": 185,
                    "red": 160,
                    "value": "160, 185, 189"
                  }
                },
                {
                  "confidence": "2.46",
                  "fraction": 0.113703705,
                  "hex": "#92abaf",
                  "rgb": {
                    "blue": 175,
                    "green": 171,
                    "red": 146,
                    "value": "146, 171, 175"
                  }
                },
                {
                  "confidence": "0.00",
                  "fraction": 0.15320988,
                  "hex": "#e5e6e6",
                  "rgb": {
                    "blue": 230,
                    "green": 230,
                    "red": 229,
                    "value": "229, 230, 230"
                  }
                }
              ],
              "enhanced": true
            },
            "id": "media-379749",
            "large": {
              "format": "jpeg",
              "location": "379/749/large_CHSDM_BC0DBD6EF38D2_1.jpg",
              "measurements": {
                "dimensions": [
                  {
                    "dimension": "height",
                    "units": "pixels",
                    "value": 1024
                  },
                  {
                    "dimension": "width",
                    "units": "pixels",
                    "value": 737
                  }
                ],
                "filesize": {
                  "units": "bytes",
                  "value": 95097
                }
              },
              "url": "https://ciim-static-media.s3.us-east-1.amazonaws.com/379/749/large_CHSDM_BC0DBD6EF38D2_1.jpg"
            },
            "preview": {
              "format": "jpeg",
              "location": "379/749/preview_CHSDM_BC0DBD6EF38D2_1.jpg",
              "measurements": {
                "dimensions": [
                  {
                    "dimension": "height",
                    "units": "pixels",
                    "value": 350
                  },
                  {
                    "dimension": "width",
                    "units": "pixels",
                    "value": 252
                  }
                ],
                "filesize": {
                  "units": "bytes",
                  "value": 35854
                }
              },
              "url": "https://ciim-static-media.s3.us-east-1.amazonaws.com/379/749/preview_CHSDM_BC0DBD6EF38D2_1.jpg"
            },
            "summary": {
              "title": "CHSDM-BC0DBD6EF38D2_1"
            },
            "type": "image"
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

###### Example 2
Request:
```
{
  object(identifier:"120873") {
    colors
  }
}
```

Response:
```
{
  "data": {
    "object": [
      {
        "colors": [
          "#7e7362",
          "#615747",
          "#a49785",
          "#d6c3ac",
          "#5a5448",
          "#413829",
          "#3a362b",
          "#7a7266",
          "#a19a8d",
          "#ecd9c3"
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
```

#### Arguments
These are all the possible arguments for an object query:
```
page: int
size: int
sort: [{arg1: order}, {arg2: order}] 
aggregations: [field,field]

general: string

agentId: string
agent: string
collectionsOnlineId: string
country: string
culture: string
colors: string
department : string
departmentId: string
displayed: boolean
dynasty: string
exhibition: string
exhibitionId: string
geography: string
hasImages: boolean
identifier: string
id: string
loaned: boolean
maker: string
makerId: string
material: string
name: string
onDisplay: boolean
period: string
provenance: string
reign: string
summary: string
subject: string
subjectId: string
title: string
year: YYYY
yearRange: {from:YYYY, to:YYYYY}
```

##### Sorting
Example sort by id:
```
{
  object(sort:[{id: "asc"}]){
       id
  }
}
```
The available sort terms are:
```
id
summary
year
```

#### Aggregations
You can create aggregations across different fields: 
```
{
object(aggregations:["department"]) {
     id    
  }
}
```
You can currently aggregate across these object fields:
```
classification
collector
culture
department
departmentID
maker
material
medium
period
place
provenance
subject
```
