---
layout: post
title: Node.js mvc 시작하기 (구조생성)
category: etc
---

## 방법1

```
먼저, 폴더를 만들고(ex: /nodejs/jadetest) 해당 디렉토리로 들어가서 아래 명령어를 실행
jw@jw-Lenovo ~/Documents/nodejs/jadetest $ npm init

This utility will walk you through creating a package.json file.  
It only covers the most common items, and tries to guess sensible defaults.  
 
See `npm help json` for definitive documentation on these fields and exactly what they do.  
 
Use `npm install <pkg> --save` afterwards to install a package and  
save it as a dependency in the package.json file.  

Press ^C at any time to quit.
name: (jadetest)
version: (1.0.0)
description: test
entry point: (index.js)
test command:
git repository:
keywords:
author: jww
license: (ISC)
About to write to /home/jw/Documents/nodejs/jadetest/package.json:

{
  "name": "jadetest",
  "version": "1.0.0",
  "description": "test",
  "main": "index.js",
  "scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "jww",
  "license": "ISC"
}

Is this ok? (yes) yes
```

package.json 수정
```
$vi package.json

{
  "name": "jadetest",
  "version": "1.0.0",
  "description": "test",
  "main": "index.js",
  "scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "jww",
  "license": "ISC",

  /// 아래 내용을 추가
  "dependencies":{
    "express":"3.3.7",
    "jade":"*"
  }
}
```

```
$ npm install
$ pwd
/Documents/nodejs/jadetest

$ mkdir views
$ mkdir routes
$ mkdir public
$ vi app.js   // github에서 확인
```

```
$ cd routes
$ vi index.js
$ vi user.js

jw@jw-Lenovo ~/Documents/nodejs/jadetest/routes $ cd ..
jw@jw-Lenovo ~/Documents/nodejs/jadetest $ cd views
$ vi layout.jade    // github에서 확인
$ vi index.jade   // github에서 확인

jw@jw-Lenovo ~/Documents/nodejs/jadetest/views $ cd ..
jw@jw-Lenovo ~/Documents/nodejs/jadetest $ cd public/
jw@jw-Lenovo ~/Documents/nodejs/jadetest/public $ ls
jw@jw-Lenovo ~/Documents/nodejs/jadetest/public $ mkdir stylesheets
jw@jw-Lenovo ~/Documents/nodejs/jadetest/public $ cd stylesheets/
jw@jw-Lenovo ~/Documents/nodejs/jadetest/public/stylesheets $ vi style.css    // github에서 확인

jw@jw-Lenovo ~/Documents/nodejs/jadetest/public/stylesheets $ cd ..
jw@jw-Lenovo ~/Documents/nodejs/jadetest/public $ cd ..
jw@jw-Lenovo ~/Documents/nodejs/jadetest $ ls
app.js package.json public views node_modules routes
jw@jw-Lenovo ~/Documents/nodejs/jadetest $ node app.js
```

---

## 방법2

```
$ sudo npm install -g express-generator
/// 폴더를 미리 만들지 않는다
$ express --session --ejs --css stylus abc #abc는 폴더이름. 짧게는 $ express abc 로 해도 된다.
$ cd abc
$ npm i


$ vi app.js
    ---------
    ///다음 내용을 추가
    var app = express();
    app.set('port', process.env.PORT || 2999);
    http.createServer(app).listen(app.get('port'), function(){
    console.log('Express server listening on port' +app.get('port'));
    }); // 이걸 추가하고 실행해도 되고
    ---------
혹은 npm i까지 한 후 vi app.js에 내용을 따로 추가하지 않고
$ npm start 해도 결과는 동일하다.
```

---

npm start와 node main.js의 차이  
&rarr; npm start를 하면 package.json에서 start를 찾아 프로그램이 시작된다.
