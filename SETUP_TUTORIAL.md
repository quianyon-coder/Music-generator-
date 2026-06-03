# 🎵 Music Generator - Complete Setup Tutorial

A step-by-step guide to get your Music Generator app up and running!

## 📋 Prerequisites

Before you start, make sure you have:
- **Python 3.9 or higher** - [Download](https://www.python.org/downloads/)
- **Git** - [Download](https://git-scm.com/download)
- **A code editor** (VS Code, PyCharm, etc.)
- **Command line/Terminal** access

### Check if you have Python installed:
```bash
python --version
# or
python3 --version
```

---

## 🚀 Installation Guide

### Step 1: Clone the Repository

```bash
git clone https://github.com/quianyon-coder/Music-generator-.git
cd Music-generator-
```

**What this does**: Downloads the Music Generator code to your computer.

---

### Step 2: Create a Virtual Environment

A virtual environment keeps your project dependencies isolated.

**On macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

**On Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**Expected output**: Your terminal should now show `(venv)` at the beginning.

---

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

**What this does**: Installs all required Python packages:
- Flask (web framework)
- SQLAlchemy (database)
- JWT (authentication)
- music21 (music generation)
- librosa (audio processing)
- numpy & scipy (math libraries)
- And more...

**Installation time**: 5-10 minutes (first time can be slower)

---

### Step 4: Configure Environment Variables

```bash
cp .env.example .env
```

Open the `.env` file and update these settings:

```env
# Flask Configuration
FLASK_ENV=development
FLASK_APP=run.py
DEBUG=True

# Database (Using SQLite for local development)
DATABASE_URL=sqlite:///music_generator.db
SQLALCHEMY_TRACK_MODIFICATIONS=False

# JWT Configuration
JWT_SECRET_KEY=change-this-to-a-random-secret-key-12345!@#$%
JWT_ACCESS_TOKEN_EXPIRES=3600

# File Upload
UPLOAD_FOLDER=uploads
MAX_CONTENT_LENGTH=52428800
ALLOWED_EXTENSIONS=wav,mp3,flac

# Audio Settings
DEFAULT_SAMPLE_RATE=44100
DEFAULT_DURATION=30
DEFAULT_TEMPO=120
```

**Important**: Change `JWT_SECRET_KEY` to a unique value for security!

Generate a secure key:
```bash
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

---

### Step 5: Initialize the Database

```bash
python -c "from app import create_app, db; app = create_app(); app.app_context().push(); db.create_all(); print('Database initialized!')"
```

**What this does**: Creates the SQLite database with all tables.

**Expected output**:
```
Database initialized!
```

---

### Step 6: Create Upload Folder

```bash
mkdir -p uploads
```

This folder will store generated music files.

---

### Step 7: Run the Application

```bash
python run.py
```

**Expected output**:
```
 * Running on http://127.0.0.1:5000
 * Debug mode: on
 * WARNING: This is a development server. Do not use it in production deployment.
```

The app is now running! 🎉

---

## 📱 Testing the API

Once the app is running, you can test it using **Postman**, **cURL**, or **Thunder Client**.

### 1. Register a New User

**Endpoint**: `POST http://localhost:5000/api/auth/register`

**Headers**:
```
Content-Type: application/json
```

**Body**:
```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "SecurePassword123!",
  "full_name": "John Doe"
}
```

**Response** (201 Created):
```json
{
  "message": "User registered successfully",
  "user": {
    "id": "abc123...",
    "username": "john_doe",
    "email": "john@example.com",
    "full_name": "John Doe",
    "created_at": "2026-06-03T12:00:00"
  }
}
```

---

### 2. Login

**Endpoint**: `POST http://localhost:5000/api/auth/login`

**Body**:
```json
{
  "email": "john@example.com",
  "password": "SecurePassword123!"
}
```

**Response** (200 OK):
```json
{
  "message": "Login successful",
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "abc123...",
    "username": "john_doe",
    "email": "john@example.com"
  }
}
```

**Save the `access_token` - you'll need it for all other requests!**

---

### 3. Generate Music

**Endpoint**: `POST http://localhost:5000/api/music/generate`

**Headers**:
```
Content-Type: application/json
Authorization: Bearer YOUR_ACCESS_TOKEN_HERE
```

**Body**:
```json
{
  "title": "Happy Birthday Song",
  "description": "A cheerful birthday celebration",
  "words": ["joy", "celebration", "happiness", "birthday"],
  "mood": "happy",
  "tempo": 120,
  "duration": 30,
  "instruments": ["piano", "violin"],
  "people_names": ["Alice", "Bob", "Charlie"],
  "file_format": "mp3"
}
```

**Response** (201 Created):
```json
{
  "message": "Music generated successfully",
  "music": {
    "id": "music_id_123",
    "title": "Happy Birthday Song",
    "description": "A cheerful birthday celebration",
    "mood": "happy",
    "tempo": 120,
    "duration": 30,
    "instruments": ["piano", "violin"],
    "people_names": ["Alice", "Bob", "Charlie"],
    "file_format": "mp3",
    "file_size": 245000,
    "duration_actual": 30.5,
    "created_at": "2026-06-03T12:05:00",
    "is_public": false,
    "download_count": 0
  }
}
```

---

### 4. Get Your Music Library

**Endpoint**: `GET http://localhost:5000/api/music/list`

**Headers**:
```
Authorization: Bearer YOUR_ACCESS_TOKEN_HERE
```

**Response** (200 OK):
```json
{
  "total": 5,
  "pages": 1,
  "current_page": 1,
  "music": [
    {
      "id": "music_id_123",
      "title": "Happy Birthday Song",
      "mood": "happy",
      "tempo": 120,
      "created_at": "2026-06-03T12:05:00",
      "download_count": 0
    },
    ...
  ]
}
```

---

### 5. Download Music

**Endpoint**: `GET http://localhost:5000/api/music/{music_id}/download`

**Headers**:
```
Authorization: Bearer YOUR_ACCESS_TOKEN_HERE
```

This will download the MP3 file to your computer.

---

### 6. Get User Profile

**Endpoint**: `GET http://localhost:5000/api/user/profile`

**Headers**:
```
Authorization: Bearer YOUR_ACCESS_TOKEN_HERE
```

**Response**:
```json
{
  "id": "abc123...",
  "username": "john_doe",
  "email": "john@example.com",
  "full_name": "John Doe",
  "created_at": "2026-06-03T12:00:00"
}
```

---

## 🛠️ Using Postman (Recommended)

Postman makes testing APIs easier. Here's how to set it up:

### 1. Download Postman
https://www.postman.com/downloads/

### 2. Create a New Collection

Click **New** → **Collection** → Name it "Music Generator"

### 3. Add Requests

For each endpoint, create a new request:
- Set method (POST, GET, DELETE)
- Enter URL
- Add headers
- Add body (for POST requests)

### 4. Use Environment Variables

Create an environment variable for your token:
```
access_token = YOUR_TOKEN_HERE
```

Then use it in headers:
```
Authorization: Bearer {{access_token}}
```

---

## 🎵 Music Generation Parameters Explained

### Moods Available:
- `happy` - Upbeat, joyful melody
- `sad` - Melancholic, slower tempo
- `energetic` - Fast, dynamic
- `calm` - Peaceful, relaxing
- `mysterious` - Intriguing, atmospheric
- `romantic` - Gentle, emotional
- `dramatic` - Intense, powerful

### Instruments Available:
- `piano` - Classic piano sound
- `violin` - Elegant strings
- `flute` - Light, airy
- `guitar` - Acoustic/electric
- `synth` - Electronic sounds
- `drums` - Rhythm/percussion
- `bass` - Low-end tones
- `trumpet` - Brass instrument

### Tempo Range:
- Minimum: 60 BPM (slow)
- Maximum: 200 BPM (fast)
- Default: 120 BPM (standard)

### Duration:
- Measured in seconds
- Default: 30 seconds
- Can be any value you want

---

## 🐛 Troubleshooting

### Issue: "Python not found"
**Solution**: 
- Make sure Python is installed
- On Windows, use `python` or `py`
- On macOS/Linux, use `python3`

### Issue: "ModuleNotFoundError: No module named 'flask'"
**Solution**: 
- Make sure virtual environment is activated
- Run `pip install -r requirements.txt` again

### Issue: "Address already in use"
**Solution**: 
- Port 5000 is already in use
- Kill the process: `lsof -ti:5000 | xargs kill -9`
- Or change port in `run.py`

### Issue: "Database error"
**Solution**: 
- Delete `music_generator.db` file
- Run initialization again: `python -c "from app import create_app, db; app = create_app(); app.app_context().push(); db.create_all()"`

### Issue: "Audio files not generating"
**Solution**: 
- Check if `uploads/` folder exists
- Verify all audio dependencies are installed
- Check console for error messages

---

## 📚 Using Thunder Client (VS Code Alternative)

If you use VS Code, Thunder Client is a great Postman alternative:

1. Install Thunder Client extension in VS Code
2. Create requests the same way as Postman
3. Use environment variables for API tokens
4. Save your collection for reuse

---

## 🚀 Next Steps

Once everything is working:

1. **Create a Frontend** - Build a React/Next.js UI
2. **Deploy** - Host on Heroku, AWS, or DigitalOcean
3. **Add Features** - Implement advanced music generation
4. **Database** - Switch from SQLite to PostgreSQL for production

---

## 📞 Need Help?

If you encounter issues:

1. Check the error message in your terminal
2. Look at the troubleshooting section above
3. Check the `.env` file configuration
4. Verify all dependencies are installed: `pip list`
5. Open an issue on GitHub

---

## ✅ Verification Checklist

Before considering setup complete:

- [ ] Python 3.9+ installed
- [ ] Repository cloned
- [ ] Virtual environment created and activated
- [ ] Dependencies installed (`pip install -r requirements.txt`)
- [ ] `.env` file configured
- [ ] Database initialized
- [ ] Upload folder created
- [ ] App running on `http://localhost:5000`
- [ ] Can register a user
- [ ] Can login and get access token
- [ ] Can generate music
- [ ] Can download generated music

---

## 🎉 Congratulations!

Your Music Generator is ready to use! Start creating amazing music! 🎵

**Happy generating!** 🚀
