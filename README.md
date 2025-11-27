# File-Archive Overlap Finder

## 💡 Core Philosophy

The **File-Archive Overlap Finder** is a powerful desktop tool designed to solve the critical problem of identifying and analyzing content reuse across large, unstructured document archives, using a single reference file as the benchmark. It operates on two fundamental principles:

1.  **Efficiency Through Layered Analysis:** The tool avoids slow, byte-by-byte comparison by first applying a fast, macro-level filter (**Jaccard Similarity**) to narrow down potential matches. Only the most promising pairs are subjected to granular, CPU-intensive scrutiny.
2.  **Structural Integrity Check:** The Advanced Structural Comparison feature moves beyond simple keyword spotting. It analyzes the **flow and structure** of content by segmenting documents into logical, page-aware text chunks (paragraphs). This method accurately identifies identical or near-identical blocks of text—the hallmarks of structural reuse—regardless of explicit section titles or minor formatting variations.

---

## 🚀 Key Features

### Interface Overview

The application interface is divided into four main areas:

1.  **Header:** Folder selection, status path, and CSV export button.
2.  **Search Controls:** Contains the two search modes (Keyword and **Overlap Finder**).
3.  **Status & Progress:** Shows the current scanning progress and file being processed.
4.  **Results Pane:** A split view where the top section displays the results table (`Treeview`) and the bottom section shows the `Instant Preview` of the selected file.

---

## ⚙️ Detailed User Guide

### 1. Installation and Setup

The File-Archive Content Comparator (FACC) requires Python and several specialized external libraries for document parsing and multi-processing.

1.  **Install Python:** Ensure you have Python 3.7+ installed on your system.
2.  **Install Dependencies:** All necessary packages are listed in `requirements.txt`. Install them using pip:
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the Application:** Ensure the main Python code is saved as `main.py` and run the program from your terminal:
    ```bash
    python main.py
    ```

### 2. Initializing the Archive

1.  **Select Archive:** Once the GUI launches, click the **"Select Archive"** button in the top right corner.
2.  **Choose Corpus:** Choose the root folder containing all the documents you wish to analyze (the *Corpus*). The path will be displayed next to the button, confirming the archive location.

### 3. Keyword Search Workflow

Use this mode for rapid search of specific terms across the entire archive.

1.  **Input Query:** In the **Keyword Search** panel, enter the text you are looking for.
2.  **Select Mode:**
    * **Standard Search (Default):** Finds exact keyword matches (case-insensitive, ignoring minor internal spacing).
    * **Regex Search:** Check the **"Regex"** box to enable regular expression matching for complex pattern searching (e.g., finding specific email formats or dates).
3.  **Start Search:** Click the **"Search"** button.
4.  **Analyze Results:** The results table will populate with matching files, showing the file name, directory, a snippet of the context where the match occurred, and the full path.

### 4. Overlap Finder Workflow (File-to-Archive Comparison)

Use this mode to find documents that are conceptually similar to a specific *Reference File* (the source).

1.  **Select Reference File:** Click the **"Find Similar..."** button in the **Overlap Finder** panel. A dialog will open, prompting you to select the *Reference File* (the document you want to compare the archive against).
2.  **Start Scan:** The application immediately begins scanning all other files in the corpus against the token set of your reference file.
3.  **Analyze Results:**
    * The results table will show files with an overlap score above $5.0\%$.
    * The table is automatically sorted by **Score (%) Descending**, placing the most similar documents at the top.
    * This score represents the percentage of unique words (tokens) shared between the reference file and the target file. 

[Image of Jaccard Similarity Calculation]


### 5. Result Analysis and Advanced Inspection

1.  **Instant Preview:** Click any row in the results table. The document's full text content will immediately load into the **Instant Preview** pane below, allowing for quick verification without opening the file.
2.  **Open File (Double-Click):** Double-click a row in the results table to open the file using your system's default application. If the file is a PDF and the search provided a page number, it will attempt to open the PDF directly to that page.

### 6. Advanced Structural Comparison

This is a **secondary analysis** performed on files identified as high-scoring by the **Overlap Finder** Scan.

1.  **Right-Click:** In the results table (after running an **Overlap Finder** Scan), right-click on a high-scoring file (e.g., $40\%+$ overlap).
2.  **Select Inspection:** Choose **"Deep Inspect Structure..."** from the context menu.
3.  **Comparison Window:** A new window opens showing the granular comparison results, chunk-by-chunk:
    * **Page (Ref):** The page number in the Reference File where the chunk starts.
    * **Page (Target):** The best matching page number in the Target File.
    * **Score %:** The structural similarity score (Sequence Matcher ratio) for that specific chunk pair.
    * **Navigation:** **Double-click** any value in the "Page (Ref)" or "Page (Target)" columns to open the corresponding PDF document directly to that page.

### 7. Exporting Results

1.  After any search that yields matches, the **"Export CSV"** button becomes active.
2.  Clicking it will generate a CSV file containing the full result set, including search type, query, file paths, and scores/context, for external logging or analysis.

---

## 📁 Supported File Formats

The tool automatically indexes files with the following extensions:

| Category | File Extensions | Description |
| :--- | :--- | :--- |
| **PDF Documents** | `.pdf` | Requires the `PyMuPDF` (`fitz`) library for fast text extraction. |
| **Word Documents** | `.docx`, `.doc` | Requires the `python-docx` library (primarily supports `.docx`). |
| **Text/Code Files** | `.txt`, `.py`, `.c`, `.cpp`, `.h`, `.java`, `.md`, `.json`, `.xml`, `.csv` | Generic text parsing with UTF-8 encoding support. |

---
*Made by [Contributor Name/Entity]*