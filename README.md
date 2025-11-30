 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
index 37d093b186ec3116bd3dc9aadfd8fb0aef247238..76a24494f21730d3aa6a5e53d9bfeb503dab68bb 100644
--- a/README.md
+++ b/README.md
@@ -1,60 +1,59 @@
 # Electoral Roll Downloader Automation
-A Python project using Selenium to automate the download of electoral rolls from the Election Commission of India website. The script navigates the portal, selects state, district, and constituency, and handles downloads efficiently. Requires Python, Selenium, and a compatible WebDriver.
-Here's a draft for your `README.md` file:
 
----
+This project automates downloading electoral roll PDFs from the Election Commission of India website using Selenium WebDriver. It includes two entry points: one that relies on **manual** CAPTCHA solving and another that attempts to solve the CAPTCHA automatically with **Tesseract OCR**.
 
-# Voter Electoral Roll Automation
+> If you only need the short version: clone, create a virtualenv, install `requirements.txt`, install a WebDriver that matches your browser, ensure `tesseract` is on your `PATH`, then run `python main.py` (manual CAPTCHA) or `python electoralRoll` (OCR attempt).
 
-This project automates the process of downloading electoral roll PDFs from the Election Commission of India website. The tool is implemented using Selenium WebDriver and includes two different approaches for handling CAPTCHA:
+## Quickstart (after cloning)
 
-1. **`main.py`:** In this version, the user manually solves the CAPTCHA, and the rest of the PDF download process is fully automated.
-2. **`electoralRoll`:** In this version, Tesseract OCR is used to attempt automatic solving of the CAPTCHA image. However, this method is not very reliable, and CAPTCHA recognition sometimes fails. Additionally, an attempt was made to integrate the 2captcha API for solving CAPTCHAs automatically, but it did not work as expected, so Tesseract was used as a fallback.
+1. **Clone and enter the project**
+   ```bash
+   git clone https://github.com/shashwatismicro/electoralRoll
+   cd electoralRoll
+   ```
 
-## Installation
+2. **Create and activate a virtual environment (recommended)**
+   ```bash
+   python3 -m venv .venv
+   source .venv/bin/activate
+   ```
 
-1. Clone this repository:
+3. **Install Python dependencies**
+   ```bash
+   pip install -r requirements.txt
+   ```
 
-```bash
-git clone https://github.com/shashwatismicro/electoralRoll
-cd /usr/local/bin
-```
-https://github.com/shashwatismicro/electoralRoll
-2. Install the required Python packages:
+4. **Install a browser WebDriver that matches your browser version**
+   - **Google Chrome**: download the matching [ChromeDriver](https://googlechromelabs.github.io/chrome-for-testing/#stable) and place the binary on your `PATH` (e.g., `/usr/local/bin/chromedriver`).
+   - **Mozilla Firefox**: download the matching [geckodriver](https://github.com/mozilla/geckodriver/releases) and place it on your `PATH`.
 
-```bash
-pip install -r requirements.txt
-```
-
-3. Install Tesseract OCR:
-   - For Linux:
+5. **Install and verify Tesseract (for the OCR flow)**
+   - Linux (Debian/Ubuntu): `sudo apt-get install tesseract-ocr`
+   - macOS (Homebrew): `brew install tesseract`
+   - Verify installation:
      ```bash
-     sudo apt-get install tesseract-ocr
+     tesseract --version
      ```
-   - For Windows, download from [Tesseract OCR GitHub](https://github.com/tesseract-ocr/tesseract).
-
-## Usage
-
-### `main.py`
-
-This file requires the user to manually solve the CAPTCHA that appears during the PDF download process. After solving the CAPTCHA, the script will proceed with downloading the PDFs automatically.
-
-To run the script:
-
-```bash
-python main.py
-```
 
-### `electoralRoll`
-
-This file uses Tesseract OCR to automatically attempt CAPTCHA solving. It works inconsistently, as Tesseract sometimes fails to correctly recognize the CAPTCHA text. You can run this version to attempt automatic CAPTCHA solving, but manual intervention may still be required in some cases.
+6. **Run the automation**
+   - Manual CAPTCHA flow (waits for you to type the CAPTCHA):
+     ```bash
+     python main.py
+     ```
+   - OCR CAPTCHA attempt (tries to solve automatically with Tesseract):
+     ```bash
+     python electoralRoll
+     ```
 
-To run the script:
+## Usage notes
 
-```bash
-python electoralRoll
-```
+- OCR-based solving is inherently unreliable; expect occasional failures and be ready to retry.
+- Keep your browser and WebDriver versions aligned to avoid Selenium errors (e.g., `SessionNotCreatedException`).
+- If you prefer an external CAPTCHA-solving service (e.g., 2Captcha), add your API credentials and replace the Tesseract step accordingly.
+- Run inside the virtual environment for consistent dependency versions.
 
-### Note on CAPTCHA Handling
+## Troubleshooting checklist
 
-- The CAPTCHA recognition using Tesseract OCR is not very efficient and can sometimes fail. It was attempted to integrate the 2captcha API, but it didn't work as expected. Thus, this project uses Tesseract as a fallback solution.
+- `selenium.common.exceptions.SessionNotCreatedException`: update Chrome/Firefox or download a matching WebDriver.
+- `pytesseract.TesseractNotFoundError`: ensure `tesseract` is installed and accessible on your `PATH`.
+- `ModuleNotFoundError: No module named 'selenium'`: (re)run `pip install -r requirements.txt` inside the activated virtual environment.
 
EOF
)
