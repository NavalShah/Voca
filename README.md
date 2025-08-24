# Voca - Speech Therapy ML Application

> Helping people who stutter become more confident, one word at a time.

## Overview

Voca is an intelligent web application that uses machine learning to help people who stutter by identifying and highlighting difficult-to-pronounce words in text. The system learns from user feedback to provide personalized word difficulty predictions and suggests easier alternatives.

### Key Features

- **Personalized Word Difficulty Detection**: Uses machine learning to identify words that may be challenging to pronounce based on your individual speech patterns
- **Active Learning**: The system continuously improves by learning from your feedback about which words are easy or difficult for you
- **Alternative Word Suggestions**: Provides phonetically similar but easier-to-pronounce alternatives for difficult words
- **Real-time Text Analysis**: Highlights difficult words as you type or paste text
- **Adjustable Confidence Threshold**: Control the sensitivity of word highlighting (0-100%)
- **Named Entity Recognition**: Preserves proper nouns and names while analyzing text

### How It Works

1. **Phonetic Analysis**: Each word is converted to a phonetic representation using pre-computed embeddings
2. **Machine Learning Classification**: A Support Vector Machine (SVM) classifier predicts the difficulty of each word
3. **Active Learning Loop**: The system identifies uncertain predictions and asks for your feedback to improve
4. **Alternative Generation**: Uses the Datamuse API to find phonetically similar but easier alternatives

## Installation

### Prerequisites

- Python 3.7 or higher
- pip (Python package installer)
- Git

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/Voca-Research.git
cd Voca-Research
```

### Step 2: Create a Virtual Environment (Recommended)

```bash
# On Windows
python -m venv .venv
.venv\Scripts\activate

# On macOS/Linux
python3 -m venv .venv
source .venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r req.txt
```

### Step 4: Download spaCy Language Model

```bash
python -m spacy download en_core_web_sm
```

### Step 5: Verify Data Files

Ensure the following data files are present in the `data/` directory:
- `phonetic_embd.pickle` - Phonetic embeddings for ~116,000 words
- `default_content.txt` - Sample text for testing
- `TED_transcripts.csv` - TED talk transcripts dataset
- `word_embeddings/glove.wikipedia.bin` - Word embeddings (if using similarity features)

## Running the Application

### Start the Flask Server

```bash
python app.py
```

The application will start on `http://localhost:5000` by default.

### Access the Application

Open your web browser and navigate to:
```
http://localhost:5000
```

## Usage Guide

### Basic Workflow

1. **Enter or Paste Text**: Use the text editor to input the text you want to analyze
2. **Set Your Preferences**: Click "Preferences" to:
   - Add words to your personal easy/difficult lists
   - Adjust the confidence threshold for highlighting
3. **Analyze Text**: Click "Analyze" to process the text and highlight difficult words
4. **Review Suggestions**: Hover over highlighted words to see:
   - Difficulty score
   - Alternative word suggestions
5. **Improve the Model**: Click "Active Learning" to help the system learn your pronunciation patterns

### Features in Detail

#### Text Editor
- Supports rich text formatting
- Real-time word highlighting
- Click on highlighted words to see and select alternatives

#### Preferences Modal
- **Easy Words**: Add words you find easy to pronounce
- **Difficult Words**: Add words you find challenging
- **Confidence Threshold**: Adjust sensitivity (0-100%)
  - Lower values: More words highlighted
  - Higher values: Only very difficult words highlighted

#### Active Learning
- The system identifies words it's uncertain about
- You label them as "Easy" or "Difficult"
- This feedback improves future predictions

#### Alternative Words
- Hover over highlighted words to see suggestions
- Click to replace with an easier alternative
- Alternatives are phonetically similar but easier to pronounce

## File Structure

```
Voca-Research/
├── app.py                 # Main Flask application
├── templates/
│   └── index.html        # Main UI template
├── css/
│   └── editor.css        # Custom styling
├── js/
│   ├── editor.js         # Text editor functionality
│   ├── main.js           # Core application logic
│   └── popover_events.js # UI interactions
├── data/
│   ├── phonetic_embd.pickle      # Phonetic embeddings
│   ├── default_content.txt       # Sample text
│   └── TED_transcripts.csv       # Dataset
├── flask_session/        # Session storage
├── notebook/             # Research notebooks
└── req.txt              # Python dependencies
```

## Troubleshooting

### Common Issues

1. **"Module not found" errors**
   - Ensure you've activated the virtual environment
   - Run `pip install -r req.txt` again

2. **spaCy model not found**
   - Run `python -m spacy download en_core_web_sm`

3. **Port already in use**
   - Change the port in app.py or kill the process using port 5000

4. **Missing data files**
   - Ensure all required pickle files are in the `data/` directory
   - Contact maintainers if files are missing

### Session Issues

The application uses file-based sessions. If you encounter session-related errors:
```bash
# Clear session files
rm -rf flask_session/*
```

## Development

### Running in Debug Mode

Modify the last line in `app.py`:
```python
app.run(debug=True)
```

### Research Notebooks

The `notebook/` directory contains Jupyter notebooks documenting the research:
- `engine.ipynb` - Core ML engine development
- `alternate_words.ipynb` - Alternative word generation research
- `preprocessing phonetic embedding.ipynb` - Phonetic embedding creation
- `TED talk - main.ipynb` - Dataset analysis and model training

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Guidelines

- Follow PEP 8 style guidelines for Python code
- Add comments for complex logic
- Update documentation for new features
- Test thoroughly before submitting PR

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- CMU Pronouncing Dictionary for phonetic data
- spaCy for natural language processing
- Datamuse API for word alternatives
- TED Talks dataset for training data

## Contact

For questions, issues, or contributions, please open an issue on GitHub or contact the maintainers.

---

**Note**: This is a research project aimed at helping people with speech difficulties. The predictions are based on machine learning and should not replace professional speech therapy advice.