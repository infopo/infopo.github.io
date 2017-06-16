---
layout: post
title: pymongo로 MongoDB 연결
category: Python
---


```python
import sys

#from pymongo import Connection # deprecated
from pymongo import MongoClient
from pymongo.errors import ConnectionFailure
```

<br>

```python
def main():
    try:
        c = MongoClient(host="IP_주소", port=27017)
        print(c.test.fromlenovo.insert_one({'eng_title': '2000', 'kor_title': 'fadfasdfsadf', 'movie_id': 11111}))
        print ('connected successfully')
        print (c)
    except ConnectionFailure as e:
        sys.stderr.write('could not connect to MongoDB: %s' % e)
        sys.exit(1)

if __name__ == '__main__':
    main()
```

    <pymongo.results.InsertOneResult object at 0x7f25f063d3f0>
    connected successfully
    MongoClient(host=['IP_주소:27017'], document_class=dict, tz_aware=False, connect=True)
