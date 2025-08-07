# Vercel Deployment Guide

This guide will help you deploy your Comment Management API to Vercel.

## Prerequisites

1. **Vercel Account**: Sign up at [vercel.com](https://vercel.com)
2. **Vercel CLI**: Install globally with `npm i -g vercel`
3. **Database**: Set up a PostgreSQL database (recommended: Prisma Accelerate)

## Environment Variables

Before deploying, you need to set up your environment variables in Vercel:

### Required Environment Variables

```env
DATABASE_URL="prisma+postgres://accelerate.prisma-data.net/?api_key=YOUR_API_KEY"
JWT_SECRET="your-super-secret-jwt-key-change-this-in-production"
EXPIRESIN="24h"
NODE_ENV="production"
```

### Optional Environment Variables

```env
CORS_ORIGIN="https://your-frontend-domain.com"
PORT=3000
```

## Deployment Steps

### 1. Local Setup

```bash
# Install dependencies
npm install

# Build the project
npm run build

# Test locally
npm run dev:local
```

### 2. Deploy to Vercel

#### Option A: Using Vercel CLI

```bash
# Login to Vercel
vercel login

# Deploy
vercel

# Follow the prompts:
# - Link to existing project or create new
# - Set environment variables
# - Deploy
```

#### Option B: Using Vercel Dashboard

1. Push your code to GitHub/GitLab/Bitbucket
2. Go to [vercel.com/dashboard](https://vercel.com/dashboard)
3. Click "New Project"
4. Import your repository
5. Configure environment variables
6. Deploy

### 3. Set Environment Variables

In your Vercel dashboard:

1. Go to your project settings
2. Navigate to "Environment Variables"
3. Add the required variables listed above

### 4. Database Setup

#### Using Prisma Accelerate (Recommended)

1. Go to [cloud.prisma.io](https://cloud.prisma.io)
2. Create a new project
3. Get your connection string
4. Add it to Vercel environment variables

#### Using Other PostgreSQL Providers

- **Neon**: [neon.tech](https://neon.tech)
- **Supabase**: [supabase.com](https://supabase.com)
- **Railway**: [railway.app](https://railway.app)

## Post-Deployment

### 1. Test Your API

Your API will be available at:

```
https://your-project-name.vercel.app
```

### 2. Health Check

Test the health endpoint:

```bash
curl https://your-project-name.vercel.app/api/health
```

### 3. API Documentation

Visit the root endpoint for API documentation:

```
https://your-project-name.vercel.app/
```

## Troubleshooting

### Common Issues

1. **Build Failures**

   - Check that all dependencies are in `package.json`
   - Ensure `vercel-build` script exists
   - Verify Prisma client generation

2. **Database Connection Issues**

   - Verify `DATABASE_URL` is correct
   - Check if database is accessible from Vercel
   - Ensure Prisma schema is pushed

3. **Environment Variables**
   - Double-check all required variables are set
   - Ensure no typos in variable names
   - Verify JWT_SECRET is strong enough

### Debugging

1. **Check Vercel Logs**

   ```bash
   vercel logs
   ```

2. **Local Testing**

   ```bash
   npm run dev
   ```

3. **Database Connection**
   ```bash
   npx prisma db push
   ```

## Performance Optimization

### For Production

1. **Enable Caching**

   - Add appropriate cache headers
   - Use Redis for session storage (if needed)

2. **Database Optimization**

   - Add database indexes
   - Use connection pooling
   - Monitor query performance

3. **Security**
   - Use strong JWT secrets
   - Enable CORS properly
   - Validate all inputs

## Monitoring

1. **Vercel Analytics**: Monitor API usage
2. **Error Tracking**: Set up error monitoring
3. **Database Monitoring**: Monitor database performance

## Updates

To update your deployment:

```bash
# Make changes to your code
git add .
git commit -m "Update API"
git push

# Vercel will automatically redeploy
```

Or manually:

```bash
vercel --prod
```

## Support

- **Vercel Documentation**: [vercel.com/docs](https://vercel.com/docs)
- **Prisma Documentation**: [prisma.io/docs](https://prisma.io/docs)
- **Project Issues**: Check the GitHub repository
