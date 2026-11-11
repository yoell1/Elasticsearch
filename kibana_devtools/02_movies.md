# [실습] movies 인덱스 - 매핑 지정 후 영화 5편 입력

# 기존 인덱스 삭제 (처음 실행이면 404가 나와도 무시)
```
DELETE movies
```

# 인덱스 생성 (매핑 지정)
```
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
```

# 문서 추가 (영화 5편)
```
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
```

# 전체 조회 (hits.total.value 가 5인지 확인)
```
GET movies/_search
```

---

### 실습하며 알게 된 것
- JSON은 필드 사이마다 쉼표(`,`)가 필요함. 빠지면 다음 줄에 에러 표시가 뜸
- `genre`는 `keyword` 타입이라 문자열 전체가 값 하나로 저장됨 → 장르별로 검색·집계하려면 배열로 나눠 넣기
- `PUT movies`를 두 번 실행하면 `resource_already_exists_exception` → `DELETE movies` 후 다시 생성
- `POST movies/_doc`는 실행할 때마다 ID가 새로 생겨서 두 번 실행하면 같은 문서가 2개 생김 → `PUT movies/_doc/1`처럼 ID를 지정하면 덮어써서 중복이 안 생김