# 📘 Deployment Docs

## Level 0 & Level 1

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

## Level 3

🧩 Backend Deployment Documentation
This section explains how I deployed my backend (using SQLite3) on Render, EC2, and [Platform 3].

1. 🚀 Render Backend Deployment
✅ Steps Taken
Created a new Web Service on Render.

Connected to my GitHub repo.

Set:

Start command: node index.js (or your main file)

Environment: Node

Added environment variables like PORT and DB paths if needed.

Deployed the app.

⚠️ Issues Faced
SQLite3 had file path issues — needed to use absolute paths or ensure the DB file was in the repo.

Render's ephemeral filesystem means no persistent writes to DB — only suitable for read-only or test use.

🔁 CI/CD Pipeline
Render redeploys automatically when I push to the main branch.

Option to trigger deploy manually.

2. ☁️ AWS EC2 Deployment
✅ Steps Taken
Launched an EC2 instance (Ubuntu).

SSH'd into the server.

Installed Node.js, Git, and dependencies:

bash
Copy
Edit
sudo apt update
sudo apt install nodejs npm git
Cloned the backend repo and installed packages:

bash
Copy
Edit
git clone https://github.com/your/repo.git
cd repo
npm install
Used pm2 to keep the backend running:

bash
Copy
Edit
npm install -g pm2
pm2 start index.js
Opened port (like 3000) in the security group.

⚠️ Issues Faced
SQLite permissions and path issues (used absolute paths).

Had to configure firewall/security group to allow traffic.

🔁 CI/CD Pipeline
Manual deployment; CI/CD can be added using GitHub Actions with SSH.

3. 🧬 Vercel Serverless Function Deployment
✅ Steps Taken
Created a new folder in the repo: /api.

Added a file like handler.js:

js
Copy
Edit
export default function handler(req, res) {
  const sqlite3 = require('sqlite3').verbose();
  const db = new sqlite3.Database('./mydb.sqlite');
  db.all("SELECT * FROM users", [], (err, rows) => {
    if (err) return res.status(500).json({ error: err.message });
    res.status(200).json({ data: rows });
  });
}
Pushed the project to GitHub and imported it into Vercel.

Vercel auto-detected the API routes in /api and deployed them as serverless functions.

⚠️ Issues Faced
SQLite is not ideal in serverless because:

No filesystem persistence

Cold starts can cause issues with DB access

Used read-only SQLite file included in repo (small DB only).

Had to ensure DB file was bundled during deployment (placed inside /api or root and required carefully).

🔁 CI/CD Pipeline
Vercel auto-redeploys on push.

Each API route inside /api is an independent serverless function.

🧠 Summary

Platform	SQLite3 Support	Persistent DB?	CI/CD
Render	✅ (for demo)	❌	Auto on push
EC2	✅	✅	Manual / GitHub Actions
Vercel	⚠️ (read-only)	❌	Auto on push
