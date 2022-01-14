# Javascript nopeat perusteet



## Tietotyypit
```javascript
let v;          // Muuttuja
let v = 1234;   // Numero
let v = "1234"; // Teksti
let v = true;   // Boolean
let v = {};     // Objekti
let v = [];     // Lista 
```

## Perusoperaatiot
```
+
-
*
/
%
++
--
```

## Muuttujien skooppi
```javascript
var v1 = 1234; // Globaali muuttuja
let v2 = 1234; // Paikallinen muuttuja
const v3 = 1234;// Muuttumat muuttuja
```

## Luokka
```javascript
class Order{
    constructor(id, content){ // Luokan konstruktori
        this.id = id;
        this.content = content;
    }

    Summarize(){ //Luokan metodi
        return 'orderId:' + this.id + " content:" + this.content;
    }
}
let order = new Order(1234, "asdf");
let summary = order.Summarize();
console.log(summary);
```

## Objektin alustus ilman luokkaa
```javascript
let order = {
    id: 1234,
    content: "asdf",
    Summarize(){
        return 'orderId:' + this.id + " content:" + this.content;
    }
}
let summary = order.Summarize();
console.log(summary);
```

## Funktiot
```javascript
let order = {
    id: 1234,
    content: "asdf"
}

const summarize = (order)=>{  // Arrow function
    return 'orderId:' + order.id + " content:" + order.content;
};

function summarize_2(order){
    return 'orderId:' + order.id + " content:" + order.content;
}

let summary = summarize(order);
console.log(summary);
let summary2 = summarize_2(order);
console.log(summary2);
```

## Rinnakkaisuus
Alla kaksi apufunktiota, joita käytetään rinnakkaisuutta käsittelevissä esimerkeissä
```javascript
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

function sleep_sync(milliseconds) {
  const start = new Date();
  for (let i = 0; i < 1e8; i++) {
    if (new Date() - start > milliseconds) {
      break;
    }
  }
};

```

## Callback-funktiot
```javascript
let order = {
    id: 1234,
    content: "asdf"
}
const summarize = (order, callback)=>{
    callback('orderId:' + order.id + " content:" + order.content);
};
summarize(order, console.log);
```


## Asynkroninen funktio, joka vastaanottaa callback-funktion
```javascript
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

let order = {
    id: 1234,
    content: "asdf"
}
const summarize = async(order, callback)=>{
    await sleep(2000);
    callback('orderId:' + order.id + " content:" + order.content);
};

console.log("before call");
summarize(order, console.log);
console.log("after call");
```


## Asynkroninen funktio, joka palauttaa Promisen
```javascript
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

let order = {
    id: 1234,
    content: "asdf"
}
const summarize = async(order)=>{
    await sleep(2000);
    return 'orderId:' + order.id + " content:" + order.content;
};

console.log("before call");
summarize(order).then((summary)=>{console.log(summary)});
console.log("after call");
```

## Luokan asynkroninen metodi, joka palauttaa Promisen
```javascript
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

class Order{
    constructor(id, content){ // Luokan konstruktori
        this.id = id;
        this.content = content;
    }

    async Summarize(){ //Luokan metodi
        sleep(2000);
        return 'orderId:' + this.id + " content:" + this.content;
    }
}
let order = new Order(1234, "asdf");
let summary = order.Summarize().then(console.log);
```

## Virheenkäsittely
```javascript
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

class Order{
    constructor(id, content){ // Luokan konstruktori
        this.id = id;
        this.content = content;
    }

    async Summarize(){ //Luokan metodi
        sleep(2000);
        throw new Error('Virhe datan käsittelyssä');
        //return 'orderId:' + this.id + " content:" + this.content;
    }
}
let order = new Order(1234, "asdf");
let summary = order.Summarize()
    .then(console.log)
    .catch((err)=>{console.log("ERROR: " + err)});
```