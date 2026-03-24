# 🏛️ Assistente Open Data · dati.gov.it

Interfaccia di ricerca per il catalogo nazionale degli open data italiani ([dati.gov.it](https://www.dati.gov.it)).

**Demo live:** https://piersoft.github.io/ckan-opendata-assistant/

## Caratteristiche

- **Zero dipendenze** — un singolo file HTML, nessun framework, nessun server
- **Zero AI** — tutto deterministico, chiamate dirette alle API CKAN
- **Ricerca per parola chiave** con suggerimenti rapidi
- **Sfoglia per gruppo/tema** (13 categorie DCAT reali di dati.gov.it)
- **Sfoglia per organizzazione** (caricate dinamicamente con contatori)
- **Dettaglio dataset** con lista risorse e link diretto
- **Anteprima DataStore** — tabella dati inline per risorse con DataStore attivo
- **Ricerca avanzata multi-filtro** — keyword + tema + organizzazione + formato + licenza + ordinamento

## Deploy

### GitHub Pages (consigliato)
Il file `index.html` funziona direttamente su GitHub Pages senza build step.

1. Fork del repo
2. Settings → Pages → Source: `main` / `root`
3. Disponibile su `https://<tuousername>.github.io/ckan-opendata-assistant/`

### Server locale
```bash
# Python 3
python3 -m http.server 8080
# poi apri http://localhost:8080
```

### Nginx (sottopath)
Copia `index.html` in `/var/www/datigovit/ckan-assistant.html` e configura:
```nginx
location /datigovit/ {
    alias /var/www/datigovit/;
    index ckan-assistant.html;
}
```

## API utilizzate

Tutte le chiamate vanno a `https://www.dati.gov.it/opendata/api/3/action/`:

| Endpoint | Uso |
|---|---|
| `package_search` | Ricerca dataset, sfoglia temi/org, ricerca avanzata |
| `package_show` | Dettaglio dataset e risorse |
| `datastore_search` | Anteprima dati tabellari |

## Configurazione

Per puntare a un altro portale CKAN, cambia una riga in `index.html`:
```js
const CKAN_BASE = 'https://www.dati.gov.it/opendata/api/3/action';
// oppure:
const CKAN_BASE = 'https://tuo-ckan.example.com/api/3/action';
```

## Licenza

MIT — libero uso, modifica e redistribuzione.
