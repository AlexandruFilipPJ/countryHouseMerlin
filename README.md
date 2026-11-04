# Country House by Merlin – site (template)

Site static, one page, construit cu HTML + Tailwind (CDN) + JavaScript simplu. Nu are nevoie de build: se deschide `index.html` direct în browser sau se urcă pe orice hosting static (Netlify, Vercel, GitHub Pages, cPanel).

## Structură

```
/
├── index.html           # Pagina principală (one page)
├── merlin-story.html    # The Real Life of Merlin (pagina dedicată, deschisă din By Merlin)
├── animation.html       # Experiența full-screen „Oraș → Natură” (deschisă din index)
├── assets/img/          # Imagini (curtea și zonele exterioare, decupate din moodboard)
├── favicon.svg
├── sitemap.xml, robots.txt
├── ro/, en/             # Redirecționări vechi către pagina principală
└── index2.html          # Versiune veche de lucru (nu e legată din site)
```

## Secțiunile paginii principale (conform brief-ului)

| Meniu | Ancoră | Conținut |
|---|---|---|
| (hero) | – | Welcome to the house · butoanele *Explore the house* și *Check availability* (WhatsApp) |
| The House | `#the-house` | Galerie cu filtre, curtea (bar, dining, lounge, jacuzzi, saună, vatra de foc), dotări, paleta casei, condiții de închiriere |
| Your Weekend | `#your-weekend` | Animația oraș → natură, cele 3 experiențe (fiecare cu WhatsApp precompletat), împrejurimi și distanțe |
| What’s On | `#whats-on` | Maximum 3 oferte: foto, date, descriere, „Include”, *Ask about this* |
| By Merlin | `merlin-story.html` | Teaser pe pagina principală + pagina dedicată, cu capitole și linkuri Instagram |
| Contact | `#faq-contact` | Întrebări frecvente, contact, condiții de rezervare, hartă |

Pe telefon, butonul **Check availability** stă fixat în partea de jos a ecranului.

## Ce trebuie înlocuit înainte de publicare

1. **Numărul de WhatsApp**: constanta `WHATSAPP_NUMBER` din `<script>`, în `index.html` și în `merlin-story.html`. Se aplică automat tuturor butoanelor. Numărul afișat în cardul de contact se schimbă manual.
2. **Email și Instagram**: în cardul de contact din `index.html`, plus linkurile `https://instagram.com` din capitolele `merlin-story.html`.
3. **Fotografii**: galeria, ofertele, portretul și capitolele folosesc acum imagini Unsplash de test. Pune fotografiile în `assets/img/` și schimbă `src` (iar în galerie și argumentul din `openLightbox(...)`).
4. **Ofertele (What’s On)**: fiecare card e un bloc HTML de sine stătător. Copiază-l sau editează-l (maximum 3).
5. **Întrebări frecvente și condiții de rezervare**: textele sunt orientative și trebuie confirmate.
6. **Distanțele din împrejurimi** trebuie verificate.
7. **Domeniul** din `sitemap.xml` și `robots.txt`.

## Paleta (din moodboard)

| Nume | Hex | Token Tailwind |
|---|---|---|
| Crem Cald | `#F5EDE1` | `merlin-oat` |
| Vișiniu | `#7A1F2E` | `merlin-clay` |
| Antracit | `#2F3237` | `merlin-pine` / `merlin-darkForest` |
| Stejar Natur | `#D6B07C` | `merlin-gold` |
| Baby Blue | `#C7DBEE` | `merlin-sky` |
| Piatră Naturală | `#E6D9C6` | `merlin-stone` |
| Grej | `#8C857A` | `merlin-greige` |

Tokenurile sunt definite în `tailwind.config`, în `<head>`, separat în fiecare pagină.

Fonturi: **Cormorant Garamond** (titluri) și **Plus Jakarta Sans** (text).

## Notă pentru producție

Tailwind se încarcă de pe CDN (`cdn.tailwindcss.com`). Pentru prezentare e suficient. Pentru site-ul final se recomandă compilarea CSS-ului cu Tailwind CLI, pentru viteză.
