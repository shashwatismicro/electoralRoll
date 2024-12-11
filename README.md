# Electoral Roll Downloader Automation
A Python project using Selenium to automate the download of electoral rolls from the Election Commission of India website. The script navigates the portal, selects state, district, and constituency, and handles downloads efficiently. Requires Python, Selenium, and a compatible WebDriver.
Here's a draft for your `README.md` file:

---

# Voter Electoral Roll Automation

This project automates the process of downloading electoral roll PDFs from the Election Commission of India website. The tool is implemented using Selenium WebDriver and includes two different approaches for handling CAPTCHA:

1. **`main.py`:** In this version, the user manually solves the CAPTCHA, and the rest of the PDF download process is fully automated.
2. **`electoralRoll`:** In this version, Tesseract OCR is used to attempt automatic solving of the CAPTCHA image. However, this method is not very reliable, and CAPTCHA recognition sometimes fails. Additionally, an attempt was made to integrate the 2captcha API for solving CAPTCHAs automatically, but it did not work as expected, so Tesseract was used as a fallback.

## Installation

1. Clone this repository:

```bash
git clone https://github.com/shashwatismicro/electoralRoll
cd /usr/local/bin
```
https://github.com/shashwatismicro/electoralRoll
2. Install the required Python packages:

```bash
pip install -r requirements.txt
```

3. Install Tesseract OCR:
   - For Linux:
     ```bash
     sudo apt-get install tesseract-ocr
     ```
   - For Windows, download from [Tesseract OCR GitHub](https://github.com/tesseract-ocr/tesseract).

## Usage

### `main.py`

This file requires the user to manually solve the CAPTCHA that appears during the PDF download process. After solving the CAPTCHA, the script will proceed with downloading the PDFs automatically.

To run the script:

```bash
python main.py
```

### `electoralRoll`

This file uses Tesseract OCR to automatically attempt CAPTCHA solving. It works inconsistently, as Tesseract sometimes fails to correctly recognize the CAPTCHA text. You can run this version to attempt automatic CAPTCHA solving, but manual intervention may still be required in some cases.

To run the script:

```bash
python electoralRoll
```

### Note on CAPTCHA Handling

- The CAPTCHA recognition using Tesseract OCR is not very efficient and can sometimes fail. It was attempted to integrate the 2captcha API, but it didn't work as expected. Thus, this project uses Tesseract as a fallback solution.
