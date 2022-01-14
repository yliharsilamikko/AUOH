# HTTP-serveri + HTTP-kyselyiden luonti

- Luo uusi tyhjä kansio harjoitukselle
- Avaa VSCodella kansio
- Kutsu npm init
- Lisää app.js-tiedosto
- Lisää package.json:iin "start"-komento, joka käynnistää app.js-tiedoston nodella.
- Asenna tarvittavat paketit
    - npm install express
    - npm install axios


## Hello World -palvelin
```javascript
const express = require('express');
const PORT = process.env.PORT || 8081;

let app = express();

app.use((req, res, next) => {
    console.log('PATH: ' + req.path);
    next();
});

app.get('/', (req, res, next) => {
    res.send('Hello');
});

app.listen(PORT);
```
- Käynnistä sovellus `npm run start`
- Mene selaimella http://localhost:8081/


## HTTP-kyselyn luonti
```javascript
const axios = require('axios');
axios.get('https://gorest.co.in/public/v1/users').then(
    (res)=>{console.log(res.data);}
);
```


## Luodaan REST-rajapinta, joka palauttaa aktiivisten käyttäjien lukumäärän
Rajapinnan osoite on:
http://localhost:8081/users/active/count

```javascript
const express = require('express');
const axios = require('axios');

const PORT = process.env.PORT || 8081;

let app = express();

app.use((req, res, next) => {
    console.log('PATH: ' + req.path);
    next();
});

app.get('/', (req, res, next) => {
    res.send('Hello');
    res.end();
});

app.get("/users/active/count", (req, res, next) => {
  axios.get("https://gorest.co.in/public/v1/users").then((users_res) => {
    let count = 0;
    const users = users_res.data.data;
    users.forEach(user => {
        if(user.status == 'active')
        {
            count++;
        }
    });
    res.send({count});
  });
});

app.listen(PORT);
```