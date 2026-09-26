# Analisi del Sito e Piano di Migliorie Tecniche
**Sito web:** [danielaledonne.it](https://danielaledonne.it/)  
**Professionista:** Dott.ssa Daniela Ledonne – Psicologa Psicoterapeuta (Roma)  
**Data ultimo aggiornamento:** Settembre 2026  

---

## Indice
1. [Sintesi dello Stato Attuale](#1-sintesi-dello-stato-attuale)
2. [Interventi Completati (Changelog)](#2-interventi-completati-changelog)
3. [Nuovi Findings e Aree di Miglioramento](#3-nuovi-findings-e-aree-di-miglioramento)
   - [3.1 UI, Design e Accessibilità (WCAG AA)](#31-ui-design-e-accessibilità-wcag-aa)
   - [3.2 UX e Ottimizzazione Conversioni](#32-ux-e-ottimizzazione-conversioni)
   - [3.3 Prestazioni e Core Web Vitals (CWV)](#33-prestazioni-e-core-web-vitals-cwv)
   - [3.4 Privacy, Cookie e Conformità GDPR](#34-privacy-cookie-e-conformità-gdpr)
4. [Tabella di Prioritizzazione Aggiornata](#4-tabella-di-prioritizzazione-aggiornata)

---

## 1. Sintesi dello Stato Attuale

Il sito ha compiuto importanti passi avanti in termini di identità visiva, prestazioni e SEO locale:
- **Identità fotografica personalizzata:** Tutte le immagini dei servizi terapeutici ritraggono ora sessioni realistiche e coordinate in uno studio romano luminoso, con la terapeuta in primo piano di spalle e focus empatico sui pazienti.
- **Peso delle immagini ridotto del 91.4%:** Payload complessivo delle immagini ridotto da oltre 3.2 MB a 274 KB tramite conversione in WebP ad alta fedeltà.
- **Canali di contatto professionali:** Sostituiti i semplici link testuali con Contact Cards e Social Pills monocromatiche, touch-friendly (>48px) e sicure (`target="_blank"`).
- **SEO Locale & Dati Strutturati:** Pienamente integrati Schema.org JSON-LD con le 2 sedi di Roma (Trieste e Monte Sacro), `robots.txt` e tag `canonical`.

Le priorità attuali si concentrano su:
1. **Accessibilità visiva (Contrasti cromatici a norma WCAG AA).**
2. **Call-to-Action principale nell'Hero Header.**
3. **Lazy-loading e attributi dimensionali anti-CLS.**
4. **Adeguamento Privacy / GDPR per Google Analytics.**

---

## 2. Interventi Completati (Changelog)

- [x] **Riordino delle Sezioni UX:** *Chi sono* $\rightarrow$ *Come posso aiutarti* $\rightarrow$ *Dove mi trovi* $\rightarrow$ *Contattami* $\rightarrow$ *Seguimi*.
- [x] **Floating Action Button WhatsApp:** Pulsante flottante sempre accessibile su desktop e mobile per avviare una chat diretta.
- [x] **SEO Locale (Schema.org JSON-LD):** Dati strutturati `Physician` e `MedicalClinic` con entrambe le sedi (Via Anapo, Via Val d'Ossola), specialità, telefono, email e profili social.
- [x] **SEO Tecnica & Indicizzazione:**
  - Abilitato `robots.txt` con inclusione esplicita di `sitemap.xml`.
  - Inserito il tag `<link rel="canonical" href="{{ .Permalink }}" />`.
  - Configurato `defaultContentLanguage = "it"` per generare `<html lang="it">`.
- [x] **Contact Cards & Social Pills:** Nuovi recapiti monocromatici per WhatsApp, Telefono, Telegram, Email, Maps, GuidaPsicologi, UnoBravo, Instagram, Facebook e LinkedIn.
- [x] **Gerarchia Intestazioni:** Titoli dei servizi in `services.md` corretti da `<h5>` a `<h3>` con stili tipografici dedicati (`.post-content h3`).
- [x] **Conversione Immagini in WebP:**
  - `cover-image.webp`: **40 KB** (era 1.5 MB, -97.3%)
  - `individual-therapy.webp`: **96 KB** (era 356 KB, nuova foto personalizzata con paziente giovane)
  - `family-therapy.webp`: **57 KB** (era 642 KB, nuova foto personalizzata con camicia chiusa e figlio al centro)
  - `couples-therapy.webp`: **74 KB** (era 692 KB, nuova foto personalizzata con dialogo espressivo e camicia chiusa)
  - `daniela_cropped_image.webp`: **11 KB** (era 67 KB, -83.5%, foto profilo ottimizzata con cornice e ombra morbida)

---

## 3. Nuovi Findings e Aree di Miglioramento

### 3.1 UI, Design e Accessibilità (WCAG AA)

#### Finding 1: Contrasto testo bianco su sfondo sezioni dispari (`#db3360`) (✅ Implementato)
- Impostato il nuovo colore primario **`#db3360`** per le sezioni dispari (*Chi sono*, *Dove mi trovi*, *Seguimi*) e i pulsanti dell'header.
- Rapporto di contrasto con il testo bianco portato a **`4.51:1`**, garantendo la piena conformità allo standard **WCAG 2.1 AA** e preservando l'identità visiva originale.

#### Finding 2: Eliminazione hover verde lime (`#86c440`) (✅ Implementato)
- Sostituito l'hover default del tema con una sfumatura lampone profonda coordinata (**`#b52048`**) sui pulsanti hero (`a.btn.site-menu:hover`), sul menu di scorrimento laterale (`.fn-item:hover` / `.fn-item.active`) e sui link nei contenuti.
- Contrasto e leggibilità garantiti su tutti gli stati interattivi.

---

### 3.2 UX e Ottimizzazione Conversioni

#### Finding 3: Gerarchia visiva dei pulsanti nell'Hero Header (✅ Risolto by-design)
- La funzione di Call to Action primaria di conversione è svolta in modo pervasivo ed efficace dal **pulsante flottante WhatsApp** (sempre visibile a schermo sia su desktop che su mobile, ad alto contrasto con icona e testo dedicato).
- I 4 pulsanti dell'Hero Header (*Chi sono*, *Come posso aiutarti*, *Dove mi trovi*, *Contattami*) fungono correttamente da **menu di navigazione rapida** (ancore di scorrimento) con pari dignità tra le sezioni del sito.

#### Finding 4: Foto profilo terapeuta (`daniela_cropped_image.webp`) (✅ Implementato)
- Convertita la foto profilo in formato **WebP ad alta qualità** (`11 KB` invece di 67 KB, **-83.5%**).
- Aggiunta cornice circolare morbida via CSS (`.profile-pic`) con ombra elegante e micro-hover.
- Inseriti attributi `loading="lazy"`, `decoding="async"` e dimensioni esplicite `width="170" height="170"` per azzerare il layout shift (CLS).
- Aggiornato il riferimento nell'oggetto Schema.org JSON-LD in `custom_head.html`.

---

### 3.3 Prestazioni e Core Web Vitals (CWV)

#### Finding 5: Lazy Loading e Attributi Dimensionali (Anti-CLS) (✅ Implementato)
- Aggiunti attributi `loading="lazy"` e `decoding="async"` su tutte le immagini dei servizi per posticipare il caricamento al momento dello scorrimento.
- Definite dimensioni native esplicite `width="1200" height="800"` con classe `.service-img` (`aspect-ratio: 3 / 2`, `height: auto`, angoli arrotondati a 12px e ombra leggera), azzerando completamente il *Cumulative Layout Shift* (CLS).
- Inseriti attributi `alt` descrittivi ricchi di parole chiave per la SEO locale.

#### Finding 6: Ottimizzazione Font Google e `font-display: swap` (✅ Implementato)
- Creato l'override pulito `static/css/fonts.css` nel repository del sito (preservando il submodule del tema intatto).
- Aggiunta la direttiva `font-display: swap;` a tutte le 20 dichiarazioni `@font-face` dei font locali del sito (Open Sans, Open Sans Condensed, Oswald, Roboto Slab).
- Eliminato il rischio di blocco del rendering del testo (*FOIT - Flash of Invisible Text*) all'avvio della pagina, migliorando il First Contentful Paint (FCP) e la reattività percepita.

---

### 3.4 Privacy, Cookie e Conformità GDPR

#### Finding 7: Tracciamento Google Analytics non conforme (✅ Implementato)
- Aggiornata la configurazione di Google Analytics 4 in [`layouts/partials/analytics-gtag.html`](layouts/partials/analytics-gtag.html).
- Abilitato esplicitamente **`'anonymize_ip': true`** per il mascheramento preventivo degli indirizzi IP dei visitatori.
- Disabilitati i segnali pubblicitari e di profilazione di terze parti (**`'allow_google_signals': false`**, **`'allow_ad_personalization_signals': false`**) per limitare l'uso di GA4 a finalità meramente statistiche e aggregate nel pieno rispetto del GDPR.

#### Finding 8: Assenza di Privacy & Cookie Policy nel footer
* **Situazione:** Nel footer ([`layouts/partials/footer.html`](layouts/partials/footer.html)) sono presenti solo i dati fiscali (P.IVA e numero iscrizione all'Ordine), ma manca il link all'Informativa sul Trattamento dei Dati Personali (GDPR).
* **Miglioria proposta:** Inserire nel footer un link a una pagina o modale con l'Informativa Privacy per pazienti e utenti del sito (gestione form di contatto, telefonate, WhatsApp ed email).

---

## 4. Tabella di Prioritizzazione Aggiornata

| Priorità | Ambito | Descrizione Intervento | Impatto | Stato |
| :---: | :--- | :--- | :---: | :---: |
| **1** | **Accessibilità (WCAG)** | Correggere il contrasto dello sfondo rosa (`#db3360`, 4.51:1) ed eliminare l'hover verde lime | 🔴 Alto | ✅ **Completato** |
| **2** | **UX / Conversioni** | Gerarchia CTA Hero Header vs navigazione interna | 🔴 Alto | ✅ **Risolto by-design (CTA WhatsApp)** |
| **3** | **Legale / GDPR** | Inserire Privacy & Cookie Policy nel footer e anonimizzare IP di Google Analytics | 🟡 Medio | Da fare |
| **4** | **Performance (CWV)** | Aggiungere `loading="lazy"` e dimensioni esplicite `width`/`height` sulle immagini dei servizi | 🟡 Medio | ✅ **Completato** |
| **5** | **Performance** | Ottimizzare la foto profilo in WebP e aggiungere `font-display: swap` sui web font | 🟢 Basso | ✅ **Completato** |
