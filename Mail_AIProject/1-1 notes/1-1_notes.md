# 1:1 Discussion Notes with End User

*Project: AI-Powered Downtime Notification Mailing System* *Date: YYYY-MM-DD* *Stakeholder:
\[End User / SME Name\]* *Interviewer: \[Your Name\]*

------------------------------------------------------------------------

## **Overview of Discussion**

Discussion around requirements for automating weekly downtime notification email generation based on Excel inputs, standardized text mappings, NLP-based email extraction, and automated email draft creation. The system reads downtime data from Excel, processes last-minute entries from emails using NLP, and generates formatted notification emails automatically every Monday.

------------------------------------------------------------------------

## **Open Questions / Pending Clarifications**

### **1. Standardized Text File Format**

-   What is the exact structure/format of the standardized text file?
-   Is it CSV format, key-value pairs, or another format?
-   What are the specific delimiters used?
-   What is the line structure?
-   How are I, J, K, L, M combinations mapped to column N descriptions?

### **2. Mailing List File Format**

-   What is the exact format of the mailing list text file?
-   How is the group mailbox address distinguished from recipient addresses?
-   Is it on the first line, marked with a specific identifier, or in a separate section?
-   What is the format for multiple recipient email addresses?

### **3. SharePoint Authentication**

-   What authentication method should be used to access the SharePoint location?
-   Should we use a service account, OAuth, API key, or another method?
-   What are the access requirements and permissions needed?

### **4. Email Service Provider**

-   Which email service provider is being used?
-   Is it Microsoft Exchange, Office 365, Gmail, or another provider?
-   What API or protocol should be used for pushing emails to the draft folder?

### **5. Flagged Items Handling**

-   How should flagged items (no match found in standardized text file) be handled in the email?
-   Should they be included with a special marker?
-   Should they be excluded entirely?
-   Should they be placed in a separate section of the email?

### **6. Email Table Columns**

-   What specific columns and information should be displayed in the email table?
-   Should it include: Date, Application names/labels for I/J/K/L/M, Description, or other metadata?
-   What is the preferred column order and formatting?

### **7. Application Column Labels**

-   What are the names/labels for columns I, J, K, L, M?
-   Are they generic labels like "Application A", "Application B"?
-   Or are they specific application/system names?
-   What are the exact application/system names represented by each column?

### **8. Timezone Considerations**

-   Should the system use a specific timezone for date calculations?
-   Or should it use the server's local timezone?
-   What timezone should be used for the email date range display?

### **9. Manual Abort Mechanism**

-   How should the system be manually aborted?
-   Should it use a stop command, configuration file flag, or process termination?
-   What is the preferred method for system administrators to stop the process?

### **10. Logging and Monitoring**

-   Should the system maintain logs of its operations for troubleshooting?
-   Even though it takes "no action" on errors, should errors be logged?
-   If yes, where should logs be stored?
-   What level of detail is needed in the logs?

### **11. Email Body Additional Content**

-   Should the email body include any introductory text?
-   Should it include closing text?
-   Should it include any other content beyond the table of items?
-   What is the preferred email structure and tone?

### **12. Multiple Excel Files**

-   Should the system process a single Excel file?
-   Or could there be multiple Excel files to process?
-   If multiple files, how should they be identified and processed?

### **13. NLP Library/Service**

-   Which NLP library or service should be used?
-   Options include: spaCy, NLTK, Transformers/Hugging Face, or cloud NLP APIs (Azure Text Analytics, AWS Comprehend, Google Cloud NLP)?
-   Are there any organizational preferences or constraints?
-   What is the budget consideration for cloud NLP services?

### **14. Email File Format**

-   What email file formats will be stored in the SharePoint folder?
-   Will they be .eml, .msg, .mbox, or other formats?
-   Should the system support multiple formats?

### **15. Email File Naming Convention**

-   Is there a specific naming convention for email files in the SharePoint folder?
-   How should the system identify which emails to process?
-   Should it process all email files or filter by naming pattern?
-   Are there any date-based naming conventions?

### **16. NLP Extraction Confidence Threshold**

-   What confidence threshold should be used for automated NLP extraction?
-   Should low-confidence extractions be automatically included in the email with a flag?
-   Or should they be automatically excluded entirely?
-   Note: No manual review process - all decisions must be automated.

### **17. Email File Processing**

-   Should the system process all email files in the folder?
-   Or only emails from a specific time period (e.g., emails added since last Monday)?
-   How should the system determine which emails are "new" or need processing?

### **18. Email File Cleanup**

-   Should processed email files be archived after processing?
-   Should they be deleted after processing?
-   Or should they be left in the SharePoint folder after processing?
-   What is the preferred lifecycle management for email files?

### **19. Date Extraction from Emails**

-   How should the system handle ambiguous date references in emails (e.g., "next Monday", "end of week")?
-   Should it use the email's received date as context?
-   How should relative dates be resolved to absolute dates?
-   What is the fallback behavior for unclear dates?

### **20. System/Application Name Recognition**

-   How should the system identify system/application names in emails?
-   Should it use a predefined list of known systems/applications?
-   Should it use pattern matching?
-   Or should it use NLP named entity recognition?
-   What is the preferred approach for matching extracted names to columns I, J, K, L, M?

------------------------------------------------------------------------

## **SME Responses (Standard Answers)**

*[To be filled in after discussion with business group]*

------------------------------------------------------------------------

## **Next Steps**

-   Present these questions to the business group.
-   Schedule follow-up discussion to resolve open questions.
-   Update PRD based on responses.
-   Finalize technical requirements and implementation approach.
