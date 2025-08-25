# 📚 ISBN Extraction from Book Images  

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)  
[![OCR](https://img.shields.io/badge/OCR-Tesseract-green.svg)](https://github.com/tesseract-ocr/tesseract)  
[![Excel](https://img.shields.io/badge/Excel-Pandas-orange.svg)](https://pandas.pydata.org/)  
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](LICENSE)  

---

## 🔎 Overview  
This project extracts **ISBN numbers** from book cover images and updates an Excel file with the results.  

✅ Detect ISBN numbers (10 or 13 digits)  
✅ Map extracted ISBNs to book IDs in Excel  
✅ Handle corrupted/unreadable images  
✅ Fill missing ISBNs as `NULL`  

---

## 📂 Dataset Example  

**Excel File (books.xlsx)**  
| ID     | ISBN |  
|--------|------|  
| Cew34  |      |  
| THR007 |      |  

**Images Folder**  



---

## ⚡ Example Output  

**Updated Excel File**  
| ID     | ISBN           |  
|--------|----------------|  
| Cew34  | "9780393040029"|  
| THR007 | NULL           |  

---

## 🚀 Tech Stack  
- Python 3.8+  
- Tesseract OCR  
- Pandas / OpenPyXL  
- Regex  

---

## ⚙️ Setup  

```bash
git clone https://github.com/your-username/isbn-extraction.git
cd isbn-extraction
pip install -r requirements.txt
```

Run
python extract_isbn.py --images ./sample_data/images --excel ./sample_data/books.xlsx --output ./sample_data/updated_books.xlsx

Output in Console
✅ Found ISBN for Cew34: 9780393040029
❌ No ISBN found in THR007
🎉 Extraction complete! Saved as: updated_books.xlsx

🛡️ MIT License

---

# 📦 requirements.txt  

```txt
pandas
openpyxl
pytesseract
Pillow
opencv-python
```

