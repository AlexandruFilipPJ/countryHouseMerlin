# Country House by Merlin - Deployment Guide

Complete guide to deploy your website to production.

## Pre-Deployment Checklist

Before uploading to production, complete these steps:

### 1. Content Updates ✓

- [ ] Update WhatsApp number in `/ro/index.html` and `/en/index.html`
- [ ] Update email address in both versions
- [ ] Add actual images (replace gray placeholders)
- [ ] Update all text content (keep both RO & EN in sync)
- [ ] Add Instagram post links in story pages
- [ ] Update FAQ answers with your policies
- [ ] Update "What's Coming Up" section with real offers/events

### 2. SEO Configuration ✓

- [ ] Update domain name in `sitemap.xml` (replace countryhousebymerlin.com)
- [ ] Update domain in `robots.txt` (replace countryhousebymerlin.com)
- [ ] Get Google Analytics ID and update both index files
- [ ] Get Google Search Console verification code and update both index files
- [ ] Test favicon displays correctly (should be a house icon)

### 3. Testing ✓

- [ ] Test on mobile (< 500px width)
- [ ] Test on tablet (500-900px width)
- [ ] Test on desktop (> 900px width)
- [ ] Test dark mode on all devices
- [ ] Test language switcher (both directions)
- [ ] Test all buttons and links
- [ ] Test WhatsApp button opens correctly
- [ ] Test smooth scrolling works
- [ ] Test FAQ accordion expands/collapses
- [ ] Test hamburger menu on mobile
- [ ] Test on multiple browsers (Chrome, Firefox, Safari, Edge)

---

## Deployment Options

### Option 1: Shared Hosting (cPanel / Plesk)

**Steps:**

1. **Connect via FTP/SFTP**
   - Open FileZilla or your FTP client
   - Connect with provided credentials
   - Navigate to public_html (or www folder)

2. **Upload Files**
   ```
   Upload these files to the root:
   - index.html
   - favicon.svg
   - robots.txt
   - sitemap.xml
   - README.md
   - DEPLOYMENT.md
   
   Upload these folders:
   - /ro/ (with index.html and merlin-story.html)
   - /en/ (with index.html and merlin-story.html)
   ```

3. **Verify Upload**
   - Visit `yoursite.com/` - should redirect based on language
   - Visit `yoursite.com/ro/` - should show Romanian version
   - Visit `yoursite.com/en/` - should show English version

4. **Configure Email (Optional)**
   - In cPanel, create email accounts for notifications
   - Update email in contact section

**Test After Upload:**
- [ ] Check home page loads
- [ ] Check language switching works
- [ ] Check images load
- [ ] Check WhatsApp button works
- [ ] Check all links work

---

### Option 2: Vercel (Recommended for Static Sites)

**Steps:**

1. **Install Vercel CLI** (or use web interface)
   ```bash
   npm install -g vercel
   ```

2. **Deploy Project**
   ```bash
   cd /path/to/countryhousebymerlin
   vercel
   ```

3. **Follow Prompts**
   - Link to your GitHub account
   - Select project directory
   - Let Vercel autodetect settings

4. **Custom Domain**
   - In Vercel dashboard: Settings > Domains
   - Add your domain (countryhousebymerlin.com)
   - Update domain's DNS records to point to Vercel

**Advantages:**
- ✅ Automatic HTTPS
- ✅ CDN distribution (fast worldwide)
- ✅ Automatic deployments on git push
- ✅ Free tier available

---

### Option 3: Netlify

**Steps:**

1. **Connect GitHub/GitLab**
   - Sign up at netlify.com
   - Create new site from your repo
   - Connect your git repository

2. **Configure Build** (usually auto-detected)
   - Build command: (leave empty)
   - Publish directory: (leave empty or .)
   - Deploy!

3. **Add Custom Domain**
   - Site settings > Domain management
   - Add your domain
   - Update DNS records

**Netlify.toml** (optional - for better configuration):
```toml
[build]
  command = ""
  publish = "."

[[redirects]]
  from = "/"
  to = "/ro/"
  status = 302
  force = false
```

---

### Option 4: GitHub Pages

**Steps:**

1. **Create Repository**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Country House by Merlin website"
   git branch -M main
   git remote add origin https://github.com/yourusername/countryhousebymerlin.git
   git push -u origin main
   ```

2. **Enable GitHub Pages**
   - Go to repository Settings
   - Scroll to "GitHub Pages"
   - Select "Deploy from a branch"
   - Choose `main` branch, root folder
   - Save

3. **Custom Domain**
   - Add CNAME file to root with your domain
   - Update domain's DNS records
   - GitHub automatically configures HTTPS

**URL will be:**
- `https://yourusername.github.io/countryhousebymerlin` (default)
- `https://countryhousebymerlin.com` (custom domain)

---

### Option 5: Self-Hosted Server (Linux)

**Steps:**

1. **SSH into Server**
   ```bash
   ssh user@yourserver.com
   ```

2. **Create Web Directory**
   ```bash
   mkdir -p /var/www/countryhousebymerlin
   cd /var/www/countryhousebymerlin
   ```

3. **Upload Files** (via SCP or Git)
   ```bash
   # Via SCP from local:
   scp -r ./* user@yourserver.com:/var/www/countryhousebymerlin/
   
   # Or via Git:
   git clone your-repo-url .
   ```

4. **Configure Web Server (Nginx)**
   ```nginx
   server {
       listen 80;
       listen 443 ssl http2;
       server_name countryhousebymerlin.com www.countryhousebymerlin.com;
       
       root /var/www/countryhousebymerlin;
       index index.html;
       
       # Redirect to HTTPS
       if ($scheme != "https") {
           return 301 https://$server_name$request_uri;
       }
       
       # SSL certificates (use Let's Encrypt)
       ssl_certificate /etc/letsencrypt/live/countryhousebymerlin.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/countryhousebymerlin.com/privkey.pem;
       
       location / {
           try_files $uri $uri/ /index.html;
       }
       
       # Cache static assets
       location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
           expires 1y;
           add_header Cache-Control "public, immutable";
       }
       
       # Gzip compression
       gzip on;
       gzip_types text/plain text/css text/javascript application/json application/javascript;
   }
   ```

5. **Enable HTTPS** (Let's Encrypt)
   ```bash
   sudo apt install certbot python3-certbot-nginx
   sudo certbot certonly --nginx -d countryhousebymerlin.com -d www.countryhousebymerlin.com
   ```

6. **Restart Web Server**
   ```bash
   sudo systemctl restart nginx
   ```

---

## Post-Deployment

### 1. Google Search Console
1. Go to https://search.google.com/search-console
2. Add your property (your domain)
3. Verify ownership using meta tag in index.html
4. Submit sitemap: `sitemap.xml`
5. Monitor: Coverage, Core Web Vitals, Mobile usability

### 2. Google Analytics
1. Go to https://analytics.google.com
2. Create new property for your site
3. Get your Measurement ID (GA_ID)
4. Should be updating in ~24 hours
5. Check: Audience, Acquisition, Behavior reports

### 3. Domain & DNS
1. Point domain to your hosting via:
   - A record (for standard hosting)
   - CNAME record (for Vercel/Netlify)
   - Nameservers (for GitHub Pages)

2. Verify DNS propagation:
   ```bash
   # On Mac/Linux:
   dig countryhousebymerlin.com
   nslookup countryhousebymerlin.com
   ```

### 4. SSL Certificate
- Most platforms (Vercel, Netlify, GitHub Pages) provide free HTTPS
- If self-hosted: Use Let's Encrypt (free)
- Always use HTTPS (not HTTP)

### 5. Monitor Performance
- **Google PageSpeed Insights**: https://pagespeed.web.dev
- **GTmetrix**: https://gtmetrix.com
- **WebPageTest**: https://www.webpagetest.org

Target metrics:
- ✅ Page Load Time: < 2 seconds
- ✅ Largest Contentful Paint (LCP): < 2.5s
- ✅ Cumulative Layout Shift (CLS): < 0.1
- ✅ First Input Delay (FID): < 100ms

---

## Maintenance

### Regular Tasks

**Monthly:**
- Check Google Analytics for traffic patterns
- Monitor Google Search Console for errors
- Review broken links
- Check performance metrics

**Quarterly:**
- Update content (new events, offers)
- Check for outdated information
- Review and update Instagram links
- Backup your website

**Yearly:**
- Review and update copy
- Refresh images if needed
- Check for security updates
- Plan new features

### Update Procedures

**To Update Content:**
1. Edit files locally
2. Test changes locally
3. Upload to server (via FTP, Git, or direct)
4. Clear cache if needed
5. Verify changes live

**To Update Images:**
1. Prepare optimized images (< 2MB each)
2. Add to local folder
3. Update HTML to reference new images
4. Upload to server
5. Verify images display

---

## Troubleshooting

### 404 Errors on /ro/ and /en/ pages
- **Issue:** Folders not uploaded correctly
- **Fix:** Ensure `/ro/` and `/en/` folders with index.html exist in root

### Language switcher not working
- **Issue:** Relative paths incorrect
- **Fix:** Use absolute paths `/ro/` instead of `ro/`

### Images not showing
- **Issue:** Image paths incorrect or images not uploaded
- **Fix:** Use absolute URLs or check image locations

### WhatsApp doesn't work on mobile
- **Issue:** WhatsApp not installed or number format wrong
- **Fix:** Verify number format (+40XXXXXXXXX) and test manually

### Poor Performance
- **Issue:** Large unoptimized images
- **Fix:** Compress images before uploading
- **Tools:** TinyPNG, ImageOptim, Squoosh

### Google Analytics not tracking
- **Issue:** Wrong GA_ID or incorrect setup
- **Fix:** 
  1. Verify GA_ID is correct
  2. Wait 24-48 hours for data
  3. Check Analytics dashboard

---

## Backup Strategy

**Backup Your Files:**
```bash
# Create backup folder
mkdir ~/countryhousebymerlin-backups

# Backup entire site
zip -r ~/countryhousebymerlin-backups/website-$(date +%Y%m%d).zip .

# Or use your hosting provider's backup tool
```

**Recommended Schedule:**
- After every content update
- Before major changes
- Monthly automatic backups

---

## SSL Certificate Renewal (Let's Encrypt)

If self-hosted with Let's Encrypt:
```bash
# Certificates auto-renew, but you can manually renew:
sudo certbot renew --nginx

# Check renewal status:
sudo certbot certificates
```

---

## Questions?

Refer to:
- README.md for content setup
- Hosting provider's documentation
- SEO guides in troubleshooting section
- Google's Web Fundamentals: https://developers.google.com/web/fundamentals
