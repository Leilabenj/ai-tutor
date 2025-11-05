# Dialy 

An interactive language learning application powered by AI that provides conversational tutoring through voice-based interactions. Practice French or German with real-time feedback, error corrections, and personalized learning experiences.

## Features

- **Voice-Based Interaction**: Record audio and receive spoken responses for natural conversation practice
- **Multi-Language Support**: Currently supports French (Français) and German (Deutsch)
- **AI-Powered Tutoring**: Uses GPT-4o-mini for intelligent, context-aware language instruction
- **Real-Time Error Detection**: Get immediate feedback on grammar, vocabulary, and pronunciation suggestions
- **Session Management**: Save and review past conversations with detailed feedback summaries
- **Teacher Dashboard**: Monitor student progress, view chat sessions, and track learning analytics
- **Mobile-Friendly**: Responsive design optimized for both desktop and mobile devices
- **Flexible Authentication**: Guest login with class ID support or individual accounts

## Tech Stack

- **Frontend**: Streamlit
- **AI/ML**: 
  - OpenAI GPT-4o-mini (conversation generation)
  - OpenAI Whisper (speech-to-text transcription)
  - ElevenLabs & gTTS (text-to-speech)
- **Backend**: Firebase (Firestore for data storage, Authentication)
- **Language**: Python 3.12.6

## Installation

### Prerequisites

- Python 3.12.6
- Firebase account and project
- OpenAI API key
- ElevenLabs API key (optional, falls back to gTTS)

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ai-tutor.git
   cd ai-tutor
   ```

2. **Create a virtual environment**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Streamlit secrets**
   
   Create a `.streamlit/secrets.toml` file with the following structure:
   ```toml
   OPENAI_API_KEY = "your-openai-api-key"
   ELEVENLABS_API_KEY = "your-elevenlabs-api-key"
   FIREBASE_WEB_API_KEY = "your-firebase-web-api-key"
   
   [CRED]
   firebase_cred = {
       # Your Firebase credentials JSON object
       "type": "service_account",
       "project_id": "...",
       # ... rest of Firebase credentials
   }
   ```

5. **Run the application**
   ```bash
   streamlit run prototype.py
   ```

## Usage

### For Students

1. **Login**: Enter your username and either:
   - Provide a class ID (language is auto-detected from class ID)
   - Select your language if you don't have a class ID

2. **Start a Conversation**: 
   - Click "Begin Conversation" to start a new session
   - Optionally provide a roleplay scenario description
   - The AI tutor will introduce itself and suggest conversation topics

3. **Practice Speaking**:
   - Click the microphone button to record your response
   - Wait for transcription and AI response
   - View real-time error corrections and suggestions
   - Access translations of the AI's responses

4. **Review Sessions**:
   - Access previous conversations from the sidebar
   - View detailed feedback summaries after completing a session
   - See conversation history with all messages and corrections

### For Teachers

1. **Access Teacher Dashboard**:
   ```bash
   streamlit run teacher_interface.py
   ```

2. **Login**: Enter your teacher ID to access your assigned classes

3. **Monitor Students**:
   - View student overview with activity statistics
   - Select individual students to review their chat sessions
   - Analyze conversation patterns and learning progress

## Project Structure

```
ai-tutor/
├── prototype.py              # Main Streamlit application
├── dialogue.py               # LLM model and conversation handling
├── transcribe.py             # Speech-to-text using OpenAI Whisper
├── tts.py                    # Text-to-speech conversion
├── teacher_interface.py      # Teacher dashboard
├── utils/
│   ├── auth_functions.py     # Authentication logic
│   ├── db_util.py            # Firestore database operations
│   └── streamlit_utils.py    # Streamlit UI utilities
├── requirements.txt          # Python dependencies
└── README.md                 # This file
```

## Key Components

### Dialogue System (`dialogue.py`)
- Manages conversation history and context
- Generates responses using GPT-4o-mini
- Provides real-time error detection and corrections
- Generates comprehensive feedback summaries

### Speech Processing
- **Transcription** (`transcribe.py`): Converts audio input to text using OpenAI Whisper
- **Text-to-Speech** (`tts.py`): Converts AI responses to audio using ElevenLabs (with gTTS fallback)

### Session Management
- Automatic saving of conversations to Firestore
- Session history and retrieval
- Feedback generation and storage
- Support for custom roleplay scenarios

## Configuration

### Language Selection
The application supports:
- **French (Français)**: Selected when class ID contains "FR" or manually selected
- **German (Deutsch)**: Selected when class ID contains "DE" or manually selected

### Model Configuration
- Default model: `gpt-4o-mini` (configurable in `dialogue.py`)
- Conversation history length: 100 messages (configurable)

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgments

- OpenAI for GPT-4 and Whisper API
- ElevenLabs for high-quality text-to-speech
- Streamlit for the web framework
- Firebase for backend infrastructure

## Support

For issues, questions, or suggestions, please open an issue on the GitHub repository.

---

**Note**: This application requires API keys for OpenAI and optionally ElevenLabs. Make sure to keep your API keys secure and never commit them to version control.
