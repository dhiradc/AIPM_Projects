# Product Requirements Document: AI-Powered Downtime Notification Mailing System

## 1. Introduction/Overview

The AI-Powered Downtime Notification Mailing System automates the generation and distribution of weekly system downtime notification emails. This system informs groups of users about system downtimes so that everyone can manage their tasks on the systems effectively. Currently, manual weekly email drafting is time-consuming and prone to inconsistencies. This system reads downtime data from an Excel file, processes it based on date ranges, matches standardized descriptions, and automatically generates formatted emails that are pushed to a group mailbox draft folder.

The system also handles last-minute downtime entries that may be missing from the Excel file. When such entries are received via email and saved in the same SharePoint folder as the Excel file, the AI system uses Natural Language Processing (NLP) techniques to extract downtime information directly from the email body and includes it in the draft email table. No modifications are made to the Excel file.

**Problem Statement:** Manual weekly email drafting for downtime notifications is time-consuming and requires significant manual effort to ensure accuracy and consistency. Additionally, last-minute downtime entries may be missed if they are not added to the Excel file in time.

**Goal:** Automate the entire process of reading downtime data from Excel and emails, formatting it appropriately, and generating weekly downtime notification emails that are ready for review and sending. The system will automatically extract last-minute downtime information from emails using NLP and include it directly in the draft email without modifying the Excel file.

## 2. Goals

1. Automate the generation of weekly downtime notification emails every Monday
2. Reduce manual effort required for drafting downtime emails by 100%
3. Ensure consistent email formatting and content standardization
4. Automatically filter and display downtime items for the correct date range (Monday to next-to-next Sunday)
5. Provide visual distinction between current week and next week items through color coding
6. Automatically match application combinations to standardized descriptions
7. Generate emails that are ready for review in the group mailbox draft folder
8. Automatically extract last-minute downtime entries from emails stored in the SharePoint folder using NLP techniques
9. Include last-minute downtime entries directly in the draft email table without modifying the Excel file

## 3. User Stories

1. **As an office assistant**, I want the system to automatically generate downtime notification emails every Monday so that I don't have to manually draft them each week.

2. **As an office assistant**, I want to fill out a mailing list in a text file so that the system knows who should receive the downtime notifications.

3. **As a system administrator**, I want the system to run automatically every Monday so that I don't need to manually trigger it each week.

4. **As a system administrator**, I want the system to continuously monitor and process until manually aborted so that I have control over when it stops.

5. **As an email recipient**, I want to receive consistently formatted downtime notification emails so that I can easily understand what systems will be down and when, allowing me to manage my tasks effectively.

6. **As a senior leadership member**, I want to be notified when no email is received so that I can follow up with operations managers to understand the reason.

7. **As an operations manager**, I want to be able to check the system locations (Excel file, standardized text file, mailing list) when issues occur so that I can identify and resolve problems.

8. **As a Release Support group member**, I want last-minute downtime entries saved as email files in the SharePoint folder so that the system can automatically include them in the weekly notification email.

9. **As an email recipient**, I want to receive downtime notifications that include both Excel data and last-minute entries from emails so that I have complete and up-to-date information about all system downtimes.

## 4. Functional Requirements

### 4.1 Excel File Reading
1. The system must read from a Downtime Notification Excel file located at a shared SharePoint location accessible to the entire team.
2. The system must read date information from column B of the Excel file.
3. The system must read application/system downtime indicators from columns I, J, K, L, and M, where an "X" mark indicates that application/system will experience downtime on that date.
4. The system must read existing standard descriptions from column N of the Excel file.
5. The system must NOT modify or write to the Excel file under any circumstances.

### 4.2 Date Range Processing
6. The system must calculate the date range starting from the current Monday (or the most recent Monday if today is not Monday).
7. The system must calculate the end date as the next-to-next Sunday (15 days from the start Monday).
8. The system must filter Excel rows to include only items where the date in column B falls within the calculated date range (inclusive of start and end dates).
9. The system must process and generate emails only on Mondays.

### 4.3 Table Display and Color Coding
10. The system must display filtered items in a table format.
11. The system must color-code items from the current week (Monday to Sunday of the current week) with light green background color.
12. The system must color-code items from the next week (Monday to Sunday of the following week) with deep green background color.
13. The system must apply the same color coding rules to last-minute entries extracted from emails.

### 4.4 Standardized Text Matching
15. The system must read standardized text descriptions from a plain text file located at a shared point location.
16. The system must perform exact matching of the combination of columns I, J, K, L, M (application/system selections) against the standardized text file.
17. The system must determine the appropriate column N entry (standard description) based on the exact match of columns I, J, K, L, M.
18. The system must flag items for review when no exact match is found for the combination of columns I, J, K, L, M.
19. The system must use the matched standardized description to populate or update column N for each row.
20. The system must apply the same standardized text matching logic to application/system combinations extracted from emails.

### 4.5 Mailing List Management
21. The system must read email addresses from a separate text file maintained by the product support assistant.
22. The system must read the group mailbox email address from the same text file that contains the recipient email addresses.
23. The system must support multiple email addresses in the mailing list text file.

### 4.6 Email Generation
24. The system must generate an email subject line in the format: "Updates from [Month Day Year] to [Month Day Year]" where the dates are the start Monday and end Sunday (next-to-next Sunday).
25. The system must format the email body as a table containing all items within the date range.
26. The system must include all filtered items from Excel (within the date range) in the email body table.
27. The system must include all last-minute downtime entries extracted from emails (within the date range) in the email body table.
28. The system must preserve the color coding (light green for current week, deep green for next week) in the email table for both Excel items and email-extracted items.
29. The system must include application/system information (from columns I, J, K, L, M or extracted from emails) and standardized descriptions (from column N or extracted from emails) in the email table.
30. The system must merge Excel data and email-extracted data into a single unified table in the draft email.

### 4.7 Email Delivery
31. The system must push the generated email to the draft folder of the group email box specified in the mailing list text file.
32. The system must ensure the email is formatted correctly for the email client to display the table and color coding.

### 4.8 Last-Minute Entry Processing (Email Reading and NLP Extraction)
33. The system must read email files from the same SharePoint folder location where the Excel file is stored.
34. The system must identify email files (e.g., .eml, .msg, or other email file formats) in the SharePoint folder.
35. The system must automatically use Natural Language Processing (NLP) services to extract downtime information from email body content with zero manual intervention.
36. The system must automatically extract information equivalent to standard Downtime Excel columns B through N from email content using NLP, including:
    - Date information (equivalent to column B)
    - Application/system indicators (equivalent to columns I, J, K, L, M - identifying which systems/applications are mentioned)
    - Standard descriptions (equivalent to column N)
37. The system must automatically parse email body text to identify:
    - Downtime dates mentioned in natural language
    - System/application names that will experience downtime
    - Downtime duration, time windows, or schedules
    - Descriptions of the downtime reason or impact
38. The system must automatically match extracted application/system names against the standardized text file to determine the appropriate standard description (column N equivalent).
39. The system must automatically filter extracted downtime entries to include only those within the date range (Monday to next-to-next Sunday).
40. The system must automatically include all successfully extracted downtime entries directly in the email table body alongside Excel entries, with no manual work or intervention required at any stage.
41. The system must automatically combine Excel data and email-extracted data into a single unified table for the draft email.
42. The system must NOT modify the Excel file with information extracted from emails.
43. The entire process of reading emails, extracting information via NLP, and including entries in the email table must be fully automated with no manual steps.

### 4.9 Automation and Scheduling
44. The system must run automatically every Monday.
45. The system must run continuously until manually aborted by a system administrator.
46. The system must be capable of running in the background without user intervention.
47. The system must scan the SharePoint folder for email files during the weekly email generation process.

### 4.10 Error Handling and Escalation
48. The system must take no action if the Excel file is missing or corrupted (no email generation, no alerts).
49. The system must take no action if the standardized text file is missing or inaccessible (no email generation, no alerts).
50. The system must take no action if the email service is unavailable (no email generation, no alerts).
51. The system must take no action and generate no email if no items are found within the date range (from both Excel and emails).
52. When no email is received by senior leadership, they must be able to contact operations managers via online meeting to inquire about the reason.
53. Operations managers must be able to personally check the required locations (Excel file location, standardized text file location, mailing list file location, SharePoint folder for email files) and confirm the reason for no email being received.
54. The system must take no action if it cannot extract downtime information from email files using NLP (no alerts, no automatic processing, but continue with Excel data if available).
55. The system must continue processing Excel data even if email extraction fails, and generate the draft email with available Excel data only.

## 5. Non-Goals (Out of Scope)

1. **Email Sending:** The system will NOT automatically send emails. It only creates drafts in the draft folder for manual review and sending.
2. **Excel File Editing:** The system will NOT modify the Excel file under any circumstances. All last-minute entries from emails are added directly to the draft email table only.
3. **User Interface:** The system does NOT require a graphical user interface. It runs as an automated background process.
4. **Real-time Monitoring Dashboard:** The system does NOT include a dashboard or monitoring interface for tracking email generation status.
5. **Email Template Customization:** The system does NOT allow users to customize email templates through a UI. Template structure is fixed.
6. **Historical Email Tracking:** The system does NOT track or store history of previously generated emails.
7. **Multi-language Support:** The system does NOT support multiple languages. It operates in a single language.
8. **Notification System:** The system does NOT send alerts or notifications when errors occur. Error handling follows the "no action" approach.
9. **Automatic Retry Logic:** The system does NOT automatically retry failed operations. It follows the "no action" approach for errors.
10. **Integration with Other Systems:** The system does NOT integrate with project management tools, calendars, or other external systems beyond the specified Excel file, text files, email files in SharePoint, and email service.
11. **Email Inbox Monitoring:** The system does NOT monitor email inboxes. It only reads email files stored in the SharePoint folder.
12. **Manual Email Processing:** The system does NOT require any manual intervention for email processing, extraction, or inclusion in the email table. NLP extraction and table inclusion are 100% automated with zero manual work.

## 6. Design Considerations

### 6.1 Table Formatting
- The email table must be HTML-formatted to support color coding in email clients.
- Table columns should include: Date, Applications (I, J, K, L, M indicators), and Description (from column N).
- Color coding must be applied using HTML/CSS background colors:
  - Light green: `#90EE90` or equivalent for current week items
  - Deep green: `#006400` or equivalent for next week items
  - Default: No background color for other items

### 6.2 Email Format
- The email must be formatted as HTML to support table rendering and color coding.
- The email body should have a clear structure: subject line, introductory text (optional), table of items, closing (optional).

### 6.3 File Format Specifications
- **Excel File:** Must be in a format readable by standard Excel libraries (.xlsx, .xls). Read-only access required.
- **Email Files:** Must support common email file formats (e.g., .eml, .msg, .mbox) stored in the SharePoint folder. The system must be able to parse email body content from these files.
- **Standardized Text File:** Plain text format with a structure that allows matching of I, J, K, L, M combinations to N descriptions.
- **Mailing List File:** Plain text file with one email address per line, and the group mailbox address clearly identified (e.g., on the first line or with a specific marker).

### 6.4 NLP Processing Requirements
- The system must automatically use NLP services/techniques to extract structured downtime information from unstructured email text with no manual intervention.
- NLP extraction must automatically identify:
  - Dates mentioned in various formats (e.g., "Monday, January 15", "1/15/2024", "next Monday")
  - System/application names (matching against known systems or patterns)
  - Time windows or durations
  - Downtime descriptions and reasons
- The system must handle variations in email formatting, language style, and information presentation automatically.
- Extracted information must be automatically normalized to match the Excel data format (columns B through N equivalent).
- All extracted entries must be automatically included in the email table body without any manual review or approval steps.

## 7. Technical Considerations

1. **Excel File Processing:** The system must use a reliable Excel reading library (e.g., openpyxl for Python, Apache POI for Java) that can handle .xlsx and .xls formats. Read-only access is required.

2. **SharePoint Integration:** The system must be able to access files from a SharePoint location. This may require:
   - SharePoint API integration
   - Authentication credentials
   - Network access to SharePoint
   - Ability to read both Excel files and email files from the same folder location

3. **Email Service Integration:** The system must integrate with the email service provider (e.g., Microsoft Exchange, Office 365, Gmail API, SMTP) to:
   - Push emails to the draft folder (requires authentication credentials for the group mailbox and permissions to create drafts)
   - Read email files (.eml, .msg, etc.) from the SharePoint folder location

4. **Date Calculation Logic:** The system must implement robust date calculation logic to:
   - Determine the current or most recent Monday
   - Calculate the next-to-next Sunday (15 days from Monday)
   - Handle timezone considerations if applicable
   - Account for week boundaries correctly

5. **Text Matching Algorithm:** The system must implement exact matching logic that:
   - Reads the standardized text file
   - Parses the file structure to extract I, J, K, L, M combinations and corresponding N descriptions
   - Performs exact string matching (case-sensitive or case-insensitive as specified)
   - Handles flagging when no match is found

6. **NLP-Based Email Content Extraction:** The system must implement fully automated Natural Language Processing (NLP) services/techniques to:
   - Automatically parse email body text from email files stored in SharePoint
   - Automatically extract date information from natural language (e.g., "Monday, January 15", "next week", "1/15/2024")
   - Automatically identify application/system names mentioned in emails using named entity recognition or pattern matching
   - Automatically extract downtime descriptions, reasons, and impact information from email text
   - Automatically map extracted information to equivalent Excel columns B through N format
   - Automatically handle various email formats, structures, and writing styles
   - Use NLP libraries or services (e.g., spaCy, NLTK, Transformers, or cloud NLP APIs) for automated text processing
   - Automatically normalize extracted dates to match Excel date format
   - Automatically match extracted system/application names against the standardized text file
   - Automatically include all extracted entries in the email table body with no manual intervention

7. **Email File Parsing:** The system must implement email file parsing to:
   - Read email files (.eml, .msg, .mbox, etc.) from the SharePoint folder
   - Extract email body content (handling both plain text and HTML emails)
   - Parse email metadata if needed (sender, subject, date received)
   - Handle email attachments if they contain relevant downtime information

8. **Scheduling System:** The system must implement a scheduling mechanism (e.g., cron job, Windows Task Scheduler, or a scheduling library) to:
   - Trigger execution every Monday
   - Run continuously until manually aborted
   - Handle system restarts gracefully (resume scheduling after restart)
   - Scan the SharePoint folder for email files during the weekly generation process

8. **Error Handling:** While the system takes "no action" on errors, it should:
   - Log errors for debugging purposes (even if not displayed to users)
   - Handle file access errors gracefully
   - Handle network connectivity issues
   - Handle email service unavailability
   - Handle email parsing and extraction errors gracefully

9. **Data Validation:** The system should validate:
   - Excel file structure (presence of required columns B, I, J, K, L, M, N)
   - Date format in column B
   - Text file formats and structures
   - Email address formats in mailing list
   - Extracted information from emails before including in draft email (date formats, application names, date range filtering)
   - NLP extraction confidence scores (automatically exclude low-confidence extractions or include them with appropriate markers in the email table)

10. **Performance Considerations:** The system should:
   - Process Excel files efficiently, even with large datasets
   - Handle text file matching efficiently
   - Complete email generation within reasonable time limits
   - Process email extraction requests in a timely manner
   - Handle concurrent email monitoring and processing

11. **Security Considerations:** The system must:
    - Securely store authentication credentials for SharePoint and email services
    - Follow security best practices for accessing shared resources
    - Ensure email content does not expose sensitive information inappropriately
    - Implement read-only access to Excel files and email files in SharePoint
    - Secure access to the SharePoint folder containing email files

## 8. Success Metrics

1. **Automation Rate:** 100% of weekly downtime notification emails are generated automatically without manual intervention (target: 52 emails per year, one per Monday).

2. **Time Savings:** Reduce time spent on manual email drafting from X hours per week to 0 hours per week (to be measured based on current baseline).

3. **Accuracy Rate:** 100% of emails contain items within the correct date range (Monday to next-to-next Sunday).

4. **Standardization Rate:** 100% of application/system combinations (I, J, K, L, M) that have matches in the standardized text file are correctly mapped to column N descriptions.

5. **Email Delivery Rate:** 100% of generated emails successfully appear in the group mailbox draft folder (when all prerequisites are met: Excel file exists, standardized text file exists, email service is available, items exist in date range).

6. **System Uptime:** System runs successfully every Monday without manual intervention (target: 95%+ success rate over a quarter).

7. **Flagging Accuracy:** All unmatched application/system combinations are correctly flagged for review (100% accuracy in flagging).

8. **Last-Minute Entry Capture:** 100% of email files containing last-minute downtime entries stored in the SharePoint folder are processed during the weekly email generation.

9. **NLP Extraction Accuracy:** Extracted downtime information from emails matches the standard Excel format (columns B through N equivalent) with 85%+ accuracy for high-confidence extractions.

10. **Email Integration Rate:** 100% of successfully extracted last-minute downtime entries (within date range) are included in the draft email table alongside Excel data.

## 9. Open Questions

1. **Standardized Text File Format:** What is the exact structure/format of the standardized text file? (e.g., CSV, key-value pairs, specific delimiters, line structure)

2. **Mailing List File Format:** What is the exact format of the mailing list text file? How is the group mailbox address distinguished from recipient addresses? (e.g., first line, specific marker, separate section)

3. **SharePoint Authentication:** What authentication method should be used to access the SharePoint location? (e.g., service account, OAuth, API key)

4. **Email Service Provider:** Which email service provider is being used? (e.g., Microsoft Exchange, Office 365, Gmail, other)

5. **Flagged Items Handling:** How should flagged items (no match found) be handled in the email? Should they be included with a special marker, excluded, or placed in a separate section?

6. **Email Table Columns:** What specific columns and information should be displayed in the email table? (e.g., Date, Application names/labels for I/J/K/L/M, Description, other metadata)

7. **Application Column Labels:** What are the names/labels for columns I, J, K, L, M? (e.g., "Application A", "Application B", or specific application names)

8. **Timezone Considerations:** Should the system use a specific timezone for date calculations, or use the server's local timezone?

9. **Manual Abort Mechanism:** How should the system be manually aborted? (e.g., stop command, configuration file flag, process termination)

10. **Logging and Monitoring:** Should the system maintain logs of its operations for troubleshooting, even though it takes "no action" on errors? If yes, where should logs be stored?

11. **Email Body Additional Content:** Should the email body include any introductory text, closing text, or other content beyond the table of items?

12. **Multiple Excel Files:** Should the system process a single Excel file, or could there be multiple Excel files to process?

13. **NLP Library/Service:** Which NLP library or service should be used? (e.g., spaCy, NLTK, Transformers/Hugging Face, cloud NLP APIs like Azure Text Analytics, AWS Comprehend, Google Cloud NLP)

14. **Email File Format:** What email file formats will be stored in the SharePoint folder? (e.g., .eml, .msg, .mbox, or other formats)

15. **Email File Naming Convention:** Is there a specific naming convention for email files in the SharePoint folder? How should the system identify which emails to process?

16. **NLP Extraction Confidence Threshold:** What confidence threshold should be used for automated NLP extraction? Should low-confidence extractions be automatically included in the email with a flag, or automatically excluded entirely? (Note: No manual review process - all decisions must be automated)

17. **Email File Processing:** Should the system process all email files in the folder, or only emails from a specific time period (e.g., emails added since last Monday)?

18. **Email File Cleanup:** Should processed email files be archived, deleted, or left in the SharePoint folder after processing?

19. **Date Extraction from Emails:** How should the system handle ambiguous date references in emails (e.g., "next Monday", "end of week")? Should it use the email's received date as context?

20. **System/Application Name Recognition:** How should the system identify system/application names in emails? Should it use a predefined list, pattern matching, or NLP named entity recognition?

