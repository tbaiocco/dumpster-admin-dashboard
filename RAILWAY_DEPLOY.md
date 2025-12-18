# Admin Dashboard - Railway Deployment Guide

## Prerequisites

1. Railway account (https://railway.app)
2. Railway CLI installed (optional): `npm i -g @railway/cli`
3. Backend API already deployed and accessible

## Environment Variables

Set these in Railway dashboard or via CLI:

### Required
- `REACT_APP_API_URL` - Your backend API URL (e.g., `https://api.yourdomain.com`)

### Optional
- `PORT` - Port for the container (default: 80, Railway auto-assigns)

## Deployment Methods

### Method 1: Railway Dashboard (Recommended)

1. Go to https://railway.app/new
2. Select **"Deploy from GitHub repo"**
3. Connect your GitHub account and select the admin-dashboard repository
4. **Configure deployment:**
   - **Builder**: Dockerfile (should auto-detect `Dockerfile.prod`)
   - **Branch**: `main` (or your preferred branch)
5. Add environment variables:
   - `REACT_APP_API_URL=https://your-backend-api.railway.app`
6. Deploy!

Railway will automatically:
- Detect the Dockerfile.prod
- Build the Docker image with build args
- Deploy to a Railway domain (e.g., `your-app.railway.app`)
- Provide SSL certificate automatically

### Method 2: Railway CLI

```bash
# Login to Railway
railway login

# Link to project (or create new)
railway link

# Set environment variables
railway variables set REACT_APP_API_URL=https://your-backend-api.railway.app

# Deploy
railway up
```

### Method 3: GitHub Integration (CI/CD)

1. Connect repository to Railway project
2. Enable automatic deployments from `main` branch (or your preferred branch)
3. Every push will trigger automatic deployment

## Build Process

The Dockerfile.prod uses multi-stage build:

**Stage 1: Builder**
- Install dependencies
- Build React app with react-scripts
- Uses `REACT_APP_API_URL` build arg

**Stage 2: Production**
- Nginx 1.25 Alpine (lightweight)
- Serves static files from build/
- Custom nginx.conf with:
  - Gzip compression
  - Security headers
  - Cache headers for static assets
  - SPA routing support
  - Health check endpoint at `/health`

## Post-Deployment

### Verify Deployment

```bash
# Check health endpoint
curl https://your-app.railway.app/health
# Should return: OK

# Visit the app
open https://your-app.railway.app
```

### Custom Domain Setup

1. Go to Railway project settings
2. Add custom domain (e.g., `admin.yourdomain.com`)
3. Update DNS records as shown by Railway:
   - Add CNAME record pointing to Railway domain
4. Wait for SSL certificate provisioning (~5 minutes)
5. Update backend CORS to allow new domain

## Configuration Files

- `Dockerfile.prod` - Production build with Nginx
- `Dockerfile` - Development build (not used for Railway)
- `railway.json` - Railway deployment configuration
- `.railwayignore` - Exclude files from upload
- `nginx.conf` - Embedded in Dockerfile.prod (SPA routing, caching, security headers)

## Performance Optimization

Already configured:
- Gzip compression for text assets
- 1-year cache for static assets (js, css, images)
- Immutable cache headers
- SPA fallback routing

## Security

Already configured:
- Security headers (X-Frame-Options, X-Content-Type-Options, etc.)
- Health check endpoint
- Minimal Alpine-based image
- Non-root nginx process

## Common Issues

### App Shows "Unable to connect to API"

**Cause**: `REACT_APP_API_URL` environment variable not set or incorrect

**Solution**: 
1. Check service variables in Railway
2. Verify backend URL is correct and accessible
3. Ensure backend has admin dashboard URL in CORS whitelist

### Build Fails - "react-scripts: command not found"

**Cause**: Dependencies not installed correctly

**Solution**: 
1. Verify package.json has all dependencies
2. Check Railway build logs
3. Try rebuilding: `railway up --force`

### 404 on Routes (other than /)

**Cause**: SPA routing not working

**Solution**: nginx.conf already handles this with `try_files $uri $uri/ /index.html`
- Verify nginx.conf is correctly copied in Dockerfile.prod

## Cost Estimation

Railway Starter Plan:
- $5/month for 500 hours
- This dashboard should use ~730 hours/month if running 24/7
- Estimated cost: ~$7-8/month

Pro Plan: $20/month for unlimited usage

## Support

- Railway Docs: https://docs.railway.app
- Railway Discord: https://discord.gg/railway
- GitHub Issues: [Your repo]/issues
