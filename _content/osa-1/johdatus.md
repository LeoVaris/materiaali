## Johdatus web-sovelluksiin

### Selain ja palvelin

Web-sovellusten toiminta perustuu HTTP-protokollaan, jossa selain lähettää palvelimelle pyyntöjä ja palvelin vastaa pyyntöihin. Selain voi pyytää palvelimelta esimerkiksi HTML-tiedoston, joka kuvaa nettisivun sisällön, ja näyttää sivun sitten käyttäjälle.

Esimerkiksi seuraavassa kuvassa selain pyytää HTML-tiedostoa `index.html`. Palvelin lähettää tiedoston sisällön HTTP-koodilla 200, mikä tarkoittaa, että pyyntö onnistui.

TODO: Kuva tähän

Perinteinen tapa toteuttaa nettisivusto on luoda HTML-tiedostot käsin ja sijoittaa ne palvelimella olevaan hakemistoon. Tämän rajoituksena on kuitenkin, että palvelimella olevat sivut ovat _staattisia_ eli aina kun käyttäjä lataa tietyn sivun, se näyttää samalta.

Tällä kurssilla opimme toteuttamaan web-sovelluksia, jotka luovat _dynaamisia_ sivuja tietokannan sisällön perusteella ja tallentavat käyttäjien antamaa tietoa tietokantaan. Tämä antaa valtavasti lisää mahdollisuuksia verrattuna staattisiin sivuihin.

### Ensimmäinen web-sovellus

Aloitamme ensimmäisen web-sovelluksen tekemisen luomalla sovellusta varten hakemiston `sovellus` ja siirtymällä sinne:

```bash
$ mkdir sovellus
$ cd sovellus
```

Jotta voimme kätevästi hallinnoida sovelluksen tarvitsemia kirjastoja, luomme hakemistoon Pythonin virtuaaliympäristön seuraavalla komennolla:

```bash
$ python3 -m venv venv
```

Tämä komento luo hakemiston `venv`, jonka sisällä on Pythonin suoritusympäristö sovellusta varten. Saamme virtuaaliympäristön käyntiin suorittamalla aktivointikomennon näin:

```bash
$ source venv/bin/activate
```

Tämän seurauksena komentorivin alkuun ilmestyy tunnus `(venv)` merkkinä siitä, että olemme virtuaaliympäristössä. 
Kun olemme virtuaaliympäristössä, voimme asentaa Python-kirjastoja paikallisesti niin, että ne ovat käytettävissä vain kyseisessä virtuaaliympäristössä emmekä tarvitse asennukseen pääkäyttäjän oikeuksia. Asennamme ensin `flask`-kirjaston:

```bash
(venv) $ pip install flask
```

Nyt meillä on pystyssä ympäristö, jossa voimme suorittaa web-sovelluksen. Tehdään testiksi yksinkertainen sovellus tiedostoon `app.py`:

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def index():
    return "Heipparallaa!"
```

Sovelluksen ideana on, että se näyttää tekstin `"Heipparallaa!"`, kun menemme sovelluksen etusivulle. Saamme sovelluksen käyntiin näin:

```bash
(venv) $ flask run
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Viimeisellä rivillä näkyy osoite, jonka kautta voimme käyttää sovellusta nettiselaimella. Kun menemme sivulle `http://127.0.0.1:5000/`, näemme sovelluksen:

TODO: Kuva tähän

Sovellus sulkeutuu painamalla Control+C komentorivillä, jolloin voimme tehdä jotain muuta komentorivillä tai käynnistää sovelluksen uudestaan.

Komento `deactivate` lopettaa virtuaaliympäristön käyttämisen ja palauttaa komentorivin takaisin tavalliseen tilaan:

```bash
(venv) $ deactivate
$ 
```

Huomaa, että tämän jälkeen emme voi enää käynnistää sovellusta, koska Flask-kirjasto on asennettu vain virtuaaliympäristöön.