# Auroraliiga Analytics

Naisten jääkiekon Auroraliigan (ent. Naisten Liiga) data-analyysityökalu kolmelta kaudelta (2023-2026).

## Data

- **42 154 laukausta** kolmelta kaudelta
- **432 ottelua** (144 per kausi)
- **9 joukkuetta**: HIFK, HPK, Ilves, K-Espoo, KalPa, Kuortane, Kärpät, RoKi, TPS
- **xG-malli**: Logistinen regressio (etäisyys + kulma)

## Ominaisuudet

- **Sarjataulukko** — perinteinen taulukko + xG-tilastot
- **Laukaisukartta** — kaikki laukaukset kaukalokartalla (maali/torjunta/peitetty/ohi)
- **Pelaajat xG-pörssi** — kuka ylittää/alittaa maaliodottaman
- **Ilves-analyysi** — 3 kauden kehityskaari

## Käyttöönotto (GitHub Pages)

1. Luo uusi GitHub-repositorio
2. Kopioi kaikki tiedostot repoon:
   ```
   index.html
   data/
     shots.json
     games.json
     teams.json
     players.json
     xg_model.json
   ```
3. Settings → Pages → Source: `main` / `root`
4. Sivu on käytettävissä osoitteessa `https://<käyttäjänimi>.github.io/<repo>/`

## Datan päivittäminen

Aja scrape-skriptit uudelleen ja korvaa JSON-tiedostot:
- `scrape_auroraliiga.py` → ottelutiedot
- `scrape_laukaukset.py` → laukaisudata

## xG-malli

Yksinkertainen logistinen regressio:

```
xG = 1 / (1 + exp(-(a + b × etäisyys + c × kulma)))
```

Parametrit: a = -0.497, b = -0.208, c = -0.014

Sovitettu 42 154 laukaukseen. Kalibroitu: yhteensä xG ≈ toteutuneet maalit.

## Datalähde

Kaikki data haettu [tulospalvelu.leijonat.fi](https://tulospalvelu.leijonat.fi/) -rajapinnasta.
