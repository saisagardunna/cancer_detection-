# 🚀 Deployment Guide for Medical Analysis Assistant

## Quick Start - Deploy to Streamlit Community Cloud (FREE)

### Prerequisites
1. ✅ GitHub account
2. ✅ Streamlit Community Cloud account (sign up at https://share.streamlit.io/)
3. ✅ OpenAI API key (get from https://platform.openai.com/api-keys)

---

## Step-by-Step Deployment

### 1️⃣ Push Your Code to GitHub

If you haven't already created a GitHub repository:

1. Go to https://github.com/new
2. Create a new repository (e.g., `medical-analysis-assistant`)
3. **DO NOT** initialize with README (your code already has one)

Then run these commands in your terminal:

```bash
# Add all files to git
git add .

# Commit your changes
git commit -m "Initial commit - Medical Analysis Assistant"

# Add your GitHub repository as remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/medical-analysis-assistant.git

# Push to GitHub
git push -u origin main
```

> **Note:** If you get an error about 'master' vs 'main', run: `git branch -M main` first

---

### 2️⃣ Deploy to Streamlit Community Cloud

1. **Go to Streamlit Cloud**
   - Visit https://share.streamlit.io/
   - Click "Sign in with GitHub"
   - Authorize Streamlit to access your repositories

2. **Create New App**
   - Click the "New app" button
   - Select your repository from the dropdown
   - **Repository:** `YOUR_USERNAME/medical-analysis-assistant`
   - **Branch:** `main`
   - **Main file path:** `main.py`

3. **Configure Secrets (IMPORTANT! )**
   - Before deploying, click "Advanced settings"
   - In the "Secrets" section, add:
   ```toml
   OPENAI_API_KEY = "sk-your-actual-api-key-here"
   ```
   - Replace with your actual OpenAI API key

4. **Deploy!**
   - Click "Deploy!"
   - Wait 2-5 minutes for deployment
   - Your app will be live at: `https://YOUR_USERNAME-medical-analysis-assistant.streamlit.app`

---

## 🔒 Security Notes

### ⚠️ IMPORTANT: API Key Security

Your OpenAI API key has been removed from the code for security. To use the Health Assistant feature:

**For Local Development:**
1. Copy `.streamlit/secrets.toml.template` to `.streamlit/secrets.toml`
2. Add your OpenAI API key to `.streamlit/secrets.toml`
3. Never commit `.streamlit/secrets.toml` to git (it's already in .gitignore)

**For Streamlit Cloud:**
- Add your API key in the Streamlit Cloud dashboard:
  1. Go to your app settings
  2. Click "Secrets" in the sidebar
  3. Add your OPENAI_API_KEY

---

## 🧪 Testing Locally First

Before deploying, test your app locally:

```bash
# Install dependencies
pip install -r requirements.txt

# Run the app
streamlit run main.py
```

The app will open at `http://localhost:8501`

---

## 📁 Required Files for Deployment

Make sure these files/folders are in your repository:

- ✅ `main.py` - Main application file
- ✅ `requirements.txt` - Python dependencies
- ✅ `apps/` folder - All page modules
- ✅ `models/` folder - ML model files (.tflite, .joblib)
- ✅ `Health.png` - Logo image
- ✅ `.gitignore` - Excludes unnecessary files

---

## 🛠️ Troubleshooting

### Issue: "ModuleNotFoundError"
**Solution:** Make sure all dependencies are in `requirements.txt`

### Issue: "Model file not found"
**Solution:** Verify all model files are committed to git:
- `models/heart.joblib`
- `models/skinmodel.tflite`
- `models/tb_model.tflite`

### Issue: "OpenAI API Error"
**Solution:** 
1. Verify your API key is valid
2. Check you have credits in your OpenAI account
3. Ensure the key is properly added to Streamlit secrets

### Issue: "Image not loading"
**Solution:** Check that `Health.png` is in the repository root

---

## 🌐 Alternative Deployment Options

### Option 2: Deploy with Docker

Create a `Dockerfile`:
```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

EXPOSE 8501
CMD ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

Build and run:
```bash
docker build -t medical-assistant .
docker run -p 8501:8501 medical-assistant
```

### Option 3: Deploy to Heroku

1. Create `Procfile`:
```
web: sh setup.sh && streamlit run main.py
```

2. Create `setup.sh`:
```bash
mkdir -p ~/.streamlit/
echo "[server]
port = $PORT
enableCORS = false
headless = true
" > ~/.streamlit/config.toml
```

3. Deploy:
```bash
heroku login
heroku create your-app-name
git push heroku main
```

---

## 📊 Monitoring Your Deployed App

Once deployed on Streamlit Cloud:
- View app logs in the Streamlit Cloud dashboard
- Monitor resource usage
- See visitor analytics
- Update secrets without redeploying

---

## 🔄 Updating Your Deployed App

To update your live app:

```bash
# Make your changes
git add .
git commit -m "Description of changes"
git push origin main
```

Streamlit Cloud will automatically redeploy your app!

---

## ✅ Deployment Checklist

- [ ] Repository created on GitHub
- [ ] Code pushed to GitHub
- [ ] All model files committed
- [ ] Images (Health.png) included
- [ ] Streamlit Community Cloud account created
- [ ] OpenAI API key ready
- [ ] App deployed on Streamlit Cloud
- [ ] Secrets configured in Streamlit Cloud
- [ ] App tested and working

---

## 🎉 Success!

Your Medical Analysis Assistant should now be live and accessible to anyone with the URL!

**Share your app:**
- Share the URL: `https://your-app-url.streamlit.app`
- Add a badge to your README:
  ```markdown
  [![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://your-app-url.streamlit.app)
  ```

---

## 📞 Need Help?

- Streamlit Documentation: https://docs.streamlit.io/
- Streamlit Community Forum: https://discuss.streamlit.io/
- Streamlit Cloud Docs: https://docs.streamlit.io/streamlit-community-cloud
