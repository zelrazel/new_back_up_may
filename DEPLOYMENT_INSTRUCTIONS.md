# Deployment Instructions

This project is set up for deployment with:
- Frontend: Vercel
- Backend: Render

## Step 1: Deploy Backend to Render

1. Create a new Render account if you don't have one: https://render.com/
2. From the Render dashboard, select "New Web Service"
3. Connect your GitHub/GitLab repository or use the manual deploy option
4. Configure your service with these settings:
   - **Name**: `your-backend-name` (choose a name)
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Environment Variables**: Add all variables from your `.env` file:
     - `MONGO_URI` - Your MongoDB connection string
     - `PORT` - Set to `5000` or let Render assign a port (use `process.env.PORT || 5000` in code)
     - `FRONTEND_URL` - Your Vercel frontend URL (add after Vercel deployment)
     - `JWT_SECRET` - Your secure JWT secret
     - `CLOUDINARY_CLOUD_NAME` - Your Cloudinary name
     - `CLOUDINARY_API_KEY` - Your Cloudinary API key
     - `CLOUDINARY_API_SECRET` - Your Cloudinary secret

5. Click "Create Web Service"
6. Wait for the deployment to complete
7. Note your backend URL (e.g., `https://your-backend-name.onrender.com`)

## Step 2: Update Frontend Configuration

1. In your frontend code, update the `.env` file:
   ```
   REACT_APP_BACKEND_URL=https://your-backend-name.onrender.com/
   ```
   Replace with your actual Render backend URL

## Step 3: Deploy Frontend to Vercel

1. Create a Vercel account if you don't have one: https://vercel.com/
2. Install Vercel CLI globally: `npm i -g vercel`
3. Login to Vercel: `vercel login`
4. Navigate to your frontend directory: `cd frontend`
5. Run: `vercel` to deploy
   - Follow the prompts to set up your project
   - When asked about build settings, use default settings for a React app
6. After deployment, note your frontend URL (e.g., `https://your-frontend-app.vercel.app`)

## Step 4: Update Backend Configuration

1. Go back to your Render dashboard
2. Find your backend service and go to Environment
3. Update the `FRONTEND_URL` environment variable with your Vercel URL: 
   ```
   FRONTEND_URL=https://your-frontend-app.vercel.app
   ```
4. Save changes and trigger a new deployment

## File Storage Considerations

For uploads and file storage, consider:
1. Using Cloudinary for file uploads (already configured in your app)
2. Or implement AWS S3 for more robust file storage

## Troubleshooting

- **CORS Issues**: Ensure the FRONTEND_URL in your backend matches exactly your Vercel URL
- **Connection Issues**: Check that REACT_APP_BACKEND_URL in your frontend includes the trailing slash
- **Database Connection**: Verify your MongoDB connection string is correct and the IP is whitelisted

## Monitoring

- Use Render's built-in logs to monitor your backend
- For production apps, consider adding a monitoring solution like Sentry 