# Korkkipeli

Moninpelattava reaktiopeli selaimessa. WebRTC peer-to-peer, ei palvelinta.

**Pelaa:** https://anttir.github.io/pullonkorkkipeli/

## Säännöt

1. Klikkaa vastustajan palloa **hyökätäksesi**
2. Vastustajan pitää klikata sinun palloasi ennen timerin loppumista **torjuakseen**
3. Torjunta = vastahyökkäys → ketju jatkuu, timer lyhenee (2.0s → 1.8s → ... → 0.2s)
4. Kun joku ei ehdi → ketju päättyy, **voittaja saa pisteet = ketjun pituus**

## Käyttö

- **Luo peli** → jaa 6-numeroinen koodi
- **Liity** → syötä koodi
- Oma pallo alhaalla (vihreä), klikkaa sitä vaihtaaksesi nimeä

## Teknologia

HTML + CSS + JS, PeerJS (WebRTC), GitHub Pages
