가타카랑 그린 북 이 2개는 정말 감명 깊게 봤어요( 울었어요 )
시간 되시면 보시면 좋을거 같아요!! (보셨을지도..)

DELETE movies

PUT movies
{
  "settings": { "number_of_shards": 1, "number_of_replicas": 0 },
  "mappings": {
    "properties": {
      "title": { "type": "text" },
      "director": { "type": "keyword" },
      "release_year": { "type": "integer" },
      "genre": { "type": "keyword" }
    }
  }
}

POST movies/_doc
{
  "title": "가타카",
  "director": "앤드루 니콜",
  "release_year": 1997,
  "genre": ["SF", "드라마", "스릴러"]
}

POST movies/_doc
{
  "title": "노인을 위한 나라는 없다",
  "director": "코엔 형제",
  "release_year": 2007,
  "genre": ["스릴러", "범죄", "드라마"]
}

POST movies/_doc
{
  "title": "그린 북",
  "director": "피터 패럴리",
  "release_year": 2018,
  "genre": ["드라마", "코미디"]
}

POST movies/_doc
{
  "title": "기생충",
  "director": "봉준호",
  "release_year": 2019,
  "genre": ["드라마", "스릴러"]
}

POST movies/_doc
{
  "title": "인터스텔라",
  "director": "크리스토퍼 놀란",
  "release_year": 2014,
  "genre": ["SF", "드라마"]
}

# 전체 조회 (hits.total.value 가 5인지 확인)
GET movies/_search