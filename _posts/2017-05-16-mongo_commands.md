---
layout: post
title: MongoDB 명령어 (pymongo포함)
category: DB
---

## database 생성
```
> use hahaha
이렇게 하면 생성완료
show dbs를 하면 보이지는 않는다.

>db.새로생성할_콜렉션이름.insert({'a':1, 'zzdfdf':235345234})
이렇게 하고

>show dbs
를 하면 hahaha db가 보인다
```

---

## database 삭제
```
> use naver_movie
> show tables

> db.dropDatabase()
{ "dropped" : "naver_movie", "ok" : 1 }
```

---

## collections 삭제
```
> use naver_movie
> show tables
moviedata

> db.moviedata.drop()
true

///기존 콜렉션(moviedata)삭제 확인
>show tables
```

---

## documents 삭제
### _id에 따라 document(행)를 삭제

```
> db.moviedata.find()
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f3"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f4"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f5"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f6"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f7"), "gen" : [ "드라마", "에로" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f8"), "gen" : [ "한국" ] }
```
```
> db.moviedata.remove({'_id':ObjectId("58d0e0b63753322bb4b8c2f8")})
WriteResult({ "nRemoved" : 1 })
```
```
> db.moviedata.find()
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f3"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f4"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f5"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f6"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f7"), "gen" : [ "드라마", "에로" ] }
```

### 특정 조건에 따라 삭제 해당 document(행)를 삭제
```
> db.moviedata.find()
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f3"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f4"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f5"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f6"), "gen" : [ "한국" ] }
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f7"), "gen" : [ "드라마", "에로" ] }
```
```
///mongodb
> db.moviedata.deleteMany({'gen':['한국']})
{ "acknowledged" : true, "deletedCount" : 4 }

> db.moviedata.find()
{ "_id" : ObjectId("58d0e0b63753322bb4b8c2f7"), "gen" : [ "드라마", "에로" ] }
```
```
///pymongo (한국 밖에 []가 없다!!)
>>> c = MongoClient()
>>> c.naver_movie.moviedata.delete_many({'gen':'한국'})
```

---

## collection의 특정 필드만 삭제 (document는 그대로 있음)  
[참고사이트](http://stackoverflow.com/questions/22901788/remove-attribute-from-all-mongodb-documents-using-python-and-pymongo){:target="_blank"}  

```
///comment_count라는 필드 자체만 document에서 삭제하고 싶을 때

///mongodb
> db.moviedata.update({}, {$unset:{'comment_count':1}}, {multi:true})

///pymongo (둘다 가능한데, 위의 것은 deprecated라고 나옴)
> c.naver_movie.moviedata.update({}, {'$unset':{'comment_count':1}}, multi=True)
> c.naver_movie.moviedata.update_many({}, {'$unset':{'comment_count':1}})
```

---

## update

특정 필드의 값을 변경하기  
kor_title값을 '집으로...'에서 '집으로'로 변경하기  

```
db.moviedata.update({"_id" : ObjectId("58df83aa3753324ee0587337")}, {$set:{'kor_title':'집으로'}})
```

---

## field 추가
[참고사이트](http://stackoverflow.com/questions/7714216/add-new-field-to-a-collection-in-mongodb){:target="_blank"}

```
> db.moviedata.find()
{ "_id" : ObjectId("58d0d3163753322bb4b8c2db"), "kor_title" : "꿩먹고 알먹고", "movie_id" : 20030 }
{ "_id" : ObjectId("58d0d3163753322bb4b8c2dc"), "kor_title" : "끊어진 항로", "movie_id" : 20031 }

///'_id'로 찾고 update를 해도 됨

> db.moviedata.update({'movie_id':20030}, {$set:{'new_field':1}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

> db.moviedata.find()
{ "_id" : ObjectId("58d0d3163753322bb4b8c2db"), "kor_title" : "꿩먹고 알먹고", "movie_id" : 20030, "new_field" : 1 }
{ "_id" : ObjectId("58d0d3163753322bb4b8c2dc"), "kor_title" : "끊어진 항로", "movie_id" : 20031 }
```

---

## find()
### 특정 필드의 값들만 출력하기
```
///MongoDB
///_id는 출력하지 말고, kor_title, comment만 출력하기
> db.moviedata.find({}, {kor_title:1, comment:1, _id:0})
{ "kor_title" : "꿩먹고 알먹고", "comment" : "NO_COMMENT" }
{ "kor_title" : "끊어진 항로", "comment" : "NO_COMMENT" }
{ "kor_title" : "끝없는 욕망", "comment" : "NO_COMMENT" }
{ "kor_title" : "끝없이 하염없이", "comment" : { "jso0122(jins****)" : 10 } }
{ "kor_title" : "끼있는 여자는 밤이슬을 좋아한다", "comment" : { "wood****" : 1 } }
{ "kor_title" : "나", "comment" : { "가리(rkfh****)" : 1, "kdg0****" : 1, "최강기아(shin****)" : 1, "msn1****" : 10, "vlf1****
```
```
///pymongo
c = MongoClient(host='localhost', port=27017)

def getdata():
  lls = []
  cur = c.naver_movie.moviedata.find({}, {'kor_title':1, 'comment':1, '_id':0})
  [lls.append(i) for i in cur]
  return lls

getdata()
```

### 조건에 따라 찾기1

```
///'아저씨'가 kor_title인 document의 내용을 모두 출력한다
> db.moviedata.find({kor_title:'아저씨'})

///'아저씨'가 kor_title인 document에서 kor_title만 출력
> db.moviedata.find({kor_title:'아저씨'}, {kor_title:1})
{ "_id" : ObjectId("58e080c337533218e2bb738a"), "kor_title" : "아저씨" }

///'아저씨'가 kor_title인 document에서 comment_count만 출력
> db.moviedata.find({kor_title:'아저씨'}, {comment_count:1})
{ "_id" : ObjectId("58e080c337533218e2bb738a"), "comment_count" : 27281 }
```

### 조건에 따라 찾기2

```
///댓글 개수가 20000개 이상인 document들의 kor_title, year, comment_count를 출력
> db.moviedata.find({comment_count:{$gt:20000}}, {kor_title:1, year:1, comment_count:1})
```

---

## export
```
///현재 디렉토리 위치에 newdbexport.json이 생긴다
$ sudo mongoexport --db newdb -c restaurants --out newdbexport.json
```

---

## import
```
$ sudo mongoimport --db test -c abc --file /home/jw/documents/output.json
```

---

## collections의 field명만 출력

```
///comment_table collections의 field명들만
> Object.keys(db.comment_table.findOne())
```

---

## collections 정렬
```
///맨 뒤에서부터 4개의 document를 출력
> db.컬렉션이름.find().sort({_id:-1}).limit(4)
```

---

## collection내의 document 숫자 세기
```
///moviedata collection의 document 갯수
> db.moviedata.count()
```

---

## collection 크기 확인
```
///kb단위
> db.콜렉션이름.stats(1024)

///mb단위
> db.콜렉션이름.stats(1024 * 1024)
```
