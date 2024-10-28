# rishi-pawar-wasserstoff-AiInternTask
PDF Processing Pipeline with MongoDB Integration

A comprehensive Python-based pipeline designed to automate the downloading, processing, and updating of PDF documents in MongoDB. This project provides a robust solution for handling bulk PDF processing, including text extraction, summarization, keyword extraction, and MongoDB updates.
Table of Contents

Overview
Features
Technologies Used
Getting Started
Prerequisites
Installation
Usage
Project Structure
Example Workflow
Future Enhancements
License
Contact
Overview

This project is a complete PDF processing pipeline that:
Connects to MongoDB to retrieve document URLs marked as pending.
Downloads PDF files from the retrieved URLs and saves them locally.
Extracts text, generates summaries, and identifies key terms from the PDFs.
Updates MongoDB with the extracted data, marking each document as processed.
Features

Automated PDF Download: Fetches and saves PDFs from URLs stored in MongoDB.
Text Extraction: Utilizes pdfminer.six for efficient PDF text extraction.
Summarization: Generates a summary of each document’s content (first 500 characters as a placeholder).
Keyword Extraction: Extracts important keywords using TF-IDF.
Database Update: Updates MongoDB with extracted summaries, keywords, and status changes.
Multithreading: Concurrent processing of multiple documents for improved performance.
Technologies Used

Python: Core programming language.
MongoDB: Database to store PDF metadata and processed information.
pdfminer.six: Library for PDF text extraction.
scikit-learn: Used for TF-IDF-based keyword extraction.
Concurrent Futures: For multithreaded processing.
Getting Started

Prerequisites
Python 3.x
MongoDB installed locally or available as a cloud service.
Installation
Clone this repository:
bash
Copy code
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
Install required Python packages:
bash
Copy code
pip install pymongo pdfminer.six dnspython scikit-learn
Set up MongoDB:
Create a MongoDB database named pdf_database and a collection named pdf_documents.
Make sure MongoDB is accessible and running.
Usage

MongoDB Configuration
Edit the MongoDB Connection URI:
In the script, replace "your_mongodb_uri" with your actual MongoDB connection string:
python
Copy code
client = MongoClient("your_mongodb_uri")
db = client['pdf_database']
collection = db['pdf_documents']
Load Initial PDF Metadata:
If you have a JSON file with PDF metadata (e.g., names, URLs, and initial status), load it into MongoDB to mark documents as "pending" for processing.
Run the Script:
Run the main script to start processing:
bash
Copy code
python your_script.py
This will:
Connect to MongoDB and find all documents marked as "pending".
Download, parse, summarize, and update each PDF document.
Mark each document as "processed" in MongoDB.
Project Structure

download_pdf(url, filename): Downloads a PDF from a URL and saves it locally.
parse_pdf(filepath): Extracts text from the downloaded PDF.
summarize_text(text): Generates a summary (first 500 characters) of the text.
extract_keywords(text, num_keywords=5): Extracts keywords using TF-IDF.
update_mongodb_with_summary_and_keywords(doc_id, summary, keywords): Updates MongoDB with summary, keywords, and sets status to "processed".
process_document(doc): Manages downloading, text extraction, summarization, keyword extraction, and updating for a single document.
start_processing(): Initiates concurrent processing of all "pending" documents.
Example Workflow

MongoDB Document Structure
The MongoDB pdf_documents collection stores each PDF with the following fields:
json
Copy code
{
  "_id": "ObjectId",
  "name": "pdf_name",
  "url": "pdf_url",
  "status": "pending"
}
After processing, each document will include:
summary: Text summary of the PDF.
keywords: Extracted keywords.
status: Changed from "pending" to "processed".
Sample Output
After running the script, MongoDB will store the processed data as follows:
json
Copy code
{
  "_id": "ObjectId",
  "name": "pdf_name",
  "url": "pdf_url",
  "summary": "Extracted summary text...",
  "keywords": ["keyword1", "keyword2", "keyword3"],
  "status": "processed"
}
Logs
The script logs each processing step, including download success/failure, extraction results, and MongoDB update status.
Future Enhancements

Advanced Summarization: Implement machine learning models for better summaries.
Enhanced Keyword Extraction: Use NLP libraries like spaCy for improved keyword extraction.
Detailed Error Handling: Add more robust error-handling mechanisms.
Improved Logging: Add logging for better tracking and debugging.
