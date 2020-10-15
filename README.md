# docker-compose-env

ตัวอย่างกำหนด env file ให้กับ container

[docker-compose.yml](https://github.com/0x01code/docker-compose-env/blob/master/docker-compose.yml)
```
version: "3"

services:
    nginx:
        image: nginx:1.18.0-alpine
        container_name: nginx
        restart: always
        volumes:
            - ./docker/nginx/default.conf:/etc/nginx/conf.d/default.conf
        ports:
            - 80:80

    express:
        build:
            context: .
            dockerfile: ./docker/express/Dockerfile
        container_name: express
        restart: always
        # env_file จะดึงไฟล์ .env ไปใช้ใน container
        env_file:
            - .env
```

[express/routes/index.js](https://github.com/0x01code/docker-compose-env/blob/master/express/routes/index.js)
```
var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function (req, res, next) {
  // process.env.NAME
  // NAME คือ ตัวแปรที่มาจากไฟล์ .env
  res.json(
    {
      title: `Name Env : ${process.env.NAME}`
    }
  );
});

module.exports = router;

```
