# LLM Basic Chatbot

A conversational chatbot web application powered by a large language model (LLM). This project demonstrates how to build an interactive chatbot interface using Flask and the Hugging Face Transformers library.

## Features

- **Web-based Interface**: Clean and intuitive chat interface built with HTML, CSS, and JavaScript
- **Conversational AI**: Powered by Facebook's BlenderBot-400M-distill model for natural conversations
- **Conversation Memory**: Maintains conversation history for contextual responses
- **CORS Support**: Enables cross-origin requests for flexibility in deployment
- **Docker Support**: Containerized application for easy deployment

## Project Structure

```
.
├── chatbot.py              # Flask backend with LLM integration
├── requirements.txt        # Python dependencies
├── Dockerfile              # Docker configuration
├── README.md              # This file
├── templates/
│   └── index.html         # Chat interface HTML
└── static/
    ├── script.js          # Frontend JavaScript logic
    └── css/
        └── style.css      # Styling
```

## Prerequisites

- Python 3.10 or higher
- pip package manager
- (Optional) Docker for containerized deployment

## Installation

### Local Setup

1. **Clone or download the project**
   ```bash
   cd LLM_basic_chatbot
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   venv\Scripts\activate  # On Windows
   # or
   source venv/bin/activate  # On macOS/Linux
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Running Locally

Start the Flask development server:
```bash
python chatbot.py
```

The application will be available at `http://localhost:5000`

### Running with Docker

1. **Build the Docker image**
   ```bash
   docker build -t llm-chatbot .
   ```

2. **Run the Docker container**
   ```bash
   docker run -p 5000:5000 llm-chatbot
   ```

Access the chatbot at `http://localhost:5000`

## Dependencies

The project requires the following Python packages (see `requirements.txt`):

- **Flask**: Web framework for building the backend API
- **Flask-CORS**: Enables Cross-Origin Resource Sharing
- **torch**, **torchvision**, **torchaudio**: PyTorch deep learning framework
- **transformers**: Hugging Face library for LLM models

## Model

The chatbot uses **Facebook's BlenderBot-400M-distill** model by default:
- A distilled 400M parameter conversational model
- Trained on diverse conversational data
- Lightweight and suitable for CPU/GPU inference

**Note**: The code includes commented alternative model (Mistral-7B-Instruct) that can be enabled for different conversation styles.

## API Endpoints

### `GET /`
Returns the chatbot web interface (index.html)

### `POST /chatbot`
Accepts a chat message and returns a model-generated response

**Request:**
```json
{
  "prompt": "Your message here"
}
```

**Response:**
```
Model-generated response text
```

## How It Works

1. User sends a message through the web interface
2. JavaScript sends the message to the `/chatbot` endpoint
3. Flask backend processes the message with the LLM:
   - Combines message with conversation history
   - Tokenizes input
   - Generates response using the model
   - Maintains conversation history for context
4. Response is returned to frontend and displayed in chat

## Configuration

To use a different model, edit `chatbot.py` and uncomment/modify the model configuration:

```python
# Example: Using Mistral-7B-Instruct
model_name = "mistralai/Mistral-7B-Instruct"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name, device_map="auto")
```

## Deployment

### On a Server

1. Install dependencies in a virtual environment
2. Run with a production WSGI server (e.g., Gunicorn):
   ```bash
   pip install gunicorn
   gunicorn -w 4 -b 0.0.0.0:5000 chatbot:app
   ```

### On Cloud Platforms

This application can be deployed to platforms like:
- **Heroku** (using Procfile)
- **AWS** (using EC2 or container services)
- **Google Cloud** (using Cloud Run or App Engine)
- **Azure** (using App Service or Container Instances)

## Performance Notes

- First run: Model download (~500MB-1GB) may take several minutes
- GPU recommended for faster inference (set device_map appropriately)
- Conversation history grows with each interaction; consider implementing history limits for long sessions

## Browser Compatibility

The web interface works on all modern browsers:
- Chrome/Chromium
- Firefox
- Safari
- Edge

## Troubleshooting

**Issue**: Model takes a long time to load
- **Solution**: This is normal on first run. Subsequent runs will be faster.

**Issue**: Out of memory errors
- **Solution**: Consider using a smaller model or increasing available RAM/VRAM.

**Issue**: CORS errors in browser console
- **Solution**: Flask-CORS is configured; ensure you're accessing via `localhost:5000`

## Future Enhancements

- Multi-language support
- User authentication
- Conversation persistence (database storage)
- Model fine-tuning on custom data
- Response streaming for real-time output
- Custom model selection from UI

## License

This project is provided as-is for educational and personal use.

## Author

Created by JC Chen

## Support

For issues or questions, please refer to:
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Hugging Face Transformers Documentation](https://huggingface.co/docs/transformers/)
- [PyTorch Documentation](https://pytorch.org/docs/)