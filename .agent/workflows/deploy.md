---
description: Deploy the Medical Analysis Assistant to Streamlit Cloud
---

# Deployment Workflow for Medical Analysis Assistant

## Option 1: Deploy to Streamlit Community Cloud (Recommended)

### Prerequisites
1. A GitHub account
2. Your code pushed to a GitHub repository
3. A Streamlit Community Cloud account (free at https://share.streamlit.io/)

### Steps

1. **Ensure your code is on GitHub**
   - If not already done, create a GitHub repository
   - Push your code to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit for deployment"
   git remote add origin https://github.com/YOUR_USERNAME/medical-analysis-assistant.git
   git push -u origin main
   ```

2. **Sign up for Streamlit Community Cloud**
   - Go to https://share.streamlit.io/
   - Sign in with your GitHub account
   - Grant Streamlit access to your repositories

3. **Deploy the app**
   - Click "New app" button
   - Select your repository: `medical-analysis-assistant`
   - Set the main file path: `main.py`
   - Click "Deploy"

4. **Wait for deployment**
   - Streamlit will automatically install dependencies from `requirements.txt`
   - The app will be live at: `https://YOUR_USERNAME-medical-analysis-assistant.streamlit.app`

### Important Notes
- Make sure all model files are included in your repository (`.tflite`, `.joblib` files)
- Ensure all image assets are present (`Health.png`, `healthy.png`)
- The `requirements.txt` must contain all necessary dependencies

---

## Option 2: Test Locally Before Deployment

// turbo
1. **Navigate to project directory**
```bash
cd d:\medical-analysis-assistant-main\medical-analysis-assistant-main
```

// turbo
2. **Install dependencies** (if not already installed)
```bash
pip install -r requirements.txt
```

// turbo
3. **Run the Streamlit app locally**
```bash
streamlit run main.py
```

4. **Access the app**
   - Open your browser to `http://localhost:8501`
   - Test all features to ensure everything works

---

## Option 3: Deploy to Heroku

### Prerequisites
- Heroku account
- Heroku CLI installed

### Additional Files Needed

1. **Create `Procfile`**
```
web: sh setup.sh && streamlit run main.py
```

2. **Create `setup.sh`**
```bash
mkdir -p ~/.streamlit/

echo "\
[server]\n\
port = $PORT\n\
enableCORS = false\n\
headless = true\n\
\n\
" > ~/.streamlit/config.toml
```

3. **Deploy to Heroku**
```bash
heroku login
heroku create your-app-name
git push heroku main
```

---

## Option 4: Deploy to Docker

1. **Create `Dockerfile`**
```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8501

CMD ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

2. **Build and run Docker container**
```bash
docker build -t medical-analysis-assistant .
docker run -p 8501:8501 medical-analysis-assistant
```

---

## Troubleshooting

### Common Issues

1. **Missing dependencies**
   - Ensure all packages are listed in `requirements.txt`
   - Check Python version compatibility

2. **Model files not found**
   - Verify all `.tflite` and `.joblib` files are in the `models/` directory
   - Check file paths in your code

3. **Image files not loading**
   - Ensure `Health.png` and `healthy.png` are in the root directory
   - Use relative paths in your code

4. **OpenAI API key issues**
   - Set environment variable: `OPENAI_API_KEY`
   - For Streamlit Cloud: Add in "App settings" → "Secrets"

### Setting Secrets in Streamlit Cloud

If your app uses API keys (like OpenAI):

1. Go to your app settings on Streamlit Cloud
2. Click on "Secrets"
3. Add your secrets in TOML format:
```toml
OPENAI_API_KEY = "your-api-key-here"
```
