# 🏥 Patient Onboarding Chatbot

An AI-powered patient onboarding system built with FastAPI backend and HTML/JavaScript frontend. This chatbot guides users through a 3-stage health intake process.

## 🚀 Part 1: Running FastAPI Backend Only

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)

### Step 1: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 2: Start FastAPI Server
```bash
uvicorn main:app --reload
```

✅ **FastAPI server will start on: http://localhost:8000**

### Step 3: Test the API
Visit these URLs in your browser:
- **API Documentation**: http://localhost:8000/docs
- **Alternative Docs**: http://localhost:8000/redoc

### Step 4: Test with curl (Optional)
```bash
# Get welcome message
curl -X POST "http://localhost:8000/chat" \
  -H "Content-Type: application/json" \
  -d '{"session_id": "test123", "message": null}'

# Send a name
curl -X POST "http://localhost:8000/chat" \
  -H "Content-Type: application/json" \
  -d '{"session_id": "test123", "message": "John Smith"}'
```

---

## 🌐 Part 2: Running Both FastAPI + HTML Frontend

### Step 1: Keep FastAPI Running
Make sure your FastAPI server is still running from Part 1:
```bash
uvicorn main:app --reload
```
(Should be running on http://localhost:8000)

### Step 2: Start HTML Frontend
Open a **new terminal** in the same directory and run:
```bash
python3 -m http.server 3000
```

✅ **Frontend will be available at: http://localhost:3000/chat.html**

### Step 3: Use the Chat Interface
1. Open your browser and go to: **http://localhost:3000/chat.html**
2. Start chatting with the onboarding bot
3. Complete the 3-stage process:
   - **Basic Info**: Name, email, phone, etc.
   - **Diet/Lifestyle**: Activity, eating habits
   - **Medical History**: Health conditions

---

## 🔧 Optional Configuration

### Environment Variables
Create a `.env` file in the project root for OpenAI integration:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

**Note**: The system works without OpenAI API key using fallback validation. GPT features enhance the experience but are not required.

## 📁 Project Structure

```
onboarding/
├── main.py              # FastAPI backend
├── chat.html            # Frontend interface  
├── requirements.txt     # Python dependencies
├── README.md           # This file
├── .gitignore          # Git ignore rules
└── __pycache__/        # Python cache (ignored)
```

## 🛠️ Development

### Backend Development

The FastAPI server runs with auto-reload enabled. Any changes to `main.py` will automatically restart the server.

**Key endpoints:**
- `POST /chat` - Main chatbot interaction endpoint
- `GET /docs` - Interactive API documentation

### Frontend Development  

The HTML file is served via Python's built-in HTTP server. Refresh your browser to see changes.

**Files:**
- `chat.html` - Complete frontend with CSS and JavaScript embedded

### Testing the API

You can test the API directly using curl:

```bash
# Get welcome message
curl -X POST "http://localhost:8000/chat" \
  -H "Content-Type: application/json" \
  -d '{"session_id": "test123", "message": null}'

# Send a name
curl -X POST "http://localhost:8000/chat" \
  -H "Content-Type: application/json" \
  -d '{"session_id": "test123", "message": "John Smith"}'
```

## 🔍 Validation Features

### Name Validation
- Requires both first and last name
- Accepts natural language: "my name is John Smith"
- Rejects single names or invalid formats

### Phone Validation
- Exactly 10 digits required
- Rejects longer/shorter numbers

### Date of Birth Validation
- YYYY-MM-DD format required
- Rejects future dates
- Rejects unrealistic ages (>120 years)

### Other Validations
- Email format validation
- Weight/height format checking
- Multiple choice validation for categorical questions

## 🚨 Troubleshooting

### Backend Issues

**Port 8000 already in use:**
```bash
# Kill existing process
lsof -ti:8000 | xargs kill -9
# Or use a different port
uvicorn main:app --reload --port 8001
```

**Import errors:**
```bash
# Reinstall dependencies
pip install -r requirements.txt
```

### Frontend Issues

**Port 3000 already in use:**
```bash
# Use a different port
python3 -m http.server 3001
# Then visit http://localhost:3001/chat.html
```

**CORS errors:**
- Ensure both servers are running
- Frontend must be served via HTTP (not file://)
- Backend has CORS middleware enabled

### Connection Issues

If the frontend can't connect to the backend:

1. Verify backend is running on http://localhost:8000
2. Check browser console for error messages
3. Ensure frontend is served via HTTP server (not opened as file)

## 🎨 Customization

### Adding New Questions

Edit the slot lists in `main.py`:

```python
BASIC_SLOTS: List[Slot] = [
    Slot(key="your_field",
         prompt="Your question here?",
         validator_regex=r"your_regex_here"),
    # ... existing slots
]
```

### Styling the Frontend

Modify the CSS in the `<style>` section of `chat.html` to customize the appearance.

### Adding New Validation

Implement custom validation functions in `main.py`:

```python
def validate_your_field(value: str) -> bool:
    # Your validation logic
    return True  # or False
```

## 📄 License

This project is open source. Feel free to modify and distribute according to your needs.

## 🤝 Support

For questions or issues:
1. Check the troubleshooting section above
2. Review the API documentation at http://localhost:8000/docs
3. Examine the browser console for frontend errors
4. Check the terminal output for backend errors

---

**Happy onboarding! 🎉**
