### Media

Media exists as an aspect of Object records. As such, media is not queryable on its own and can only be retrieved as part of an object.

The best way to find records with media is to include the `hasMedia: true` flag to your query, for example:
```
{
  object(hasImages:true) {
    id    
    multimedia
  }
}
```

#### cc0
If an object record has a linked media record, and its rights contain ‘CC0’ then all the linked media will be CC0. It is based on the TMS data rule from Cooper Hewitt this moment (202207). When a record is CC0, both the object and media link will have the CC0 flag which can be seen in multimedia.cc0 and legal.cc0. If a record has no multimedia.cc0/legal.cc0 field at all, then it is not CC0. In other words, the CC0 flag is only on the record when the record is CC0.

Please see the response from the request as an example,

```
{
  "data": {
    "object": [
      {
        "multimedia": [
          {
            "cc0": true,
            "datatype": {
              "actual": "image",
              "base": "media"
            },
            "department": [
              {
                "@admin": {
                  "id": "department-25",
                  "source": "tms",
                  "status": "public",
                  "uuid": "4dd6611b-dc73-3841-8154-209e3436cc34"
                }
              }
            ],
            "id": "media-68817",
            "large": {
              "format": "jpeg",
              "location": "68/817/large_1916_29_111_01_RS.jpg",
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
                    "value": 1641
                  }
                ],
                "filesize": {
                  "units": "bytes",
                  "value": 193869
                }
              },
              "url": "https://ciim-static-media.s3.us-east-1.amazonaws.com/68/817/large_1916_29_111_01_RS.jpg"
            },
            "legal": {
              "rights": [
                {
                  "holder": "Cooper-Hewitt, National Design Museum, Smithsonian Institution",
                  "type": "copyright"
                }
              ]
            },
            "original": {
              "format": "jpeg",
              "location": "68/817/1916_29_111_01_RS.jpg",
              "measurements": {
                "dimensions": [
                  {
                    "dimension": "height",
                    "units": "pixels",
                    "value": 1872
                  },
                  {
                    "dimension": "width",
                    "units": "pixels",
                    "value": 3000
                  }
                ],
                "filesize": {
                  "units": "bytes",
                  "value": 3543848
                }
              },
              "processed": true,
              "url": "https://ciim-static-media.s3.us-east-1.amazonaws.com/68/817/1916_29_111_01_RS.jpg"
            },
            "preview": {
              "format": "jpeg",
              "location": "68/817/preview_1916_29_111_01_RS.jpg",
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
                    "value": 561
                  }
                ],
                "filesize": {
                  "units": "bytes",
                  "value": 54057
                }
              },
              "url": "https://ciim-static-media.s3.us-east-1.amazonaws.com/68/817/preview_1916_29_111_01_RS.jpg"
            },
            "summary": {
              "title": "1916_29_111_01_RS.jpg"
            },
            "type": "image"
          }
        ],
        "legal": {
          "cc0": true,
          "credit": "Gift of Georgina and Louisa L. Schuyler",
          "rights": [
            {
              "details": "no information in file",
              "type": "copyright"
            }
          ]
        }
      }
    ]
  }
}
```

#### Media Artifacts
These are the fields within the `multimedia` block. Each entry will contain several sizes of media, referred to as 'artifacts'. 
The current artifacts are:
  - `preview`: 350px on its shortest side.
  - `large`: 1024px on its shortest side.
  - `zoom`: A zoomable pyramid tiff generated from the source image. Only generated for media whose original is at least 300px on its shortest side.
  - `original`: The original image asset, published where the object is licensed as CC0.

The generated artifacts are stored in Amazon S3, and can be found at the `url` for the respective artifact block. For example: `multimedia.preview.url`

If an object record falls under the CC0 license, its media link will contain `cc0: true`, else there will not be a `cc0` field on the link. For example, see [this record](https://ch-api.ch-dev-use.link/?query=%7B%0A%20%20object(identifier%3A%229346%22)%7B%0A%09%09id%0A%20%20%20%20multimedia%20%20%20%20%0A%20%20%7D%0A%7D).

Linked media data may also contain Google Vision AI enhancements which show the RGB and hex values of the Google Vision color detection. The hex values are also copied to `colors` as a string of hex values. The Google Vision data is visible under `gvision.colors`

An example of color searching can be found [here](https://ch-api.ch-dev-use.link/?query={%0A%20%20object(colors%3A%22%238eabae%22)%20{%0A%20%20%20%20id%0A%20%20%20%20colors%0A%20%20%20%20multimedia%0A%20%20}%0A}).

```
"gvision": {
  "colors": [
    {
      "confidence": "58.85",        # The AI's confidence of the result in %
      "fraction": 0.37141976,       # The fraction of pixels the color occupies in the image [0-1]
      "hex": "#8eabae",             # The hex value of the color
      "rgb": {
        "blue": 174,        
        "green": 171,
        "red": 142,
        "value": "142, 171, 174"    # The combined RGB values
      }
    }
  ]
},
```

To search for object records that have color data, you can add a search filter `hasColors:true`. For example:
```
{
  object(hasColors:true) {
    id
    color
  }
}
```

#### Specific Media Artifacts
There is a separate search point that can be used if you know specifically which media artifact you are interested in.

```
{
  object(hasImages:true) {
    media {
      id
      large
      preview
      zoom
      original
    }
  }
}
```


