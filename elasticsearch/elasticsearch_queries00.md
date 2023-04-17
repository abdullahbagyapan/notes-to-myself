# ElasticSearch Console Commands

## 1) Create New Index.
    PUT lesson
**Create index which name is 'lesson'**

<hr>

## 2) Add Document to Index
    POST lesson/_doc
    {
        "lesson_name":"mathematics",
        "lesson_credits":3.0
    }
**Add new document ('row') to lesson**

<hr>

## 3) Get All Documents
    GET lesson/_search
    {
        "query":{
            "match_all":{}
        }
    }

<hr>

## 4) Get Document By Id
     GET lesson/_search/'_id'

<hr>

## 5) Update Document Field By Id
    POST lesson/_update/'_id'
    {
        "doc":{
                "lesson_credits":4.0
        }
    }

<hr>

## 6) Mapping field

    PUT lesson
    {
        "mappings":{
            "properties":{
                "lesson_name":{"type":"text"},
                "lesson_credits":{"type":"float"},
                "lesson_time":{"type":"integer"},
                "teacher":{
                    "properties":{
                        "teacher_name":{"type":"text"},
                        "teacher_age":{"type":"integer"}
                    }
                }
            }
        }
    }

<br>

**If we check by 'GET lesson/_mapping' output will be like that :**

```json
{
  "lesson": {
    "mappings": {
      "properties": {
        "lesson_credits": {
          "type": "float"
        },
        "lesson_name": {
          "type": "text"
        },
        "lesson_time": {
          "type": "integer"
        },
        "teacher": {
          "properties": {
            "teacher_age": {
              "type": "integer"
            },
            "teacher_name": {
              "type": "text"
            }
          }
        }
      }
    }
  }
}
```