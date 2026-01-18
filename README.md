# OCR Document Processing with LangChain and Gemini

Extract tax and total amounts from invoice documents using Optical Character Recognition (OCR), Regular Expressions, and AI-powered extraction with Google Gemini.

## Features

- **OCR Text Extraction**: Uses Tesseract to extract text from invoice images
- **Multiple Extraction Methods**:
  - Regex-based pattern matching for structured data
  - Google Gemini LLM for intelligent extraction
  - Simple agent-based orchestration
- **Invoice Data Extraction**: Automatically extracts Tax and Total amounts
- **LangChain Integration**: Tool-based approach for modular document processing

## Prerequisites

- Python 3.8+
- Tesseract-OCR (for Windows: [Download](https://github.com/UB-Mannheim/tesseract/wiki))
- Google Gemini API Key (free tier available)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/mars-alien/document_processing_with-_OCR.git
cd OCR
```

### 2. Create Virtual Environment

```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Install Tesseract-OCR (Windows)

1. Download the installer from: https://github.com/UB-Mannheim/tesseract/wiki
2. Install to default location: `C:\Program Files\Tesseract-OCR`
3. Verify installation:
   ```bash
   tesseract --version
   ```

**For Linux/Mac:**
```bash
# macOS with Homebrew
brew install tesseract

# Ubuntu/Debian
sudo apt-get install tesseract-ocr
```

## Configuration

### 1. Set Up Environment Variables

Create a `.env` file in the `OCR` directory:

```env
GOOGLE_API_KEY=your_google_api_key_here
```

### 2. Get Google Gemini API Key

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Click "Create API Key"
3. Copy the key to your `.env` file

### 3. Update Tesseract Path (if needed)

In `document_processing_with_ocr.ipynb`, update this line if Tesseract is installed elsewhere:

```python
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
```

## Usage

### Run the Jupyter Notebook

```bash
jupyter notebook document_processing_with_ocr.ipynb
```

### Basic Workflow

The notebook demonstrates three extraction methods:

1. **OCR Text Extraction**
   ```python
   ocr_text = ocr_read_document.run(image_path)
   ```

2. **Regex Extraction**
   - Extracts Tax and Total using regex patterns
   - Fast but requires well-formatted documents

3. **Gemini LLM Extraction**
   - Uses Google Gemini for intelligent extraction
   - Works with varied invoice formats
   - More accurate for complex documents

4. **Agent-Based Approach**
   - Orchestrates OCR and extraction steps
   - Provides structured results

### Example

```python
from PIL import Image
import pytesseract

# Load and display invoice
image_path = r'E:\Jupyter\OCR\invoice.png'
img = Image.open(image_path)

# Extract text using OCR
ocr_text = ocr_read_document.run(image_path)

# Extract amounts using Gemini
# (See notebook for full implementation)
```

## Project Structure

```
OCR/
├── document_processing_with_ocr.ipynb  # Main notebook with all extraction methods
├── requirements.txt                     # Python dependencies
├── .env.example                         # Template for environment variables
├── invoice.png                          # Sample invoice image
└── README.md                            # This file
```

## Dependencies

- **pytesseract**: OCR text extraction wrapper
- **PIL (Pillow)**: Image processing
- **python-dotenv**: Environment variable management
- **google-generativeai**: Google Gemini API client
- **langchain**: Tool and agent framework
- **IPython**: Jupyter notebook support

See `requirements.txt` for full dependency list.

## Troubleshooting

### Issue: Tesseract not found
**Solution**: Verify Tesseract installation and update the path in the notebook:
```python
pytesseract.pytesseract.tesseract_cmd = r'your/path/to/tesseract.exe'
```

### Issue: Google API Key not found
**Solution**: Ensure `.env` file exists in the project directory with:
```env
GOOGLE_API_KEY=your_actual_key
```

### Issue: Image not found
**Solution**: Update the `image_path` variable to point to your invoice image:
```python
image_path = r'C:\full\path\to\your\invoice.png'
```

### Issue: OCR results are poor quality
**Solution**: 
- Ensure invoice image is clear and well-lit
- Try preprocessing the image (grayscale, contrast adjustment)
- Use Gemini extraction for better accuracy

## Performance Notes

- **Regex Extraction**: Fast (~1-2 seconds), requires consistent formatting
- **Gemini Extraction**: Slower (~5-10 seconds), more accurate for varied formats
- **Agent Approach**: Good for orchestrating multiple steps

## Future Enhancements

- [ ] Support multiple document types (receipts, expense reports)
- [ ] Batch processing for multiple invoices
- [ ] Extract additional fields (date, vendor, line items)
- [ ] Web API interface
- [ ] Database integration for storing extracted data

## Security

⚠️ **Important**: Never commit `.env` files with API keys to version control. Use `.env.example` as a template instead.

```bash
# Add to .gitignore
.env
__pycache__/
.ipynb_checkpoints/
```

## License

This project is open source. Feel free to use and modify for your purposes.

## Support

For issues, questions, or contributions, please visit the [GitHub repository](https://github.com/mars-alien/document_processing_with-_OCR).

---

**Created**: January 2026
