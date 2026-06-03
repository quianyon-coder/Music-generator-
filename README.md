# Music Generator

A sophisticated app that generates music using words, descriptions, and person names. This application uses advanced audio synthesis and machine learning to create unique musical compositions.

## Features

- 🎵 **Audio Generation**: Generate music directly from text descriptions
- 👤 **User Authentication**: Secure user registration and login
- 💾 **Save & Store**: Save generated music to your library
- 🎧 **Preview**: Listen to previews before downloading
- 📥 **Export Options**: Download as MP3, WAV, or other formats
- 🎨 **Customization**: Control tempo, mood, instruments, and style
- 📊 **Music Library**: Manage and organize your generated tracks
- 🔄 **Collaboration**: Generate music with multiple people names

## Tech Stack

### Backend
- **Python 3.9+**
- **Flask** - Web framework
- **SQLAlchemy** - ORM
- **music21** - Music generation
- **librosa** - Audio processing
- **pydub** - Audio manipulation
- **JWT** - Authentication
- **PostgreSQL** - Database

### Frontend
- **React** - UI framework
- **Axios** - HTTP client
- **Tailwind CSS** - Styling
- **React Router** - Navigation

## Installation

### Backend Setup

```bash
# Clone the repository
git clone https://github.com/quianyon-coder/Music-generator-.git
cd Music-generator-

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env

# Initialize database
python run.py

# Run the backend
python run.py
```

### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm start
```

## Usage

1. **Register/Login**: Create an account
2. **Create Music**: Provide words, descriptions, and person names
3. **Customize**: Adjust parameters like tempo, mood, instruments
4. **Generate**: Click generate to create unique audio
5. **Listen**: Preview the generated music
6. **Export**: Download in your preferred format

## API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout

### Music Generation
- `POST /api/music/generate` - Generate new music
- `GET /api/music/list` - Get user's music library
- `GET /api/music/<id>` - Get specific music details
- `DELETE /api/music/<id>` - Delete music

### User
- `GET /api/user/profile` - Get user profile
- `PUT /api/user/profile` - Update profile

## Project Structure

```
Music-generator-/
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── models/
│   │   ├── routes/
│   │   ├── services/
│   │   └── utils/
│   ├── migrations/
│   ├── tests/
│   ├── requirements.txt
│   ├── config.py
│   └── run.py
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   └── App.js
│   └── package.json
└── README.md
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see LICENSE file for details.

## Support

For issues and questions, please open an issue on GitHub.

---

**Happy Music Generating! 🎶**
