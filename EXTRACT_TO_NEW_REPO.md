# Extract Admin-Dashboard to New Repository

## Method 1: Simple Copy (Recommended for Clean Start)

```bash
# Create new repository on GitHub (e.g., dumpster-admin-dashboard)

# Clone it locally
git clone https://github.com/tbaiocco/dumpster-admin-dashboard.git
cd dumpster-admin-dashboard

# Copy all admin-dashboard files (from outside the new repo)
cp -r /home/baiocte/personal/dumpster/admin-dashboard/* .
cp /home/baiocte/personal/dumpster/admin-dashboard/.* . 2>/dev/null || true

# Initialize git if needed
git add .
git commit -m "feat: initial admin-dashboard setup from dumpster monorepo

- React 19.2.0 + TypeScript 5.9.3
- Vite build system
- Tailwind CSS
- shadcn/ui components
- Docker multi-stage build ready"

git push origin main
```

## Method 2: Preserve Git History (Advanced)

If you want to keep the commit history for admin-dashboard files:

```bash
# Clone the original repo
git clone https://github.com/tbaiocco/dumpster-spec.git dumpster-admin-dashboard
cd dumpster-admin-dashboard

# Filter only admin-dashboard directory history
git filter-branch --subdirectory-filter admin-dashboard -- --all

# Or use git-filter-repo (faster, cleaner)
# pip install git-filter-repo
# git filter-repo --path admin-dashboard/ --path-rename admin-dashboard/:

# Add new remote
git remote remove origin
git remote add origin https://github.com/tbaiocco/dumpster-admin-dashboard.git

# Push to new repo
git push -u origin main
```

## After Extraction

1. **Update README.md** - Remove monorepo references
2. **Deploy to Railway**:
   - Connect new GitHub repo
   - Set environment variables (see below)
   - Deploy!
3. **Custom Domain** (optional):
   - Add in Railway settings
   - Configure DNS records
   - Example: `admin.yourdomain.com`

## Environment Variables Needed

For Railway deployment:
```
VITE_API_URL=https://your-backend.railway.app
```

For local development (`.env.local`):
```
VITE_API_URL=http://localhost:3000
```

## Next Steps After Repository Creation

1. Update workspace: Add to `dumpster.code-workspace`
2. Create Railway deployment configuration (railway.json, RAILWAY_DEPLOY.md)
3. Set up CI/CD with GitHub integration
4. Configure custom domain

## Estimated Timeline

- Repository setup: 5 minutes
- Railway connection: 5 minutes
- First deployment: 5-10 minutes
- Custom domain (optional): 30-60 minutes

Total: **15-30 minutes** to be fully deployed
