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


