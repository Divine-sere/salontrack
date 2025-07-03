# Deployment Guide for SalonTrack

## Deploying to Vercel

### Prerequisites
1. GitHub account with your SalonTrack repository
2. Vercel account (sign up at [vercel.com](https://vercel.com))
3. PostgreSQL database (recommended: [Neon](https://neon.tech) or [PlanetScale](https://planetscale.com))

### Step 1: Upload to GitHub
First, ensure your code is on GitHub:
```bash
git init
git add .
git commit -m "Initial commit: SalonTrack loyalty system"
git remote add origin https://github.com/yourusername/salontrack.git
git push -u origin main
```

### Step 2: Deploy on Vercel
1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click "New Project"
3. Import your SalonTrack repository
4. Vercel will automatically detect the configuration from `vercel.json`
5. Click "Deploy"

### Step 3: Environment Variables
In your Vercel project dashboard:
1. Go to "Settings" > "Environment Variables"
2. Add these variables:
   - `DATABASE_URL`: Your PostgreSQL connection string
   - `SESSION_SECRET`: A secure random string for sessions
   - `NODE_ENV`: Set to "production"

### Step 4: Database Setup
1. Create a PostgreSQL database on Neon or PlanetScale
2. Copy the connection string to your `DATABASE_URL` environment variable
3. Run database migrations:
   ```bash
   npm run db:push
   ```

### Step 5: Domain Configuration
- Your app will be available at `https://your-project-name.vercel.app`
- To use a custom domain, go to "Settings" > "Domains" in Vercel

## Alternative: Deploy to Railway

### Quick Railway Deployment
1. Fork the repository on GitHub
2. Go to [railway.app](https://railway.app)
3. Click "Start a New Project" > "Deploy from GitHub repo"
4. Select your SalonTrack repository
5. Add environment variables in Railway dashboard
6. Deploy automatically handles the build process

## Environment Variables Reference

```env
# Required
DATABASE_URL=postgresql://user:password@host:port/database
SESSION_SECRET=your-secure-session-secret

# Optional
NODE_ENV=production
PORT=5000
```

## Database Providers

### Neon (Recommended)
- Free tier available
- Serverless PostgreSQL
- Easy connection string setup

### PlanetScale
- MySQL-compatible
- Free tier available
- Built-in branching

### Supabase
- PostgreSQL with additional features
- Free tier available
- Built-in authentication

## Build Process
The deployment uses these commands:
1. `npm install` - Install dependencies
2. `npm run build` - Build frontend and backend
3. Deploy to serverless functions

## Troubleshooting

### Common Issues
1. **Database connection**: Ensure your DATABASE_URL is correct
2. **Session secret**: Make sure SESSION_SECRET is set
3. **Build errors**: Check that all dependencies are listed in package.json

### Logs
- Check deployment logs in Vercel dashboard
- Use `vercel logs` command for real-time debugging

## Production Checklist
- [ ] Database connected and migrated
- [ ] Environment variables set
- [ ] Custom domain configured (optional)
- [ ] SSL certificate active
- [ ] Database backups configured
- [ ] Monitoring setup