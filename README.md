# Kompass-India

# Email Verification Tool

A comprehensive Python application for bulk email verification with a user-friendly GUI interface. This tool processes contact data, generates email variations, and verifies email addresses via SMTP.

![Email Verification Tool GUI](https://github.com/Vishlu/Kompass-India/blob/76f9a65e8ce02c031e2d672fe524a11555a9f55c/Email%20Verification%20Software-20250515T150434Z-1-001/Email%20Verification%20Software/Screenshot%20(85).png)

## 📋 Features

### 1. **Email Variation Generation**
- Generates multiple email format variations from contact data
- Supports formats like `firstname.lastname@domain.com` and `firstname@domain.com`
- Handles missing data gracefully with default values

### 2. **Bulk Email Verification**
- Validates email syntax using regex patterns
- Checks DNS MX records for domain validity
- Performs SMTP verification to determine email activity
- Processes emails in batches to manage large datasets

### 3. **User-Friendly GUI**
- Clean, dark-themed interface
- Progress tracking with real-time updates
- Batch processing with intermediate file saving
- Easy file selection and output configuration

### 4. **Data Management**
- Reads from and writes to Excel files (.xlsx)
- Maintains original data structure with verification results
- Supports optional `_id` field for data tracking
- Preserves contact information (name, website, LinkedIn, etc.)

## 🚀 Installation

### Prerequisites
- Python 3.7+
- Required Python packages

### Install Dependencies
```bash
pip install pandas openpyxl dnspython

## 📁 Input File Format

The tool expects an Excel file with the following columns:

| Column Name | Description | Required |
|-------------|-------------|----------|
| _id | Unique identifier | Optional |
| firstName | Contact's first name | Yes |
| lastname | Contact's last name | Yes |
| webSites | Domain/website for email generation | Yes |
| salutation | Contact title/prefix | No |
| functionName | Job function/role | No |
| functionCode | Function code | No |
| linkedinprofile | LinkedIn profile URL | No |

**Note:** Required fields will use defaults if missing (`'unknown'` for firstName/webSites, empty string for others).

## 🛠️ Usage

### Running the Application
```bash
python email_verification.py

Step-by-Step Process
Launch the Application

Run the script to open the GUI window

Application title: "Bulk Email Verification"

Upload Input File

Click "Upload Excel File" button

Select your input Excel file containing contact data

Select Output Directory

Click "Select Output Directory" button

Choose folder where results will be saved

Specify Output Filename

Enter desired name for final output file (without extension)

Start Processing

Click "Submit" button

Monitor progress in the status window

Processing Flow
The tool follows this workflow:

Generate Email Variations - Creates possible email formats for each contact

Stack Variations - Organizes all variations into single-column format

Verify Emails - Checks each email address for validity and activity

Batch Processing - Saves intermediate results every 100 emails

Final Compilation - Combines all batches into final output file

📊 Output Files

Generated Files:
Batch Files (e.g., Batch_1.xlsx, Batch_2.xlsx)

Intermediate results saved every 100 emails

Contains verification status and reasons

Final Results File (e.g., [your_filename].xlsx)

Complete consolidated results

Same format as input with additional columns:

Email: The verified email address

Status: "Active" or "Inactive"

Reason: Detailed verification result

Output Columns:
All original input columns

Email: The email address that was verified

Status: Verification status ("Active"/"Inactive")

Reason: Explanation of verification result

⚙️ Technical Details

Email Verification Process
Syntax Validation - Regex pattern matching for valid email format

Domain Validation - DNS MX record lookup

SMTP Verification - SMTP server communication to check mailbox existence

Rate Limiting - Built-in delays to prevent server blocking

Error Handling
Invalid email formats are marked as "Inactive"

Missing MX records are properly handled

Network timeouts and DNS failures are caught and logged

Missing input data uses sensible defaults

⚠️ Limitations & Considerations
SMTP Server Policies

Some email servers may block verification attempts

Results depend on individual server configurations

Rate Limiting

Built-in 3-second delay between verifications

May affect processing speed for large datasets

Data Requirements

At least first name and website are required

Last name is optional but affects email variations

File Formats

Input and output are Excel (.xlsx) files only

Uses openpyxl engine for Excel operations

🛡️ Privacy & Security

No email data is stored permanently

Temporary files are automatically cleaned up

Verification process is transparent and logged

No external data transmission beyond SMTP verification

📝 Troubleshooting

Common Issues:
"Input file must contain mandatory fields" error

Ensure your Excel file has required columns: firstName, lastname, webSites

Check column spelling and capitalization

Slow processing speed

The tool includes 3-second delays between email checks

This prevents being blocked by email servers

Consider reducing batch size for testing

"Domain does not have MX records" errors

Some domains may not have properly configured MX records

This is correctly identified as an invalid email

Memory issues with large files

Tool processes in batches of 100 emails

Intermediate files are saved to disk

Consider splitting very large files (>10,000 rows)

🔧 Customization
Modify Email Variations
Edit the generate_email_variations() function to add different email formats:

python
# Current formats:
# 1. firstname.lastname@domain.com
# 2. firstname@domain.com
Adjust Verification Settings
Modify these parameters as needed:

sleep(3) - Delay between email checks

batch_size = 100 - Number of emails per batch

timeout=10 - SMTP connection timeout

📄 License

This tool is provided as-is for email verification purposes. Users are responsible for complying with applicable laws and email service terms of use.

🤝 Contributing

Feel free to fork and modify this tool for your specific needs. Suggested improvements:

Additional email format variations

Parallel processing for faster verification

Support for more input formats (CSV, JSON)

Enhanced error handling and retry logic

