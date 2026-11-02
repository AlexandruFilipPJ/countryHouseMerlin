# Country House by Merlin - Website

A modern, responsive static website for Country House by Merlin, built with HTML, CSS, and vanilla JavaScript. Fully multi-lingual (Romanian & English), mobile-optimized, with Dark Mode support and SEO features.

## File Structure

```
/
├── index.html                 # Redirects to /ro/ (default)
├── favicon.svg               # Website favicon
├── robots.txt                # Search engine crawler rules
├── sitemap.xml              # SEO sitemap
├── ro/
│   ├── index.html           # Main page (Romanian)
│   └── merlin-story.html    # Story page (Romanian)
├── en/
│   ├── index.html           # Main page (English)
│   └── merlin-story.html    # Story page (English)
└── README.md                # This file
```

## Features

✅ **Multi-Language Support** - Full RO & EN versions with language switcher  
✅ **Mobile-Responsive** - Works on phones, tablets, and desktops  
✅ **Dark Mode** - Auto-adapts to system theme preference  
✅ **Icons** - Font Awesome icons throughout the site  
✅ **SEO Optimized** - Meta tags, hreflang tags, sitemap.xml, robots.txt  
✅ **Google Analytics Ready** - Placeholder for GA4 integration  
✅ **Google Search Console Ready** - Verification meta tag  
✅ **Favicon** - Custom SVG favicon  
✅ **WhatsApp Integration** - Pre-filled messages for booking requests  
✅ **Sticky Navigation** - Fixed header with language switcher  
✅ **Accordion FAQs** - Click to expand/collapse  
✅ **Mobile Menu** - Hamburger menu on small screens  

## Setup & Configuration

### 1. Set Your Domain
Update all URLs in `sitemap.xml`:
```xml
<loc>https://countryhousebymerlin.com/ro/</loc>
<!-- Replace with your actual domain -->
```

### 2. Google Analytics Setup
In both `/ro/index.html` and `/en/index.html`, find:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_ID"></script>
<script>
  gtag('config', 'GA_ID');  <!-- Replace GA_ID with your property ID -->
</script>
```

Get your ID from: https://analytics.google.com

### 3. Google Search Console
In both `/ro/index.html` and `/en/index.html`, find:
```html
<meta name="google-site-verification" content="VERIFICATION_CODE">
<!-- Replace VERIFICATION_CODE with your code -->
```

Get your code from: https://search.google.com/search-console

### 4. WhatsApp Number
In both language versions (`/ro/index.html` and `/en/index.html`):
```javascript
const WHATSAPP_NUMBER = '+40XXX000000'; // Replace with your WhatsApp number
```

The number format: `+[country code][phone number]` (digits only)

### 5. Contact Information
Update in both language versions (search for "Contact" section):
- WhatsApp number
- Email address
- Location (already set to Robești, Buzău)

## Content Customization

### Images
Replace placeholder gray boxes in all pages:

**Main Page Images:**
- `.hero-image` - Hero section banner
- `.gallery-item` - 6 gallery photos (bedrooms, living, kitchen, terrace, etc)
- `.by-merlin-image` - Your portrait photo

**Story Page Images:**
- `.chapter-image` - 5 chapter images

To add images, use CSS background-image:
```html
<div class="hero-image" style="background-image: url('path/to/image.jpg'); background-size: cover;"></div>
```

Or replace `<div>` with `<img>`:
```html
<img src="path/to/image.jpg" alt="description" class="gallery-item">
```

### Text Content

**Romanian Version (/ro/)**
- Update all sections in `/ro/index.html`
- Update story chapters in `/ro/merlin-story.html`
- Add Instagram links (replace `href="#"` with actual URLs)
- Update FAQ answers with your policies

**English Version (/en/)**
- Update all sections in `/en/index.html`
- Update story chapters in `/en/merlin-story.html`
- Add Instagram links (replace `href="#"` with actual URLs)
- Update FAQ answers with your policies

### Colors & Styling
Edit the `:root` CSS block in both versions:
```css
:root {
  --bg: #faf8f6;           /* Background */
  --fg: #2a2520;           /* Text color */
  --accent: #b8860b;       /* Buttons & links */
  --muted: #8b7d75;        /* Secondary text */
  --border: #e8e3dd;       /* Dividers & borders */
  --card-bg: #ffffff;      /* Card background */
}
```

Dark mode colors are automatically applied from the media query.

### Fonts
Default fonts (editable in `:root`):
- **Display:** Playfair Display (Google Fonts) - headings
- **Body:** System fonts - paragraphs and body text

To change, edit `--font-display` and `--font-body` variables.

## Deployment

### Option 1: Standard Web Hosting
1. Upload all files to your hosting server
2. Ensure folder structure matches (ro/, en/ folders)
3. Set document root to the root directory containing robots.txt

### Option 2: Vercel / Netlify
1. Connect your GitHub repository
2. Build command: (leave blank - static site)
3. Publish directory: (root directory)
4. Deploy!

### Option 3: GitHub Pages
1. Create a `gh-pages` branch
2. Upload all files
3. Enable GitHub Pages in repo settings
4. Your site will be at `username.github.io/countryhousebymerlin`

## Testing Checklist

Before launch:

- [ ] Test on mobile (phone width ~400px)
- [ ] Test on tablet (tablet width ~768px)
- [ ] Test on desktop (wide screens)
- [ ] Test dark mode (Windows: Settings > Personalization > Colors)
- [ ] Test dark mode (Mac: System Preferences > General > Dark)
- [ ] Test all language switchers
- [ ] Test all WhatsApp buttons (replace +40XXX with real number first)
- [ ] Test smooth scrolling navigation
- [ ] Test FAQ accordion (click to expand)
- [ ] Test hamburger menu on mobile
- [ ] Verify all images load correctly
- [ ] Check all links work
- [ ] Test Google Analytics (check GA dashboard after 24h)
- [ ] Submit sitemap to Google Search Console
- [ ] Test on different browsers (Chrome, Firefox, Safari, Edge)

## SEO Tips

1. **Sitemap**: Automatically generated. Submit to Google Search Console.
2. **Robots.txt**: Configured to allow crawling. Update domain if needed.
3. **Meta Tags**: Already included for title, description, keywords, og:image
4. **hreflang**: Configured for language alternates (helps SEO for multi-language)
5. **Canonical Tags**: Each page has canonical URL (prevents duplicate content)
6. **Mobile-First**: Site is mobile-responsive (Google prefers this)

## Troubleshooting

### Images not showing
- Check image paths are correct
- Use absolute URLs if relative paths don't work: `https://yoursite.com/images/photo.jpg`
- Ensure images are in PNG, JPG, or WebP format

### WhatsApp button not working
- Verify phone number format: `+40XXXXXXXXX` (digits only)
- Test link manually: `https://wa.me/40XXXXXXXXX`

### Language switcher not working
- Check that `/ro/` and `/en/` folders exist with correct files
- Verify paths are correct in language switcher links

### Dark mode not working
- Tested on: Windows Settings > Personalization > Colors
- Tested on: Mac System Preferences > General > Dark
- Or manually test: Open DevTools > ⋯ > More tools > Rendering > Emulate CSS media feature prefers-color-scheme

### Google Analytics not tracking
- Wait 24-48 hours for first data to appear
- Check that GA_ID is correctly entered
- Verify Analytics property exists in Google Analytics dashboard

## Support & Updates

- Font Awesome Icons: https://fontawesome.com/
- Google Fonts: https://fonts.google.com/
- Meta Tag Generator: https://www.metatags.io/
- Mobile Responsive Test: https://www.responsivedesignchecker.com/

## License

All content and design © 2024 Country House by Merlin. All rights reserved.