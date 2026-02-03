# Korkkipeli - Toteutussuunnitelma

## Konsepti
Moninpelattava reaktiopeli: pelaajat "heittävät korkkeja" klikkaamalla toistensa palloja ja torjuvat klikkaamalla takaisin ajoissa.

## Arkkitehtuuri
- Yksi HTML-tiedosto (inline CSS + JS)
- PeerJS WebRTC peer-to-peer
- Host välittää viestit pelaajien välillä
- GitHub Pages -hostaus

## Tila (state)

```
myId, myName, roomCode, isHost, isPaused
players: Map<id, {id, name, score, isPaused}>
myActiveChains: Map<chainId, {opponentId, turn, startTime, duration}>
myPendingAttacks: Map<targetId, chainId>
connections: Map<peerId, connection>
```

## Näkymät

### Lobby
- Nimi-input
- Huonekoodi-input + "Liity" (primary)
- "Luo peli" (secondary)

### Peli
- Pelaajat ympyrässä, oma pallo kello 6:ssa (eri väri)
- Timer-kehä pallon ympärillä (SVG circle, stroke-dashoffset animaatio)
- Pistetaulu, huonekoodi + kopiointipainike, poistu-nappi

## Pelimekaniikka

### Hyökkäys
1. Klikkaa vastustajan palloa
2. Tarkista: onko aktiivinen ketju tämän kanssa? → torjunta
3. Tarkista: onko jo lähetetty hyökkäys tälle? → nollaa timer (rangaistus)
4. Muuten: luo uusi ketju, lähetä `attack`-viesti

### Torjunta
1. Klikkaa hyökkääjän palloa ennen timerin loppumista
2. Poista oma aktiivinen ketju
3. Lähetä `attack`-viesti takaisin (turn + 1, lyhyempi duration)

### Ketjun päättyminen
- Timer loppuu → häviäjä menettää pisteet, voittaja saa (pisteet = ketjun pituus)
- Lähetä `chain_won`-viesti voittajalle

### Timer
- Alkuarvo: 2.0s, lyhenee 0.2s/vuoro, minimi 0.2s
- Tarkista 50ms välein, päivitä UI

## Verkkoviestit

| Viesti | Sisältö |
|--------|---------|
| join | player: {id, name, score, isPaused} |
| game_state | players: [...] |
| player_joined | player |
| player_left | playerId |
| player_update | player |
| attack | chainId, attackerId, turn, duration |
| chain_won | chainId, points |
| relay | from, to, payload (host välittää) |

## PeerJS-konfiguraatio
- Host peer ID: `korkkipeli_${roomCode}`
- Pelaaja peer ID: `korkkipeli_${myId}_${timestamp}`
- STUN-palvelimet: Google (stun.l.google.com:19302)
- Timeout: 15s

## UI-yksityiskohdat
- Oma pallo: vihreä, reunus
- Muut: sininen
- Timer-kehä: oranssi → punainen (< 30%)
- Kehän paksuus kasvaa ketjun edetessä
- Pisteilmoitus: +X vihreä / -X punainen, fade out
- Pause: klikkaa omaa palloa → nimen vaihto, himmennetty pallo

## Erikoistapaukset
- Ikkunan resize → renderöi pelaajat uudelleen
- Yhteys katkeaa → poista pelaaja, hävitä ketjut
- localStorage: tallenna pelaajan ID ja nimi
