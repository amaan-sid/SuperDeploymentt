## 📘 Deployment Docs

# Level 0

1. 📦 Vercel Deployment
✅ Steps Taken
Pushed project to GitHub.

Logged in to Vercel.

Clicked on "Add New Project" and selected the GitHub repo.

Set up default settings (React app is auto-detected).

Clicked Deploy.

🛠 Issues Faced
Slow initial build time.

Had to set build command to npm run build explicitly once.

🔁 CI/CD Pipeline
Vercel automatically redeploys the app when I push to the main branch.

No manual configuration needed for basic use.

2. 🌐 Netlify Deployment
✅ Steps Taken
Went to Netlify.

Clicked on "Import from Git" and connected GitHub repo.

Set build command: npm run build

Set publish directory: build/

Deployed the site.

🛠 Issues Faced
Environment variables had to be re-added in the Netlify dashboard.

Sometimes build would hang — fixed by clearing the cache and retrying.

🔁 CI/CD Pipeline
Netlify provides out-of-the-box CI/CD.

It automatically builds and deploys the site whenever changes are pushed to the repo.

3. ⚙️ Render Deployment
✅ Steps Taken
Visited Render.

Selected "Static Site" from the dashboard.

Connected GitHub repo and filled:

Build Command: npm run build

Publish Directory: build/

Clicked Create Static Site.

🛠 Issues Faced
Initial deploy failed due to wrong publish path (build/ was not recognized).

Had to manually set Node and NPM versions for compatibility.

🔁 CI/CD Pipeline
Render auto-builds and redeploys on push.

Option to trigger manual deploy is also available.

🧪 Conclusion
Deploying to Vercel, Netlify, and Render gave me insight into how different platforms handle React apps. Vercel felt the smoothest for quick deployments, Netlify gave the most flexibility, and Render was useful for full-stack setups.