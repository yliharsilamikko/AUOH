# Harjoitustyö
  
## 1) Toteuta koneistustietokanta REST-rajapinnalla
  
Toteuta CRUD operaatiot:
  
Lisää parametrisetti:
- POST /machining-parameter-set
  
Kysy kaikki parametrisetit:
- GET /machining-parameter-sets
  
Kysy tietty parametrisetti:
- GET /machining-parameter-set/:id
  
Päivitä parametrisetti:
- PUT /machining-parameter-set/:id
  
Poista parametrisetti:
- DELETE /machining-parameter-set/:id
  
Tietomalli:
Machining parameter set
-	string: Tool name  (e.g. Jyrsin 10mm)
-	string: Material (e.g. S355)
-	number: Cutting speed (e.g. 100 m/min)
-	number: Feed rate (e.g. 0.25 mm/teeth)
  
Extra:
- Lisää websocket yhteys, joka ilmoittaa jos jotain tietoja on muutettu


## 2) Julkaise palvelu herokuun


## 3) Palautus

- Lähetä sähköpostilla opettajalle rajapinnan url (qwerty.heroku.com tms..), sekä dokumentaatio kuinka rajapintaa käytetään
- Lähetä github-linkki, josta löytyy koodi
- Vaihtoehtoisesti koodin voi palauttaa zip-pakettina spostin mukana
- Palautus 30.4 mennessä!

## 4) Voit myös toteuttaa oman aiheen, jossa hyödynnetään WebSocket/REST -tekniikkaa.