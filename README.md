# AI-SocialMedia-Automation

Here's your README in text format:

---

# AI Social Media Automation Workflow

## Overview
An end-to-end n8n workflow that automatically generates AI-powered social media content using Google Gemini and posts it to multiple platforms with image generation.

---

## Features
- AI content generation using Google Gemini 2.5 Flash
- Platform-specific captions for Instagram and LinkedIn
- Automatic hashtag and CTA generation
- AI image generation using Pollinations.ai
- Multi-platform posting to Telegram and LinkedIn
- Automated logging to Google Sheets
- Error handling and logging

---

## Tech Stack
- n8n (Workflow Automation)
- Google Gemini 2.5 Flash API (Content Generation)
- Pollinations.ai (Image Generation - Free)
- Telegram Bot API (Social Posting)
- LinkedIn API (Social Posting)
- Google Sheets API (Logging)

---

## Workflow Architecture
```
Trigger → Edit Fields → Gemini AI → Code in JS → Generate Image → IF
                                                                    ↓ true
                                                    Telegram (Photo + Text) → LinkedIn → Google Sheets
                                                                    ↓ false
                                                                Error Handling Sheet
```

---

## APIs Used

### 1. Google Gemini API
- Endpoint: https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent
- Authentication: API Key
- Purpose: Generate social media captions, hashtags, CTA and image prompts
- Free Tier: 15 requests/minute

### 2. Telegram Bot API
- Endpoint: https://api.telegram.org/bot{TOKEN}/sendPhoto
- Authentication: Bot Token
- Purpose: Post content with AI generated images
- Free Tier: Unlimited

### 3. LinkedIn API
- Endpoint: https://api.linkedin.com/v2/ugcPosts
- Authentication: OAuth 2.0
- Purpose: Post professional content to LinkedIn profile
- Free Tier: Available with Developer App

### 4. Pollinations AI
- Endpoint: https://image.pollinations.ai/prompt/{prompt}
- Authentication: None required
- Purpose: Generate AI images from text prompts
- Free Tier: Completely free

### 5. Google Sheets API
- Authentication: OAuth 2.0 via n8n
- Purpose: Log all generated content and track posts

---

## Setup Instructions

### Prerequisites
- n8n installed locally or cloud
- Google Account
- LinkedIn Account
- Telegram Account

### Step 1 — Gemini API Setup
1. Go to https://aistudio.google.com
2. Click "Get API Key"
3. Create new API key
4. Copy and save the key

### Step 2 — Telegram Bot Setup
1. Open Telegram
2. Search @BotFather
3. Send /newbot
4. Follow instructions
5. Copy the bot token
6. Get chat ID from https://api.telegram.org/bot{TOKEN}/getUpdates

### Step 3 — LinkedIn API Setup
1. Go to https://developer.linkedin.com
2. Create new app
3. Add products: Share on LinkedIn, Sign In with OpenID
4. Get Client ID and Client Secret
5. Generate OAuth token from token generator

### Step 4 — Google Sheets Setup
1. Create a new Google Sheet
2. Add columns: Topic, Instagram Caption, LinkedIn Post, Hashtags, CTA, Image URL, Time
3. Connect via n8n Google Sheets node

### Step 5 — n8n Workflow Setup
1. Import the workflow JSON file
2. Add credentials for each service
3. Update Telegram chat ID
4. Update LinkedIn person ID
5. Test the workflow

---

## Google Sheets Columns
| Column | Description |
|---|---|
| Topic | Input topic |
| Instagram Caption | AI generated Instagram caption |
| LinkedIn Post | AI generated LinkedIn post |
| Hashtags | Relevant hashtags |
| CTA | Call to action |
| Image URL | Pollinations AI generated image URL |
| Time | Timestamp of post |

---

## Test Cases

### Test Case 1 — AI in Education
- Input: "AI in Education"
- Output: Generated captions, hashtags, image
- Platforms: Telegram, LinkedIn
- Status: Success

### Test Case 2 — Sustainable Fashion
- Input: "Sustainable Fashion"
- Output: Generated captions, hashtags, image
- Platforms: Telegram, LinkedIn
- Status: Success

### Test Case 3 — Future of Remote Work
- Input: "Future of Remote Work"
- Output: Generated captions, hashtags, image
- Platforms: Telegram, LinkedIn
- Status: Success

---

## Error Handling
- IF node checks if content generation was successful
- True path: Posts to all platforms and logs to Sheets
- False path: Logs error details to separate Error Handling sheet
- Each node has "Continue on Error" enabled

---

## Limitations
1. Gemini API free tier limited to 15 requests per minute
2. LinkedIn image embedding requires complex binary upload process — currently implemented as text post
3. Pollinations.ai images may not always perfectly match the topic
4. LinkedIn OAuth token expires periodically and needs manual refresh
5. Workflow currently runs manually — can be automated with n8n Schedule trigger
6. Instagram and YouTube direct posting not supported due to strict API review requirements

---

## Future Improvements
- Add scheduling for automatic daily posts
- Integrate Leonardo AI for better image quality
- Add Facebook posting
- Add sentiment analysis for content optimization
- Add analytics tracking
- Support multiple topics in one run

---

## Author
- Name: Jagadeshwar Davuluri
- University: Woxsen University
- Assignment: Final Selection Round — AI Social Media Automation

---

## License
This project is created for internship assignment purposes.

