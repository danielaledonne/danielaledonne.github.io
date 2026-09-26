# Analisi del Sito e Piano di Migliorie Suggerite
**Sito web:** [danielaledonne.it](https://danielaledonne.it/)  
**Professionista:** Dott.ssa Daniela Ledonne – Psicologa Psicoterapeuta (Roma)  
**Data analisi:** Settembre 2026  

---

## Indice
1. [Sintesi Generale](#1-sintesi-generale)
2. [Architettura delle Informazioni e Funnel UX](#2-architettura-delle-informazioni-e-funnel-ux)
3. [Prestazioni e Core Web Vitals (CWV)](#3-prestazioni-e-core-web-vitals-cwv)
4. [SEO Locale e Posizionamento su Google (Roma)](#4-seo-locale-e-posizionamento-su-google-roma)
5. [UI, Design e Accessibilità (A11y - WCAG AA)](#5-ui-design-e-accessibilità-a11y---wcag-aa)
6. [Privacy, Cookie e GDPR](#6-privacy-cookie-e-gdpr)
7. [Tabella di Prioritizzazione degli Interventi](#7-tabella-di-prioritizzazione-degli-interventi)

---

## 1. Sintesi Generale

Il sito presenta un'ottima impronta: è minimale, chiaro, veloce da navigare ed empatico nella comunicazione. La specializzazione in psicoterapia sistemico-relazionale e l'approccio orientato alla relazione emergono chiaramente.

Tuttavia, l'analisi tecnica ha evidenziato diverse aree di miglioramento che possono aumentare significativamente:
- **Tasso di contatto (conversioni):** facilitando la richiesta di primo colloquio da smartphone e desktop.
- **Visibilità su Google a Roma (SEO Locale):** tramite dati strutturati per studi medici/psicologici con due sedi.
- **Velocità di caricamento su reti mobili:** riducendo il peso delle immagini di oltre l'85%.
- **Accessibilità visiva:** risolvendo criticità di contrasto cromatico su testi e link.
- **Conformità legale (GDPR):** adeguando il tracciamento di Google Analytics e le informative.

---

## 2. Architettura delle Informazioni e Funnel UX

### 2.1 Riordino logico delle sezioni (✅ Implementato)
- **Nuovo ordine applicato nei file Markdown:**
  1. **Chi sono** (`weight: 1`) – Presentazione ed approccio sistemico-relazionale.
  2. **Come posso aiutarti** (`weight: 2`) – Servizi offerti (terapia individuale, familiare, di coppia) e disturbi trattati.
  3. **Dove mi trovi** (`weight: 3`) – Studi a Roma (Trieste, Monte Sacro) e sedute online.
  4. **Contattami** (`weight: 4`) – Modalità di primo contatto rassicuranti (telefono, WhatsApp, Telegram, email).
  5. **Seguimi** (`weight: 5`) – Profili social divulgativi.

### 2.2 Call to Action (CTA) principale nell'Hero Header
- **Situazione attuale:** I pulsanti dell'header sono tutti visivamente identici (`Chi sono`, `Come posso aiutarti`, `Dove mi trovi`, `Contattami`).
- **Miglioria proposta:** Introdurre un pulsante primario in evidenza con un'azione chiara (es. *"Richiedi un primo colloquio"* o *"Scrivimi su WhatsApp"*), mantenendo gli altri con stile secondario per la navigazione interna.

### 2.3 Floating Action Button per Mobile (WhatsApp / Telefono) (✅ Implementato)
- **Implementazione completata:**
  - Creato [`layouts/partials/custom_body.html`](layouts/partials/custom_body.html) con pulsante flottante WhatsApp (link diretto a `https://wa.me/393517193288` con messaggio introduttivo preimpostato, icona vettoriale SVG accessibile).
  - Stili dedicati aggiunti in [`static/css/custom.css`](static/css/custom.css): badge pillola su desktop con scritta *"Scrivimi su WhatsApp"*, collassamento automatico su schermi mobile (<=600px) in comodo pulsante circolare FAB touch-friendly in basso a destra.

---

## 3. Prestazioni e Core Web Vitals (CWV)

### 3.1 Peso e formato delle immagini (~3.2 MB totali)
Attualmente la sola pagina iniziale carica oltre 3.2 MB di immagini in formato JPEG non compresso ad altissima risoluzione:
- `cover-image.jpg`: **1.5 MB** (2048×1365 px)
- `couples-therapy.jpg`: **692 KB** (900×600 px)
- `family-therapy.jpg`: **642 KB** (900×600 px)
- `individual-therapy.jpg`: **356 KB** (900×601 px)

**Miglioria proposta:**
1. Convertire tutte le immagini in formato moderno **WebP** o **AVIF** con compressione bilanciata:
   - `cover-image.webp`: riducibile a **~100–140 KB** (-90%).
   - Immagini dei servizi: riducibili a **~35–50 KB** ciascuna (-93%).
   - Peso totale delle immagini: da ~3.2 MB a **meno di 300 KB**.
2. Aggiungere gli attributi `loading="lazy"` e `decoding="async"` a tutte le immagini sotto la piega iniziale (servizi e foto profilo).
3. Specificare `width` e `height` su ogni tag `<img>` per azzerare il *Cumulative Layout Shift* (CLS).

### 3.2 Pulizia e modernizzazione Script e Font
- **jQuery 1.11.3 (2015):** Il tema include una versione obsoleta di jQuery per gestire lo scorrimento e l'evidenziazione del menu. È possibile alleggerirla o sostituirla con JavaScript nativo moderno (`scroll-behavior: smooth`, `IntersectionObserver`).
- **Font Face non utilizzati:** [`themes/hugo-scroll/static/css/fonts.css`](file:///Users/maurizio/Projects/danielaledonne.github.io/themes/hugo-scroll/static/css/fonts.css) dichiara formati legacy (`.eot`, `.ttf`, `.svg`) per 4 famiglie distinte. Conviene mantenere esclusivamente i pesi utilizzati in formato compresso `.woff2` con direttiva `font-display: swap`.

---

## 4. SEO Locale e Posizionamento su Google (Roma)

### 4.1 Dati Strutturati Schema.org (JSON-LD) (✅ Implementato)
Per uno psicologo con studio a Roma, i dati strutturati sono fondamentali per comparire nel Google Knowledge Panel e nei risultati locali (Google Maps / Local Pack).

**Implementazione completata:** Inserito in `layouts/partials/custom_head.html` un blocco JSON-LD completo con le due sedi (Trieste e Monte Sacro), i contatti, le specialità e i link social:
```json
{
  "@context": "https://schema.org",
  "@type": "Physician",
  "name": "Dott.ssa Daniela Ledonne - Psicologa Psicoterapeuta",
  "medicalSpecialty": "Psychotherapy",
  "description": "Psicologa Clinica e Psicoterapeuta ad orientamento Sistemico-Relazionale a Roma. Terapia individuale, di coppia e familiare.",
  "url": "https://danielaledonne.it/",
  "telephone": "+393517193288",
  "email": "info@danielaledonne.it",
  "image": "https://danielaledonne.it/images/daniela_cropped_image.png",
  "priceRange": "$$",
  "location": [
    {
      "@type": "MedicalClinic",
      "name": "Studio di Psicoterapia - Quartiere Trieste",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "Via Anapo 26",
        "addressLocality": "Roma",
        "postalCode": "00199",
        "addressCountry": "IT"
      }
    },
    {
      "@type": "MedicalClinic",
      "name": "Studio di Psicoterapia - Monte Sacro",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "Via Val d'Ossola",
        "addressLocality": "Roma",
        "postalCode": "00141",
        "addressCountry": "IT"
      }
    }
  ],
  "sameAs": [
    "https://www.guidapsicologi.it/studio/dottssa-daniela-ledonne",
    "https://www.unobravo.com/psicologi/daniela-ledonne",
    "https://www.instagram.com/daniela_ledonne_psicologa/",
    "https://www.facebook.com/psicodanielaledonne/",
    "https://www.linkedin.com/in/danielaledonne/"
  ]
}
```

### 4.2 Abilitazione `robots.txt` e Tag `canonical` (✅ Implementato)
- In `config.toml`, rimosso `"robotsTXT"` dalla lista `disableKinds` e aggiunto `enableRobotsTXT = true`.
- Creato `layouts/robots.txt` con inclusione esplicita del riferimento a `sitemap.xml`.
- Aggiunto il tag `<link rel="canonical" href="{{ .Permalink }}" />` in `layouts/partials/custom_head.html`.

### 4.3 Attributo Lingua `lang="it"` (✅ Implementato)
- Verificata la configurazione `defaultContentLanguage = "it"` in `config.toml` che alimenta `<html lang="{{ site.Language.Lang }}">` in Hugo per corretta indicizzazione e screen reader.

---

## 5. UI, Design e Accessibilità (A11y - WCAG AA)

### 5.1 Contrasto Colori
- **Sfondo sezioni dispari (`#e15379`):** Il testo bianco su questo colore produce un contrasto di **3.67:1**, non conforme allo standard WCAG AA (minimo **4.5:1** per testo corpo).
- **Hover link (`#86c440` - verde lime):** Su sfondo rosa il contrasto crolla a **1.75:1** e su sfondo chiaro a **1.83:1**, risultando quasi illeggibile al passaggio del mouse.
- **Miglioria proposta:**
  - Sostituire il fucsia/rosa con una tonalità più satura o profonda (es. bordeaux scuro/marsala `#9e1b43` o verde salvia/ottanio elegante) che garantisca un contrasto superiore a 5:1.
  - Sostituire il verde lime dell'hover con un colore coordinato e leggibile.

### 5.2 Formattazione dei Canali di Contatto (✅ Implementato)
- Recapiti e canali esterni trasformati in eleganti **Contact Cards** e **Social Pills** monocromatiche con icone semplici e minimaliste, garantendo touch target ampio (>48px) e transizioni morbide all'hover.

### 5.3 Link Esterni Sicuri (✅ Implementato)
- Aggiunti `target="_blank" rel="noopener noreferrer"` a tutti i link verso servizi terzi (Google Maps, UnoBravo, GuidaPsicologi, Instagram, Facebook, LinkedIn, WhatsApp, Telegram).

### 5.4 Gerarchia Titoli e Layout Schede
- In `services.md`, sostituire i titoli `#####` (`<h5>`) con `###` (`<h3>`) per mantenere una corretta gerarchia semantica dopo il titolo di sezione `<h2>`.
- Presentare i tre servizi (Individuale, Familiare, Coppia) con card stilizzate, angoli arrotondati e immagini coordinate, anziché come un lungo blocco di testo continuo.

---

## 6. Privacy, Cookie e GDPR

- **Tracciamento Google Analytics:** Lo script `G-DLHYE5GV19` è attualmente caricato all'apertura della pagina senza verifica del consenso preventivo né anonimizzazione dell'indirizzo IP.
- **Informativa Privacy e Cookie:** Trattandosi di un sito professionale sanitario che raccoglie comunicazioni dirette di pazienti, è obbligatorio per legge (GDPR e linee guida del Garante per la protezione dei dati personali) fornire un link nel footer a una pagina o modale con l'**Informativa sul trattamento dei dati personali (Privacy Policy)** e sulla gestione dei cookie.

---

| Priorità | Ambito | Descrizione Intervento | Impatto | Stato |
| :---: | :--- | :--- | :---: | :---: |
| **1** | **UX / Conversioni** | Riordinare le sezioni portando *Come posso aiutarti* subito dopo *Chi sono* | 🔴 Alto | ✅ **Completato** |
| **2** | **Performance** | Convertire e comprimere le immagini in formato WebP (-85% peso) | 🔴 Alto | Da fare |
| **3** | **Accessibilità** | Correggere contrasti cromatici (`#e15379`, hover link) e inserire `lang="it"` | 🔴 Alto | 🟡 In corso (`lang="it"` ✅) |
| **4** | **SEO Locale** | Inserire Schema.org JSON-LD per `MedicalBusiness` / `Psychologist` con le 2 sedi | 🔴 Alto | ✅ **Completato** |
| **5** | **UI / Mobile** | Introdurre pulsante flottante WhatsApp e stilizzare i canali di contatto in card | 🟡 Medio | ✅ **Completato** |
| **6** | **Legale / GDPR** | Predisporre Privacy Policy e adeguare il tracciamento di Google Analytics | 🟡 Medio | Da fare |
| **7** | **SEO** | Abilitare `robots.txt`, tag `canonical` e gerarchia corretta dei titoli (`h3`) | 🟢 Basso | 🟡 In corso (`robots.txt` + `canonical` ✅) |
