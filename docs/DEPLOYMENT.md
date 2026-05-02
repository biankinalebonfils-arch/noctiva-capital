# Deployment Guide

## GitHub Pages Deployment

This document provides step-by-step instructions for deploying NOCTIVA Capital to GitHub Pages.

### Prerequisites

- ✅ Repository created on GitHub
- ✅ Main branch contains `index.html`
- ✅ GitHub account with repository access

### Automatic Deployment Setup

#### Step 1: Enable GitHub Pages

1. Navigate to your repository on GitHub
2. Go to **Settings** (top navigation)
3. Select **Pages** (left sidebar under "Code and automation")

#### Step 2: Configure Source

1. Under **Build and deployment** → **Source**
2. Select: **Deploy from a branch**
3. Choose Branch: **main**
4. Choose Folder: **/ (root)**
5. Click **Save**

#### Step 3: Wait for Deployment

GitHub will automatically:
- Detect the new Pages configuration
- Build your site (usually instant for static HTML)
- Deploy to GitHub Pages
- Display the site URL in Settings > Pages

This typically takes **30 seconds to 2 minutes**.

#### Step 4: Access Your Site

Your site is now live at:
```
https://biankinalebonfils-arch.github.io/noctiva-capital/
```

---

## Custom Domain Setup (Optional)

### Using a Custom Domain

If you own a domain (e.g., `noctiva-capital.com`), you can point it to GitHub Pages.

#### Step 1: Create CNAME File

1. Create a file named `CNAME` in your repository root
2. Add a single line with your domain:
   ```
   noctiva-capital.com
   ```
3. Commit and push to main

#### Step 2: Configure DNS

You must configure your domain's DNS to point to GitHub's servers.

**Option A: A Records (Recommended)**

Create 4 A records pointing to GitHub's IP addresses:
```
A  @ → 185.199.108.153
A  @ → 185.199.109.153
A  @ → 185.199.110.153
A  @ → 185.199.111.153
```

Replace `@` with your domain registrar's notation (often just leave blank or use `@`).

**Option B: CNAME Record**

Create a CNAME record:
```
CNAME  www → biankinalebonfils-arch.github.io.
```

#### Step 3: Verify in GitHub

1. Go to **Settings > Pages**
2. Under **Custom domain**, enter your domain
3. GitHub will verify the DNS configuration
4. Check the "Enforce HTTPS" checkbox once it's available

#### Step 4: Wait for SSL Certificate

GitHub automatically provisions an SSL certificate (takes a few minutes to 24 hours).

You'll see in Settings > Pages:
- ✅ Domain configured
- ✅ HTTPS enabled (green checkmark)

---

## Troubleshooting

### Site Not Showing After Enabling Pages

**Problem:** Settings show Pages is enabled, but the site isn't live.

**Solutions:**
1. Wait 2-3 minutes (deployment can take time)
2. Hard refresh your browser (Ctrl+Shift+R / Cmd+Shift+R)
3. Check that **Source** is set to "Deploy from a branch" with "main" selected
4. Verify `index.html` exists in the root directory of main branch

### 404 Error on Custom Domain

**Problem:** Accessing your custom domain returns 404.

**Solutions:**
1. Verify DNS records are correctly configured
2. Check that `CNAME` file exists in repository root
3. In Settings > Pages, ensure custom domain is entered correctly
4. Wait for DNS propagation (can take up to 48 hours)
5. Use DNS checker tool: https://mxtoolbox.com/

### HTTPS Not Working

**Problem:** Site works on HTTP but not HTTPS, or certificate isn't provisioning.

**Solutions:**
1. Wait 24 hours for certificate to be issued
2. Remove and re-add the custom domain:
   - Settings > Pages > Custom domain → Remove
   - Add it again
   - Wait for verification
3. If HTTPS checkbox doesn't appear, DNS setup may need correction

### Changes Not Appearing After Push

**Problem:** You pushed changes to main but the site doesn't update.

**Solutions:**
1. Wait 1-2 minutes for deployment
2. Hard refresh browser (Ctrl+Shift+R)
3. Check GitHub Actions:
   - Go to **Actions** tab
   - Look for "Deploy to GitHub Pages" workflow
   - Verify it shows ✅ passing
4. If workflow failed, click it to see error logs

### Custom Domain Points to Wrong Site

**Problem:** Your custom domain is showing content from a different repository.

**Solutions:**
1. Verify no other repository on your account is using the same custom domain
2. Remove the domain from that other repository's Pages settings
3. Re-configure on your intended repository
4. Wait 5 minutes and test

---

## Workflow Status & Monitoring

### Automatic Deployments

Every push to `main` triggers automatic deployment via the GitHub Actions workflow.

#### View Deployment Status

1. Go to **Actions** tab
2. Look for "Deploy to GitHub Pages" workflow
3. Click the most recent run
4. View:
   - ✅ Build job status
   - ✅ Deploy job status
   - 📊 Job logs and details

#### Manual Redeploy

If you need to force a redeploy without making changes:

1. Go to **Actions** > **Deploy to GitHub Pages**
2. Click **Run workflow**
3. Select branch: **main**
4. Click **Run workflow**

---

## Performance & Optimization

### Current Site Performance

The NOCTIVA Capital site is optimized for speed:

- **Single HTML file**: No external page loads
- **Embedded CSS**: Styles included in HTML
- **Inline JavaScript**: No external JS files
- **Google Fonts**: Only 3 font families loaded
- **No external APIs**: Pure static content

### Expected Performance

- 📊 **Lighthouse Score**: 90+
- ⚡ **First Contentful Paint**: < 1s
- 🎬 **Time to Interactive**: < 2s
- 📦 **Page Size**: ~50 KB

### Caching

GitHub Pages automatically caches your site. If you need to clear cache:

1. Go to **Settings > Pages**
2. Toggle "Enforce HTTPS" off, then back on (forces cache refresh)
3. OR wait 24 hours for automatic cache expiration

---

## Security Considerations

### What's Secure

✅ GitHub Pages provides:
- Automatic HTTPS for github.io domains and custom domains
- DDoS protection
- Reliable uptime (99.9%)
- No configuration needed

✅ Your site has:
- No backend services
- No database
- No authentication
- No sensitive data
- Pure static HTML/CSS/JS

### What to Be Aware Of

⚠️ Remember:
- Any content in your repository is public (unless you make the repo private)
- Do NOT commit API keys, credentials, or secrets
- Do NOT store user data (the site has no backend)
- All code and content is visible in the repository

### Best Practices

1. **Keep repo public** for GitHub Pages to work
2. **Use .gitignore** to exclude sensitive files
3. **Use environment variables** for any configuration (though this site doesn't need them)
4. **Review commits** before pushing to main (all changes trigger deployment)

---

## DNS Propagation Testing

### Check Your DNS Configuration

Use these tools to verify DNS is set up correctly:

1. **MX Toolbox DNS Checker**
   - https://mxtoolbox.com/
   - Enter your domain
   - Check A records or CNAME record

2. **Google DNS Checker**
   - https://www.google.com/search?q=dns+checker
   - Search "DNS propagation checker"

3. **Command Line (Mac/Linux)**
   ```bash
   # Check A records
   dig your-domain.com A
   
   # Check CNAME records
   dig www.your-domain.com CNAME
   
   # Get GitHub's IPs (for verification)
   dig biankinalebonfils-arch.github.io A
   ```

4. **Windows Command Prompt**
   ```cmd
   nslookup your-domain.com
   ```

---

## Rollback & Version Control

### If Something Goes Wrong

Since this uses GitHub Pages with automatic deployment:

1. **Recent Issue?** Check recent commits to main
2. **Revert a Commit:**
   ```bash
   git revert <commit-sha>
   git push origin main
   ```
3. **Deploy a Previous Version:**
   ```bash
   git reset --hard <commit-sha>
   git push -f origin main
   ```

**Note**: Force push (`-f`) overwrites history. Use with caution!

---

## Next Steps

1. ✅ Enable GitHub Pages (see top of this guide)
2. ✅ Test your site at the GitHub Pages URL
3. 🔗 (Optional) Set up custom domain
4. 📊 Monitor deployments via Actions tab
5. 🎨 Make updates and push to main

---

## Support Resources

- **GitHub Pages Docs**: https://docs.github.com/en/pages
- **GitHub Actions Docs**: https://docs.github.com/en/actions
- **GitHub Pages Troubleshooting**: https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-common-issues-with-github-pages
- **Custom Domain Setup**: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

---

**Last Updated**: 2026-05-02
**Status**: Ready for deployment ✅