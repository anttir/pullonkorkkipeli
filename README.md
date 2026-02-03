# Korkkipeli

Moninpelattava reaaliaikainen reaktiopeli selaimessa. Digitalisoi perinteisen pullonkorkkien heittelypelin.

**Pelaa:** https://anttir.github.io/pullonkorkkipeli/

## Pelisäännöt

1. **Hyökkää** klikkaamalla toisen pelaajan palloa
2. Kohteen ruudulle ilmestyy timer sinun pallosi ympärille
3. Kohteen pitää **torjua** klikkaamalla sinun palloasi ennen timerin loppumista
4. Torjunta on samalla vastahyökkäys → ketju jatkuu!
5. Timer **lyhenee** joka vuorolla (2.0s → 1.8s → 1.6s → ... → 0.2s)
6. Kun joku ei ehdi → ketju päättyy, **voittaja saa pisteet = ketjun pituus**

### Strategia

- Hyökkää pelaajaa joka on jo kiinni toisessa ketjussa
- Priorisoi: jatkatko arvokasta ketjua vai puolustatko uutta hyökkäystä?
- Voit olla mukana useissa ketjuissa samanaikaisesti

## Käyttö

### Pelin luominen
1. Syötä nimesi
2. Klikkaa "Luo uusi peli"
3. Jaa 6-numeroinen koodi kavereille

### Peliin liittyminen
1. Syötä nimesi
2. Syötä huonekoodi
3. Klikkaa "Liity peliin"

### Pelin aikana
- **Klikkaa** vastustajan palloa hyökätäksesi tai torjuaksesi
- **Oma pallo** on alhaalla keskellä (vihreä)
- **Timer-kehä** näyttää kuinka kauan sinulla on aikaa vastata
- Klikkaa omaa palloa **vaihtaaksesi nimeä** (laittaa sinut pauselle)
- **Poistu**-nappi palauttaa lobbyyn

## Tekniset tiedot

- **Hostaus:** GitHub Pages (staattinen sivu)
- **Verkko:** PeerJS (WebRTC peer-to-peer)
- **Teknologia:** HTML, CSS, JavaScript (ei riippuvuuksia buildiin)
- **Pelaajat:** 2-20

### Parametrit

| Parametri | Arvo |
|-----------|------|
| Aloitustimer | 2.0 sek |
| Timer-lyhennys/vuoro | 0.2 sek |
| Minimi-timer | 0.2 sek |

## Kehitys

```bash
# Kloonaa repo
git clone https://github.com/anttir/pullonkorkkipeli.git

# Avaa selaimessa
open index.html

# Tai käytä local serveriä
python -m http.server 8000
```

## Lisenssi

MIT
