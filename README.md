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
🐍 extract_isbn.py
import os
import re
import argparse
import pandas as pd
from PIL import Image
import pytesseract

def clean_isbn(text):
    """Extracts ISBN number (10 or 13 digits) from OCR text"""
    text = text.replace("-", "").replace(" ", "")
    matches = re.findall(r"\b\d{10}\b|\b\d{13}\b", text)
    return matches[0] if matches else None

def extract_isbns(image_folder, excel_file, output_file):
    df = pd.read_excel(excel_file)

    if "ISBN" not in df.columns:
        df["ISBN"] = ""

    for idx, row in df.iterrows():
        book_id = row["ID"]
        image_path = os.path.join(image_folder, f"{book_id}.jpg")

        isbn_value = None

        if not os.path.exists(image_path):
            print(f"⚠️ Image not found for ID: {book_id}")
        else:
            try:
                img = Image.open(image_path)
                text = pytesseract.image_to_string(img)

                isbn_value = clean_isbn(text)

                if isbn_value:
                    print(f"✅ Found ISBN for {book_id}: {isbn_value}")
                else:
                    print(f"❌ No ISBN found in {book_id}")

            except Exception as e:
                print(f"🚨 Error processing {book_id}: {e}")

        df.at[idx, "ISBN"] = isbn_value if isbn_value else "NULL"

    df.to_excel(output_file, index=False)
    print(f"\n🎉 Extraction complete! Updated file saved as: {output_file}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Extract ISBNs from book cover images and update Excel.")
    parser.add_argument("--images", required=True, help="Path to the folder containing book cover images")
    parser.add_argument("--excel", required=True, help="Path to the input Excel file")
    parser.add_argument("--output", required=True, help="Path to save the updated Excel file")

    args = parser.parse_args()

    extract_isbns(args.images, args.excel, args.output)


📊 Sample Data
| ID     | ISBN |
| ------ | ---- |
| Cew34  |      |
| THR007 |      |


🖼️ images/
Cew34.jpg → contains text ISBN 978-0-393-04002-9

THR007.jpg → contains no ISBN
