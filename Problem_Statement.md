# 📄 Problem Statement

## **Context**

A library dataset contains approximately **3,000 book images**. These images include:

* **Book covers** (front pages)
* Some images **do not have ISBN numbers**
* ISBN numbers may appear in different positions on the image (usually near the word **"ISBN"**)

Additionally:

* An **Excel file** contains two columns:

  * `ID` → Unique identifier for each book
  * `ISBN` → Currently empty or partially filled

* The **images folder** contains files named with the same `ID` as in the Excel file (e.g., `Cew34.jpg` corresponds to `ID = Cew34`).



## **Problem**

We need to:

* Extract **ISBN numbers** (10 to 13 digits) from the corresponding book images.
* **Map each extracted ISBN to the correct `ID`** in the Excel file without altering the order of rows.
* Handle cases where:

  * Images are **corrupted** or **unreadable**
  * ISBN is **not present** in the image (fill as `"NULL"` in the Excel file)

---

## **Constraints & Requirements**

* ISBN format:

  * Must contain only **digits**
  * Length: **10 or 13 digits**
  * Remove all **spaces, hyphens, or special characters**
* Final ISBN should be stored as a **string** in Excel cells, in the format:

  ```
  "1234567890"
  ```
* No reordering of the original Excel rows.

---

## **Input**

* **Excel File**:

  ```
  ID        | ISBN
  Cew34     |
  THR007    |
  ```
* **Images Folder**:

  ```
  /images/img/
      Cew34.jpg
      THR007.jpg
  ```

---

## **Output**

Updated Excel file with ISBN numbers:

```
ID        | ISBN
Cew34     | "126897293820"
THR007    | NULL
```
