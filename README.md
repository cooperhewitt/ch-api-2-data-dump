# API - GraphQL Query Documentation with examples

## Quick links:
### Entities: 

- [Agent](/entities/agent.md)
- [Department](/entities/department.md)
- [Exhibition](/entities/exhibition.md)
- [Location](/entities/location.md)
- [Object](/entities/object.md)
  - [Media](/entities/media.md)
- [Package](/entities/package.md)
- [Tag](/entities/tag.md)
- [Term](/entities/term.md)

### Extras:
- [Aggregations](/extras/aggregations.md)
- [Pagination](/extras/pagination.md)
- [Fragments](/extras/fragments.md)
- [Error Handling](/extras/error_handling.md)


### Examples:
- [What Objects did Dieter Rams make in the 60s?](/examples/example1.md)
- [Get me all the Objects where "Winslow Homer" is the Subject.](/examples/example2.md)
- [What Objects were part of 'The Jazz Age' Exhibition and who made them?](/examples/example3.md)
- [Find me a Wooden chair from the 50s that is on display.](/examples/example4.md)
- [Find French Makers and the Objects they made.](/examples/example5.md)

## Introduction
GraphQL queries follow this basic structure:
```
{
  object (arguments) {
    fields
  }
}
```
The resultant data follows the same structure as the query
```
{
  "data": {
    "object": {
      "field": value
    }
  }
}
```
There is also an extensions block in addition to the data response. This follows the GraphQL specifications and allows us to write more detailed responses, including information regarding pagination and aggregations.

```
  "extensions": {
    "aggregations": {
      "department": {
        "buckets": [
          {
            "key": "Drawings, Prints, and Graphic Design Department",
            "doc_count": 129079
          },
          {
            "key": "Product Design and Decorative Arts Department",
            "doc_count": 28924
          },
          ...
        ]
      }
    },
    "pagination": {
      "hits": 196951,
      "per_page": 10,
      "current_page": 0,
      "number_of_pages": 19696
    }
  }
```
