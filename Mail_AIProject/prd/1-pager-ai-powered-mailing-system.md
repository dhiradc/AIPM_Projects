# 1-Pager: AI-Powered Mailing System

## Outcome

Currently, operations managers spend significant manual effort creating date-based email campaigns from Excel data. The process requires manual date calculations for a 15-day period, applying visual organization to distinguish between weeks, standardizing category labels, and filling email templates for each item. This workflow is time-consuming, error-prone, and repetitive, often taking hours to complete for campaigns with 50-100 items. The manual nature of this work introduces risks of date calculation errors, inconsistent category terminology, and missed items. By automating this entire workflow, we can reduce manual effort by at least 80%, eliminate calculation errors, ensure consistent terminology through automated standardization, and generate individual email drafts ready for review and sending in under 2 minutes.

**Key Points:**
* Current state: Manual date calculations, template filling, and text standardization consume hours per release
* Problem impact: Error-prone process with inconsistent terminology and potential missed items
* Target outcome: 80% reduction in manual effort, zero date calculation errors, consistent standardization
* Business value: Campaign managers can focus on strategic work instead of repetitive data entry

## Opportunity

The opportunity exists to transform a manual, error-prone process into an automated system that processes Excel files containing task/event items, automatically calculates dates for a 15-day period (from today to the next-to-next Sunday), applies visual color coding to distinguish between weeks, standardizes category labels using mapping files, and generates individual email draft files ready to be sent to predefined email groups. The system addresses a clear pain point where campaign managers must repeatedly perform the same calculations and formatting tasks, with each campaign requiring the same sequence of operations. The standardized nature of the workflow makes it an ideal candidate for automation, and the end users have already validated the requirements through 1:1 sessions, confirming the Excel column structure, template placeholders, mapping formats, and output specifications. The opportunity is particularly valuable because it eliminates a bottleneck that prevents campaign managers from scaling their operations and reduces the risk of human error in date-sensitive communications.

**Key Points:**
* Automation target: End-to-end workflow from Excel input to email draft generation
* Process standardization: Consistent 15-day period calculation, week-based color coding, category standardization
* User validation: Requirements confirmed through stakeholder interviews with clear specifications
* Scalability impact: Enables campaign managers to handle larger volumes without proportional time increase

## Lessons

Previous attempts at partial automation or manual tooling have revealed that campaign managers need a complete solution rather than incremental improvements. The complexity arises not from individual steps but from the orchestration of multiple interdependent operations: date calculation must account for weekends and the specific "next-to-next Sunday" requirement, category standardization must handle edge cases where mappings don't exist, and the system must gracefully handle missing data while maintaining auditability through error logs. Key learnings from stakeholder discussions include the importance of supporting both .eml and .txt output formats for compatibility, allowing user override of output locations while providing sensible defaults, and implementing sequential date assignment with weekend exclusion to match current manual processes. The requirement for rich text (HTML) email templates and specific date formatting (MMMM DD, YYYY) reflects the need for professional, readable output that matches existing communication standards.

**Key Points:**
* Complete automation required: Partial solutions don't address the core time-savings need
* Orchestration complexity: Multiple interdependent operations (dates, standardization, templating) must work together
* User preferences validated: Sequential assignment, weekend exclusion, specific date formats confirmed through interviews
* Output flexibility: Dual format support (.eml primary, .txt secondary) ensures compatibility with existing workflows

## Solutions & Assumptions

The proposed solution is an automated system that reads Excel files containing task/event items with columns for Item ID, Description, Owner, Region, Priority, Category (Column F), Notes, and Email_Group. The system calculates a 15-day date range from today to the next-to-next Sunday, assigns items sequentially to dates (excluding weekends), applies light green color coding to first-week items and dark green to second-week items, standardizes category labels using a CSV mapping file (old_text,new_text format), and generates individual email draft files using a predefined template with placeholders for {{Item_Name}}, {{Category}}, {{Date_Assigned}}, and {{Notes}}. The system outputs .eml files (with .txt as secondary) to ~/email_drafts/ by default, with user override capability. Error handling skips rows with missing required data and generates an error log listing all issues encountered.

**Value Risk:** The assumption that 80% time savings will be achieved depends on the actual volume and complexity of campaigns. If campaigns are infrequent or the manual process is faster than expected, the ROI may be lower. However, stakeholder validation suggests this is a high-frequency, high-pain process.

**Viability Risk:** The assumption that users will adopt the automated output format (.eml/.txt) without requiring integration with email clients may limit adoption if manual import is cumbersome. The fallback to default distribution lists when Email_Group is missing assumes this matches user expectations.

**Feasibility Risk:** The assumption that sequential date assignment with weekend exclusion will meet all use cases may be challenged if future requirements need more complex scheduling logic. The single-template approach may need expansion if different campaign types emerge.

**Usability Risk:** The assumption that users can easily provide correctly formatted Excel files and CSV mapping files may be optimistic. Missing data handling through skipping rows may frustrate users who expect warnings or partial processing. The error log approach assumes users will review logs, which may not happen without clear notifications.

**Key Points:**
* Solution approach: Automated Excel processing → date calculation → standardization → template filling → draft generation
* Value assumption: 80% time savings validated through stakeholder pain point discussions
* Viability assumption: .eml/.txt output format acceptable without email client integration
* Feasibility assumption: Sequential assignment and single template sufficient for initial version
* Usability assumption: Users can provide properly formatted inputs and will review error logs

## Decision Requests

**Primary Decision:** Is the opportunity to automate email campaign draft generation valuable enough to prioritize as an initiative? The stakeholder validation suggests strong pain points, but we need confirmation that the 80% time savings target and elimination of errors justify the development investment.

**Secondary Decisions:**
1. **Output Format Priority:** Should we prioritize .eml format (primary) with .txt as secondary, or is there a preference for a different format that better integrates with existing email workflows?
2. **Error Handling Strategy:** Is skipping rows with missing data and generating error logs the right approach, or should we implement warnings/notifications to ensure users review issues?
3. **Template Flexibility:** Should we proceed with a single default template, or is there immediate need for template variations that would change the scope?
4. **Weekend Exclusion Confirmation:** The requirement to exclude weekends from date assignment is validated, but we need confirmation this matches all use cases or if there are scenarios where weekend inclusion is needed.
5. **Email Group Fallback:** When Email_Group column is missing, using a default distribution list is proposed. Is there a specific default list, or should this be configurable?

**Key Discussion Points:**
* Value justification: Confirm 80% time savings target and error elimination justify development investment
* Output format: Validate .eml/.txt approach or identify preferred integration method
* Error handling: Confirm skip-and-log approach or request alternative user experience
* Scope boundaries: Single template sufficient, or immediate need for variations?
* Edge case handling: Weekend exclusion and Email_Group fallback approach confirmation

