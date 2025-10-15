# Credit Card Statement Parser 💳

A Flask-based web application that automatically extracts key information from credit card statements across multiple banks using PDF parsing and pattern recognition.

## 📋 Features

- **Multi-Bank Support**: Parses statements from 5 major banks:
  - Axis Bank
  - Citibank
  - HDFC Bank
  - ICICI Bank
  - Silk Bank

- **Smart Extraction**: Automatically detects and extracts:
  - Cardholder Name
  - Card Number (Last 4 digits)
  - Credit Limit
  - Total Amount Due
  - Payment Due Date

- **Multiple Output Formats**: 
  - JSON export
  - CSV export
  - Real-time web display

- **Batch Processing**: Upload and parse up to 5 PDF statements simultaneously

- **User-Friendly Interface**: 
  - Drag & drop file upload
  - Progress indicators
  - Detailed parsing results
  - Error handling and validation

## 🏗️ Project Structure

```
credit_parser/
├── app.py                      # Flask application & routes
├── config.py                   # Configuration settings
├── requirements.txt            # Python dependencies
│
├── parsers/                    # Bank-specific parsers
│   ├── __init__.py
│   ├── base.py                # Base parser class
│   ├── bank_detector.py       # Automatic bank detection
│   ├── axis.py               # Axis Bank parser
│   ├── citi.py               # Citibank parser
│   ├── hdfc.py               # HDFC Bank parser
│   ├── icici.py              # ICICI Bank parser
│   └── silk.py               # Silk Bank parser
│
├── utils/                      # Utility modules
│   ├── __init__.py
│   ├── pdf_utils.py           # PDF text extraction & OCR
│   ├── data_io.py             # JSON/CSV export functions
│   └── text_utils.py          # Regex & text processing
│
├── templates/                  # HTML templates
│   └── index.html             # Main web interface
│
├── static/                     # Static assets
│   ├── main.js                # Frontend JavaScript
│   └── style.css              # CSS styling
│
├── uploads/                    # Temporary PDF storage
└── output/                     # Parsed results
    ├── parsed_data.json
    └── parsed_data.csv
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Git (for cloning)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/OmMakwana02/CreditCardParser
   cd "Credit Card Statement Parser"
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   # Windows
   python -m venv venv
   venv\Scripts\activate

   # macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Create required directories** (if not present)
   ```bash
   mkdir uploads output
   ```

### Running the Application

1. **Start the Flask server**
   ```bash
   python app.py
   ```

2. **Access the web interface**
   - Open your browser and navigate to: `http://127.0.0.1:5000`
   - Or: `http://localhost:5000`

3. **Upload and parse statements**
   - Drag and drop PDF files (or click to browse)
   - Click "Parse Statements"
   - View results and download JSON/CSV

## 📦 Dependencies

### Core Libraries
- **Flask** (2.3.0+) - Web framework
- **pdfplumber** (0.9.0+) - PDF text extraction
- **pandas** (2.0.0+) - Data manipulation & CSV export
- **Werkzeug** (2.3.0+) - File upload handling

### Optional (for OCR support)
- **pytesseract** (0.3.10+) - OCR engine wrapper
- **pdf2image** (1.16.0+) - Convert PDF to images for OCR
- **Pillow** (10.0.0+) - Image processing

### Full `requirements.txt`
```
Flask==2.3.0
pdfplumber==0.9.0
pandas==2.0.0
pytesseract==0.3.10
pdf2image==1.16.0
Pillow==10.0.0
python-dotenv==1.0.0
Werkzeug==2.3.0
```

## 🎯 Usage

### Web Interface

1. **Upload PDFs**
   - Click the upload area or drag files
   - Maximum 5 files per batch
   - Each file must be under 10MB

2. **Parse Statements**
   - Click "Parse Statements" button
   - Wait for processing (automatic bank detection)
   - View results in real-time

3. **Download Results**
   - Click "Download JSON" or "Download CSV"
   - Files saved in `output/` directory

### API Endpoints

- `GET /` - Main web interface
- `POST /parse` - Upload and parse PDFs
- `GET /download/json` - Download JSON results
- `GET /download/csv` - Download CSV results
- `GET /health` - Health check endpoint



## 📊 Output Format

### JSON Output
```json
[
  {
    "bank": "axis",
    "filename": "AXIS.pdf",
    "status": "success",
    "cardholder_name": "JOHN DOE",
    "card_number": "1234",
    "credit_limit": "50000.00",
    "total_due": "15000.00",
    "payment_due_date": "2024-11-15"
  }
]
```

### CSV Output
```csv
bank,filename,status,cardholder_name,card_number,credit_limit,total_due,payment_due_date
axis,AXIS.pdf,success,JOHN DOE,1234,50000.00,15000.00,2024-11-15
