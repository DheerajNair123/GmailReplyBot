# GmailReplyBot

A Google Apps Script solution that automatically finds emails matching specific criteria and lets you approve before sending replies.

## Features

- **Two-step approval workflow**: Review emails before replies are sent
- **Customizable search criteria**: Filter by sender, subject, content, and more
- **Auto-labeling**: Automatically organizes emails with custom Gmail labels
- **Scheduled scanning**: Option to automatically scan for new emails at set intervals
- **Logging and diagnostics**: Debug mode for troubleshooting

## How It Works

This script follows a simple workflow:

1. **Find matching emails**: The script searches your Gmail for emails matching your criteria
2. **Mark for approval**: Matching emails are labeled with "Pending-Auto-Reply"
3. **Review**: You review the pending emails in Gmail
4. **Approve and send**: Run the send function to reply to approved emails
5. **Track responses**: Emails that received replies are labeled with "Auto-Replied"

## Setup Instructions

### 1. Create a Google Apps Script Project

1. Go to [Google Apps Script](https://script.google.com/)
2. Click "New Project"
3. Delete any default code in the editor
4. Copy and paste the script code
5. Save the project (File > Save) with a name like "Gmail Auto-Reply"

### 2. Configure the Script

Edit these constants at the top of the script to customize your auto-reply:

```javascript
const AUTO_REPLY_TEXT = "Thank you for your email. I'll get back to you as soon as possible.";
const PENDING_LABEL_NAME = "Pending-Auto-Reply";
const REPLIED_LABEL_NAME = "Auto-Replied";
const DEBUG_MODE = true; // Set to true for detailed logging

// Define the criteria to match emails for auto-reply
const EMAIL_CRITERIA = {
  unread: true,
  newer_than_days: 1,    // Only look at emails from the last day
  from_contains: "sender@example.com",  // Only from senders containing this text
  subject_contains: "",  // Only with subjects containing this text
  body_contains: "",     // Only with body containing this text
  label: ""              // Only with this label (leave empty to ignore)
};
```

### 3. Testing the Script

Before setting up automation, test your configuration:

1. Run the `listAllLabels()` function to verify label access
2. Run the `testCriteria()` function to see which emails would match your criteria without taking action

### 4. Using the Script

#### Manual Operation

1. Run `findEmailsForApproval()` to find and label matching emails
2. Search in Gmail for `label:Pending-Auto-Reply` to review the emails
3. Remove the "Pending-Auto-Reply" label from any emails you don't want to reply to
4. Run `sendApprovedReplies()` to send responses to the approved emails

#### Automatic Scanning (Optional)

Run `setupAutomaticFinding()` to create a trigger that automatically finds matching emails every 30 minutes and marks them for approval. You'll still need to manually run `sendApprovedReplies()` to send the responses.

## Functions

| Function | Description |
|----------|-------------|
| `findEmailsForApproval()` | Finds emails matching criteria and labels them for approval |
| `sendApprovedReplies()` | Sends replies to all emails with the pending label |
| `setupAutomaticFinding()` | Sets up a trigger to find emails every 30 minutes |
| `testCriteria()` | Tests search criteria without taking action |
| `listAllLabels()` | Lists all available Gmail labels |

## Permissions

When you first run the script, Google will ask for permission to:
- Read, create, and modify your email
- Connect to an external service
- Display and run third-party web content
- Allow this application to run when you are not present

These permissions are necessary for the script to function properly.

## Troubleshooting

If you encounter issues:

1. Enable DEBUG_MODE to get detailed logs
2. Run `listAllLabels()` to verify label access
3. Check the execution logs in the Apps Script editor
4. Verify your search criteria aren't too restrictive

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Google Apps Script documentation
- Gmail API reference

---

**Note**: This script only sends replies to emails that you approve. It will never automatically send emails without your explicit approval.
