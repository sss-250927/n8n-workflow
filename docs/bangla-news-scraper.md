# 📰 Bangla News Scraper & AI Summarizer

> **Automated Bangla News Processing Pipeline**  
> Scrape, summarize, translate, and analyze Bangla news articles with AI-powered intelligence

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Workflow Architecture](#workflow-architecture)
- [News Sources](#news-sources)
- [Setup Instructions](#setup-instructions)
- [Configuration](#configuration)
- [AI Summarization](#ai-summarization)
- [Output Format](#output-format)
- [Usage Examples](#usage-examples)
- [Adding New Sources](#adding-new-sources)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [FAQ](#faq)

---

## 🎯 Overview

The **Bangla News Scraper & AI Summarizer** is a fully automated n8n workflow that collects the latest news articles from multiple Bangla and English news websites, uses AI to generate bilingual summaries (Bangla and English), analyzes sentiment, extracts key topics, and stores everything in Google Sheets for easy access and analysis.

**✨ NEW in v3.0:** Dynamic multi-source architecture! Easily add unlimited news sources by editing a single configuration node - no need to add new nodes for each source.

### What This Workflow Does

1. **🌐 Scrapes News** - Fetches latest articles from multiple Bangla news sources
2. **🧹 Cleans Data** - Validates and removes duplicate articles
3. **🤖 AI Summarization** - Generates concise summaries in Bangla and English
4. **📊 Sentiment Analysis** - Determines article sentiment (Positive/Negative/Neutral)
5. **🏷️ Topic Extraction** - Identifies key topics and themes
6. **💾 Stores Data** - Saves to Google Sheets with full metadata
7. **📈 Generates Stats** - Creates summary statistics for monitoring

---

## ✨ Features

### Core Features

- **🔄 Automated Scraping** - Runs every 2 hours automatically
- **🌐 Dynamic Multi-Source** - Easy configuration-based source management
- **➕ Unlimited Sources** - Add new sources without adding nodes
- **🤖 AI-Powered** - Uses OpenAI GPT-4o Mini for intelligent processing
- **🇧🇩 Bangla Support** - Full Unicode Bangla character support
- **🌍 Bilingual Summaries** - Summaries in both Bangla and English
- **📊 Sentiment Analysis** - Automatic sentiment detection
- **🏷️ Topic Extraction** - Identifies key topics and themes
- **🔍 Duplicate Detection** - Smart similarity-based deduplication
- **✅ Data Validation** - Ensures article quality before processing
- **💾 Google Sheets Integration** - Organized, searchable storage
- **📈 Statistics Dashboard** - Summary stats after each run

### Technical Features

- **Latest n8n Version** - Uses modern node types
- **Cheerio HTML Parsing** - Reliable web scraping
- **Fallback Selectors** - Multiple parsing strategies
- **Error Handling** - Graceful failure recovery
- **Structured Output** - JSON schema validation
- **Timezone Support** - Configured for Asia/Dhaka
- **Efficient Processing** - Batch processing with limits
- **Performance Optimized** - 10-minute execution timeout

---

## 🏗️ Workflow Architecture

### Processing Pipeline (12 Nodes) - v3.0 Dynamic

```
 Schedule Trigger (Every 2 hours)
          ↓
 Configure News Sources (6 default sources)
          ↓
     Fetch HTML (Dynamic - loops through all sources)
          ↓
 Parse Articles (Universal parser for any source)
          ↓
    Merge All Sources
          ↓
   Validate Articles
          ↓
  Remove Duplicates (URL + similarity)
          ↓
 AI News Summarizer (Multilingual)
          ↓
   Format Final Data
          ↓
  Save to Google Sheets (18 columns)
          ↓
  Generate Statistics
```

### Node Details

**Configuration Phase (1 node):**
1. **Configure News Sources** - ⚙️ Central config with JavaScript array of sources
   - Contains 6 default sources (expandable to unlimited)
   - Each source has: name, URL, selectors, language, limits
   - Edit this node to add/remove sources!

**Scraping Phase (2 nodes):**
2. **Fetch HTML** - Dynamic HTTP requests to each configured source
3. **Parse Articles (Universal)** - Single parser that works with ANY source
   - Uses selectors from configuration
   - Automatic fallback strategy
   - Bangla/English text detection

**Data Processing Phase (3 nodes):**
4. **Merge All Sources** - Combines articles from all configured sources
5. **Validate Articles** - Ensures required fields exist
6. **Remove Duplicates** - Advanced deduplication:
   - Exact URL matching
   - Title similarity (Levenshtein distance)
   - 85% similarity threshold

**AI Processing Phase (4 nodes):**
7. **AI News Summarizer** - LangChain AI agent with multilingual support
8. **OpenAI GPT-4o Mini** - Language model (Bangla + English)
9. **Structured Output Parser** - JSON schema validation
10. **Format Final Data** - Combines scraped + AI data

**Storage Phase (2 nodes):**
11. **Save to Google Sheets** - Stores with 18 columns of metadata
12. **Generate Statistics** - Creates comprehensive execution summary

**Documentation Nodes (5 sticky notes):**
- Workflow Overview
- Configuration Info
- Parser Info  
- AI Processing Info
- Storage Info

---

## 🌐 News Sources

### Default Sources (6 Configured)

#### 1. Prothom Alo (প্রথম আলো)
- **URL:** https://www.prothomalo.com/
- **Description:** Bangladesh's leading daily newspaper
- **Language:** Bangla
- **Coverage:** National news, politics, sports, entertainment, international

#### 2. Kaler Kantho (কালের কণ্ঠ)
- **URL:** https://www.kalerkantho.com/
- **Description:** Popular Bangla daily newspaper
- **Language:** Bangla
- **Coverage:** National news, culture, sports, lifestyle

#### 3. The Daily Star
- **URL:** https://www.thedailystar.net/
- **Description:** Leading English-language newspaper in Bangladesh
- **Language:** English
- **Coverage:** National news, business, opinion, world news

#### 4. Jugantor (যুগান্তর)
- **URL:** https://www.jugantor.com/
- **Description:** Widely circulated Bangla newspaper
- **Language:** Bangla
- **Coverage:** News, politics, sports, entertainment

#### 5. Samakal (সমকাল)
- **URL:** https://samakal.com/
- **Description:** Popular daily Bangla newspaper
- **Language:** Bangla
- **Coverage:** National news, culture, features

#### 6. Bangladesh Pratidin (বাংলাদেশ প্রতিদিন)
- **URL:** https://www.bd-pratidin.com/
- **Description:** High-circulation Bangla daily
- **Language:** Bangla
- **Coverage:** National news, politics, lifestyle

### 🎯 Easy to Add More!

The workflow uses a **configuration-based architecture** - you can add unlimited sources by simply editing the "Configure News Sources" node. No need to create new HTTP or parser nodes!

### Extraction Strategy

Each source uses:
- **Primary Selectors** - Standard HTML elements (`article`, `.news-card`, `.story-card`)
- **Fallback Selectors** - Generic elements with Bangla text detection
- **Unicode Detection** - Identifies Bangla characters: `[\u0980-\u09FF]`
- **Smart Filtering** - Removes non-news content (ads, navigation, etc.)

### Data Extracted Per Article

- **Title (শিরোনাম)** - Article headline
- **Link (লিংক)** - Full URL to article
- **Description (বিবরণ)** - Article excerpt or preview
- **Image (ছবি)** - Featured image URL
- **Category (বিভাগ)** - News category or section
- **Source Metadata** - Source name and URL

---

## 🚀 Setup Instructions

### Prerequisites

- ✅ n8n instance (v1.0 or higher)
- ✅ OpenAI API account with API key
- ✅ Google account (for Sheets)
- ✅ Basic understanding of web scraping

### Step 1: Import the Workflow

1. Open your n8n instance
2. Click **Import from File**
3. Select `latest-bangla-news-scraper.json`
4. Workflow imports with all nodes

### Step 2: Configure OpenAI Credentials

1. Get your OpenAI API key from [platform.openai.com](https://platform.openai.com/)
2. In n8n, add **OpenAI** credentials
3. Enter your API key
4. Connect to the **OpenAI GPT-4o Mini** node

### Step 3: Configure Google Sheets

#### Create the Spreadsheet

1. Create a new Google Sheet named "Bangla News Archive"
2. Add these column headers in the first row:
   ```
   Date | Time | Weekday | Source | Source (Bangla) | Language | Category | Title | Original Summary | English Summary | Key Topics | Sentiment | Main Theme | Article Link | Image URL | Scraped At | Processed At | Processing Time (sec)
   ```

#### Connect n8n

1. In n8n, add **Google Sheets OAuth2** credentials
2. Authorize n8n to access your Google account
3. Open the **Save to Google Sheets** node
4. Select your spreadsheet from the dropdown
5. Verify column mappings match your headers

### Step 4: Test the Workflow

#### Manual Test

1. Click **Execute Workflow** button
2. Wait for execution to complete (may take 2-5 minutes)
3. Check execution log for any errors
4. Verify data appears in your Google Sheet

#### Test Individual Nodes

1. Click **Execute Node** on "Fetch Prothom Alo"
2. Verify HTML is fetched
3. Click **Execute Node** on "Parse Prothom Alo Articles"
4. Verify articles are extracted
5. Continue testing each node

### Step 5: Activate Automation

1. Review all configurations
2. Click **Active** toggle in top-right
3. Workflow now runs every 2 hours automatically!

---

## ⚙️ Configuration

### Schedule Settings

**Default:** Every 2 hours

**To Change Frequency:**

```javascript
// In Schedule Trigger node
{
  "rule": {
    "interval": [
      {
        "field": "hours",
        "hoursInterval": 2  // ← Change this value
      }
    ]
  }
}
```

**Common Options:**
- Every hour: `"hoursInterval": 1`
- Every 4 hours: `"hoursInterval": 4`
- Every 6 hours: `"hoursInterval": 6`
- Daily at specific time: Use "cronExpression" instead

### Article Limits

**Default:** 10 articles per source × 6 sources = ~60 articles total

**To Change Limit for All Sources:**

```javascript
// In Configure News Sources node
{
  name: 'Source Name',
  // ... other fields ...
  maxArticles: 15,  // ← Change this value
  enabled: true
}
```

**To Change Limit for Specific Source:**

Just update the `maxArticles` value for that source in the configuration array.

**Recommendations:**
- Small scale: 5-10 articles per source
- Medium scale: 10-15 articles per source
- Large scale: 15-25 articles per source
- Note: More articles = longer processing time + higher OpenAI costs

### AI Model Settings

**Current Model:** GPT-4o Mini

**Settings:**
- Temperature: 0.4 (consistent summaries)
- Max Tokens: 1000 (sufficient for summaries)

**To Use Different Model:**

```javascript
// In OpenAI GPT-4o Mini node
{
  "model": "gpt-4o-mini",  // ← Change to: "gpt-4", "gpt-4-turbo", etc.
  "options": {
    "temperature": 0.4,    // 0.0-1.0 (lower = more consistent)
    "maxTokens": 1000      // Increase if summaries are cut off
  }
}
```

### Duplicate Detection Sensitivity

**Default:** 80% similarity threshold

**To Change:**

```javascript
// In Remove Duplicates node
if (similarity > 0.8) {  // ← Change threshold (0.0-1.0)
  isDuplicate = true;
}
```

**Recommendations:**
- Strict (fewer duplicates): 0.7-0.8
- Moderate (balanced): 0.8-0.9
- Loose (allow more): 0.9-0.95

### Timezone

**Default:** Asia/Dhaka (Bangladesh timezone)

**To Change:**
1. Open workflow settings
2. Update `timezone` field
3. Use IANA timezone identifiers (e.g., "America/New_York")

---

## 🤖 AI Summarization

### How It Works

The workflow uses an **AI Agent** powered by OpenAI GPT-4o Mini to analyze and summarize Bangla news articles.

### AI Agent Capabilities

1. **Bangla Language Understanding** - Reads and comprehends Bangla text
2. **Summarization** - Creates concise 2-3 sentence summaries
3. **Translation** - Translates Bangla summary to English
4. **Topic Extraction** - Identifies 3-5 key topics
5. **Sentiment Analysis** - Determines overall sentiment
6. **Theme Identification** - Extracts main theme

### AI Prompt Structure

**User Prompt:**
```
Please summarize this Bangla news article:

**Title:** [Article Title]
**Description:** [Article Description]
**Source:** [News Source]
**Category:** [Article Category]

Provide:
1. A concise Bangla summary (2-3 sentences)
2. An English translation of the summary
3. Key topics/tags (in English, comma-separated)
4. Sentiment (Positive/Negative/Neutral)
```

**System Prompt:**
```
You are an expert news analyst and translator specializing in Bangla (Bengali) language content.

Your Task:
Analyze and summarize Bangla news articles, providing both Bangla and English summaries.

Instructions:
1. Read and understand the Bangla news article
2. Create a concise summary in Bangla (2-3 sentences)
3. Translate the summary to English
4. Identify 3-5 key topics or tags (in English)
5. Determine the sentiment of the article

Output Format (JSON):
{
  "bangla_summary": "বাংলায় সংক্ষিপ্ত সারাংশ",
  "english_summary": "Concise English summary",
  "key_topics": ["topic1", "topic2", "topic3"],
  "sentiment": "Positive/Negative/Neutral",
  "main_theme": "Brief theme description"
}
```

### Output Structure

**Structured JSON Output:**
```json
{
  "bangla_summary": "প্রধানমন্ত্রী আজ নতুন উন্নয়ন প্রকল্প উদ্বোধন করেছেন।",
  "english_summary": "The Prime Minister inaugurated a new development project today.",
  "key_topics": ["politics", "development", "infrastructure"],
  "sentiment": "Positive",
  "main_theme": "Government infrastructure development"
}
```

### Cost Estimation

**Per Article:**
- Input tokens: ~300-500 (article data)
- Output tokens: ~200-400 (summary)
- Cost: ~$0.001-0.002 per article

**Per Run (60 articles with 6 sources):**
- Total cost: ~$0.06-0.12
- Monthly cost (12 runs/day): ~$22-45

**Optimization Tips:**
- Use GPT-4o Mini (cheapest)
- Limit article descriptions
- Batch process when possible
- Monitor token usage

---

## 📊 Output Format

### Google Sheets Structure

**18 Columns:**

| Column | Description | Example |
|--------|-------------|---------|  
| **Date** | Formatted date | October 2, 2025 |
| **Time** | Formatted time | 02:30 PM |
| **Weekday** | Day of week | Thursday |
| **Source** | News source (English) | Prothom Alo |
| **Source (Bangla)** | Source in Bangla | প্রথম আলো |
| **Language** | Article language | Bangla |
| **Category** | Article category | রাজনীতি (Politics) |
| **Title** | Original headline | প্রধানমন্ত্রীর ভাষণ |
| **Original Summary** | AI summary (original language) | সংক্ষিপ্ত সারাংশ... |
| **English Summary** | Translated summary | Brief summary... |
| **Key Topics** | Comma-separated topics | politics, speech, government |
| **Sentiment** | Article sentiment | Positive |
| **Main Theme** | Main theme | Political address |
| **Article Link** | Full URL | https://... |
| **Image URL** | Featured image | https://... |
| **Scraped At** | Scraping timestamp | 2025-10-02T14:30:00Z |
| **Processed At** | Processing timestamp | 2025-10-02T14:32:15Z |
| **Processing Time (sec)** | Time to process | 2.35 |

### Sample Row

```
Date: October 2, 2025
Time: 02:30 PM
Source: Prothom Alo
Category: রাজনীতি
Title (Bangla): প্রধানমন্ত্রীর জাতির উদ্দেশে ভাষণ
Bangla Summary: প্রধানমন্ত্রী আজ জাতির উদ্দেশে গুরুত্বপূর্ণ ভাষণ দিয়েছেন। তিনি দেশের অর্থনৈতিক উন্নয়ন ও ভবিষ্যৎ পরিকল্পনা নিয়ে কথা বলেছেন।
English Summary: The Prime Minister delivered an important address to the nation today. He spoke about the country's economic development and future plans.
Key Topics: politics, economy, development, government, speech
Sentiment: Positive
Main Theme: Prime Minister's national address on economic development
Article Link: https://www.prothomalo.com/bangladesh/...
Image URL: https://www.prothomalo.com/img/...
Scraped At: 2025-10-02T14:30:00.000Z
Processed At: 2025-10-02T14:32:15.000Z
```

### Data Analysis Possibilities

With this structured data, you can:

- **📈 Trend Analysis** - Track topic popularity over time
- **😊 Sentiment Tracking** - Monitor news sentiment trends
- **📰 Source Comparison** - Compare coverage across sources
- **🏷️ Topic Clustering** - Group similar news stories
- **📅 Historical Archive** - Build searchable news database
- **📊 Reporting** - Create charts and dashboards
- **🔍 Search & Filter** - Find articles by topic, sentiment, date
- **🤖 ML Training** - Use as dataset for ML models

---

## 📖 Usage Examples

### Example 1: Daily News Digest

Create a daily summary of all news:

```javascript
// Add after Generate Summary Stats node
// Send email with daily digest
{
  "subject": "Daily Bangla News Digest",
  "body": "Total articles: {{$json.summary.total_articles}}\n\nBy Source:\n{{$json.summary.sources}}\n\nSentiment:\nPositive: {{$json.summary.sentiment_distribution.Positive}}\nNegative: {{$json.summary.sentiment_distribution.Negative}}\nNeutral: {{$json.summary.sentiment_distribution.Neutral}}"
}
```

### Example 2: Topic-Based Alerts

Get notified about specific topics:

```javascript
// Add after Format Final Data node
if ($json.key_topics.includes('economy') || 
    $json.key_topics.includes('technology')) {
  // Send notification
  return [$input.item];
}
return [];
```

### Example 3: Sentiment Dashboard

Create a sentiment dashboard in Google Sheets:

1. Use the existing data
2. Create pivot tables by:
   - Sentiment vs Date
   - Source vs Sentiment
   - Category vs Sentiment
3. Add charts for visualization

### Example 4: Export to Database

Store in PostgreSQL or MongoDB:

1. Add database node after Format Final Data
2. Insert each article as a record
3. Use for advanced querying and analysis

---

## ➕ Adding New Sources

### ✨ New Dynamic Method (v3.0) - RECOMMENDED

With the new configuration-based architecture, adding sources is incredibly easy!

#### Step-by-Step Guide

**1. Open the Configuration Node**
- Click on the **"Configure News Sources"** node
- You'll see a JavaScript code editor with a `newsSources` array

**2. Copy the Source Template**

Scroll to the bottom of the code and you'll find this template:

```javascript
// ============================================
// 📝 TO ADD A NEW SOURCE:
// ============================================
// 1. Copy the template below
// 2. Update all fields with your source info
// 3. Set enabled: true
// 4. Save and test!
//
// {
//   name: 'Source Name',
//   nameInBangla: 'বাংলা নাম',
//   url: 'https://example.com/',
//   language: 'Bangla', // or 'English'
//   selectors: {
//     article: 'article, .news-card',  // Container for each article
//     title: 'h2, .headline',          // Title element
//     link: 'a',                       // Link element
//     description: 'p, .excerpt',      // Description element
//     image: 'img',                    // Image element
//     category: '.category'            // Category element
//   },
//   maxArticles: 10,
//   enabled: true
// },
```

**3. Customize Your Source**

Example - Adding BBC Bangla:

```javascript
const newsSources = [
  // ... existing sources ...
  
  // Add your new source here:
  {
    name: 'BBC Bangla',
    nameInBangla: 'বিবিসি বাংলা',
    url: 'https://www.bbc.com/bengali',
    language: 'Bangla',
    selectors: {
      article: 'article',
      title: 'h3',
      link: 'a',
      description: 'p',
      image: 'img',
      category: '.category'
    },
    maxArticles: 10,
    enabled: true
  }
];
```

**4. Find the Right Selectors**

a) **Open the News Website:**
   - Go to the homepage in your browser
   - Find a news article

b) **Inspect the HTML:**
   - Right-click on the article → "Inspect" or "Inspect Element"
   - Chrome DevTools or Firefox Developer Tools will open

c) **Identify the Selectors:**

```html
<!-- Example HTML structure -->
<article class="news-item">
  <h2 class="headline">Article Title</h2>
  <a href="/article/123">Read more</a>
  <p class="excerpt">Article description...</p>
  <img src="image.jpg" />
  <span class="category">Politics</span>
</article>
```

**Your selectors would be:**
```javascript
selectors: {
  article: 'article, .news-item',    // Container (use comma for multiple options)
  title: 'h2, .headline',            // Title element
  link: 'a',                         // Link (usually just 'a')
  description: 'p, .excerpt',        // Description
  image: 'img',                      // Image (usually just 'img')
  category: '.category, .tag'        // Category
}
```

**5. Test Your New Source**

1. Save the node
2. Click **"Execute Node"** on "Configure News Sources"
3. You should see output for each enabled source
4. Click **"Execute Workflow"** to test the full flow
5. Check if articles are extracted correctly

**6. Troubleshoot if Needed**

If no articles are found:
- Check console logs in the "Parse Articles (Universal)" node
- Try more generic selectors: `article, div, section`
- Use browser DevTools to verify selector matches
- Enable fallback parsing (it's automatic!)

### 🎯 Selector Tips

**Be Flexible - Use Multiple Options:**
```javascript
article: 'article, .news-card, .post, .story-card, .news-item'
```

**Common Patterns:**
```javascript
// Semantic HTML5
article: 'article'

// Class-based
article: '.news-item, .post-item, .article-card'

// ID-based
article: '#news-list article'

// Attribute selectors
article: '[data-type="article"]'

// Descendant selectors
article: '.news-section article'
```

**Finding the Right Selector:**
1. Start generic: `article`
2. If too many matches: Add specificity → `article.news-item`
3. If no matches: Use classes → `.news-card, .post`
4. Multiple options: `article, .news-card, .story`

### 📋 Complete Example

**Adding Dhaka Tribune:**

```javascript
const newsSources = [
  // ... existing 6 sources ...
  
  {
    name: 'Dhaka Tribune',
    nameInBangla: 'ঢাকা ট্রিবিউন',
    url: 'https://www.dhakatribune.com/',
    language: 'English',
    selectors: {
      article: 'article, .article-card',
      title: 'h2, h3, .article-title',
      link: 'a',
      description: 'p, .article-excerpt',
      image: 'img',
      category: '.category, .section-name'
    },
    maxArticles: 10,
    enabled: true
  }
];
```

### ⚙️ Advanced Configuration

**Disable a Source Temporarily:**
```javascript
{
  name: 'Source Name',
  // ... other fields ...
  enabled: false  // ← Set to false to skip this source
}
```

**Adjust Article Limits Per Source:**
```javascript
{
  name: 'High Volume Source',
  // ... other fields ...
  maxArticles: 20  // ← Fetch more articles from this source
}

{
  name: 'Low Volume Source',
  // ... other fields ...
  maxArticles: 5   // ← Fetch fewer articles
}
```

**Multiple Language Support:**
```javascript
{
  name: 'Bilingual Source',
  nameInBangla: 'দ্বিভাষিক উৎস',
  url: 'https://example.com/',
  language: 'Bangla',  // Primary language for detection
  // ... selectors ...
}
```

### 🔄 Workflow Benefits

**Old Method (v1.0-2.0):**
- ❌ Add 2 new nodes per source (HTTP + Parser)
- ❌ Duplicate code for each source
- ❌ Hard to manage many sources
- ❌ Complex workflow diagram

**New Method (v3.0):**
- ✅ Edit one configuration node
- ✅ Add unlimited sources
- ✅ Single universal parser
- ✅ Clean, maintainable workflow
- ✅ Easy to enable/disable sources

### 📊 Scalability

**The workflow can handle:**
- 6 sources (default) = ~60 articles/run
- 10 sources = ~100 articles/run
- 20 sources = ~200 articles/run
- 50+ sources = adjust limits as needed

**Performance Considerations:**
- Each source adds ~10-30 seconds
- AI processing is the slowest part
- Google Sheets has 10 million cell limit
- OpenAI costs scale with article count

---

### 📜 Old Method (Legacy - v1.0-2.0)

**For reference only - not recommended for new sources**

<details>
<summary>Click to expand old method documentation</summary>

#### Step 1: Add HTTP Request Node

```javascript
{
  "parameters": {
    "url": "https://www.new-bangla-news-site.com/",
    "options": {
      "redirect": {
        "redirect": {}
      }
    }
  },
  "type": "n8n-nodes-base.httpRequest",
  "name": "Fetch New Source"
}
```

#### Step 2: Create Parser Node

```javascript
{
  "parameters": {
    "jsCode": `
const cheerio = require('cheerio');
const html = $input.item.json.data;
const $ = cheerio.load(html);

const articles = [];
let count = 0;
const maxArticles = 10;

$('article, .news-item').each(function() {
  if (count >= maxArticles) return false;
  
  const $article = $(this);
  const title = $article.find('h2, h3').first().text().trim();
  let link = $article.find('a').first().attr('href');
  
  if (link && !link.startsWith('http')) {
    link = 'https://www.new-source.com' + link;
  }
  
  if (title && link && title.length > 10) {
    articles.push({
      source: 'New Source',
      title: title,
      link: link,
      // ... more fields
    });
    count++;
  }
});

return articles.map(article => ({ json: article }));
    `
  },
  "type": "n8n-nodes-base.code",
  "name": "Parse New Source"
}
```

#### Step 3: Connect to Merge Node

Add connection from parser to Merge All Articles node.

</details>

---

## 🎨 Customization

### Change Summary Length

**Current:** 2-3 sentences

**To Change:**

```javascript
// In AI News Summarizer prompt
"Provide:\n1. A concise Bangla summary (2-3 sentences)"  
// Change to: "1. A detailed Bangla summary (4-5 sentences)"
```

### Add Image Analysis

Include image description:

```javascript
// Modify AI prompt to include:
"**Image URL:** {{ $json.image }}\n\nAnalyze the image and include description in summary."
```

### Filter by Category

Only process specific categories:

```javascript
// Add after Validate Articles node
if ($json.category.includes('রাজনীতি') || 
    $json.category.includes('অর্থনীতি')) {
  return [$input.item];
}
return [];
```

### Add Translation to Other Languages

Extend AI prompt:

```javascript
"Provide:\n1. Bangla summary\n2. English summary\n3. Hindi summary\n4. Urdu summary"
```

### Custom Sentiment Categories

Modify sentiment options:

```json
{
  "sentiment": {
    "enum": ["Very Positive", "Positive", "Neutral", "Negative", "Very Negative"]
  }
}
```

### Add Article Full Text Extraction

Fetch and summarize full article:

1. Add HTTP Request node after validation
2. Fetch full article URL
3. Extract main content
4. Pass to AI for deeper analysis

---

## 🔧 Troubleshooting

### Common Issues

#### 1. No Articles Extracted

**Symptoms:** Parser returns empty array

**Solutions:**
- Website structure changed → Update selectors
- Check if website blocks scrapers → Add user agent
- Verify URL is correct and accessible
- Test HTML fetch manually

**Debug:**
```javascript
// Add console logging in parser
console.log('HTML Length:', html.length);
console.log('Articles found:', articles.length);
console.log('Sample article:', articles[0]);
```

#### 2. AI Summarization Fails

**Symptoms:** "AI agent failed" errors

**Solutions:**
- Verify OpenAI API key is valid
- Check API credits/limits
- Ensure GPT-4o Mini model is available
- Reduce input length if timeout

**Check API Status:**
- OpenAI status: https://status.openai.com/

#### 3. Duplicate Articles Not Removed

**Symptoms:** Same articles appear multiple times

**Solutions:**
- Lower similarity threshold (0.8 → 0.7)
- Check if titles are actually different
- Add additional deduplication by URL

**Enhanced Deduplication:**
```javascript
// Also check URL
const seenUrls = new Set();
if (seenUrls.has(item.json.link)) {
  isDuplicate = true;
}
seenUrls.add(item.json.link);
```

#### 4. Google Sheets Not Updating

**Symptoms:** Workflow runs but no data in sheets

**Solutions:**
- Re-authorize Google Sheets credentials
- Verify sheet ID is correct
- Check column names match exactly
- Ensure sheet has permissions

#### 5. Bangla Text Shows as ????

**Symptoms:** Bangla characters display incorrectly

**Solutions:**
- Google Sheets: Set font to support Bangla (e.g., "Noto Sans Bengali")
- Ensure UTF-8 encoding
- Check browser/app supports Bangla Unicode

#### 6. Workflow Times Out

**Symptoms:** Execution exceeds 10 minutes

**Solutions:**
- Reduce articles per source (10 → 5)
- Process fewer sources simultaneously
- Increase execution timeout in settings
- Optimize AI prompts (reduce tokens)

#### 7. Rate Limiting Issues

**Symptoms:** HTTP 429 errors from news sites

**Solutions:**
- Add delay between requests
- Use proxies/VPN
- Reduce scraping frequency
- Contact site for API access

---

## 💡 Best Practices

### Web Scraping Ethics

1. **Respect robots.txt** - Check site's scraping policy
2. **Rate Limiting** - Don't overwhelm servers
3. **User Agent** - Identify yourself properly
4. **Cache Results** - Avoid repeated requests
5. **Terms of Service** - Review and comply

### Data Quality

1. **Validate Bangla Text** - Use Unicode detection
2. **Remove Duplicates** - Use similarity matching
3. **Handle Missing Data** - Provide defaults
4. **Timestamp Everything** - Track when data was collected
5. **Monitor Quality** - Regular data audits

### AI Usage

1. **Optimize Prompts** - Clear, concise instructions
2. **Monitor Costs** - Track token usage
3. **Temperature Settings** - Lower for consistency
4. **Error Handling** - Fallback for AI failures
5. **Output Validation** - Verify JSON structure

### Performance

1. **Batch Processing** - Process multiple articles together
2. **Limit Articles** - Don't scrape everything
3. **Efficient Selectors** - Use specific, fast selectors
4. **Async Operations** - Parallel processing when possible
5. **Monitor Execution Time** - Optimize slow nodes

### Maintenance

1. **Regular Testing** - Test workflow weekly
2. **Update Selectors** - Sites change, adapt parsers
3. **Monitor Logs** - Check for new errors
4. **Backup Data** - Export sheets regularly
5. **Version Control** - Save workflow versions

---

## ❓ FAQ

### General Questions

**Q: How often does the workflow run?**  
A: Every 2 hours by default. Customizable in Schedule Trigger node.

**Q: How many articles are processed per run?**  
A: 10 articles per source × 6 sources = ~60 articles total per run (default). Fully customizable per source.

**Q: How many sources are included by default?**  
A: 6 sources (Prothom Alo, Kaler Kantho, Daily Star, Jugantor, Samakal, Bangladesh Pratidin). Unlimited sources can be added!

**Q: What languages are supported?**  
A: Bangla (primary) and English (translations). Can be extended to other languages.

**Q: Can I use this for other languages?**  
A: Yes! Update the Unicode detection pattern and AI prompts for your target language.

**Q: Is this free to run?**  
A: Mostly! Google Sheets is free, n8n can be self-hosted (free), but OpenAI API has costs (~$0.02-0.04 per run).

### Technical Questions

**Q: What's the minimum n8n version required?**  
A: n8n v1.0 or higher for AI agent support.

**Q: Can I run this on n8n Cloud?**  
A: Yes! All features are compatible with n8n Cloud.

**Q: Does this require Node.js packages?**  
A: Yes, Cheerio is used for HTML parsing. It's included in n8n by default.

**Q: How much does OpenAI API cost?**  
A: GPT-4o Mini costs ~$0.001-0.002 per article. Monthly cost: $7-15 for 12 runs/day.

**Q: Can I use a different AI model?**  
A: Yes! Change the model in OpenAI node. Alternatives: GPT-4, Claude, Gemini, etc.

### Customization Questions

**Q: Can I add more news sources?**  
A: Absolutely! See [Adding New Sources](#adding-new-sources) section.

**Q: Can I change the summary language?**  
A: Yes! Modify the AI prompt to request summaries in any language.

**Q: Can I export data to other formats?**  
A: Yes! Add nodes to export to CSV, JSON, databases, etc.

**Q: Can I schedule different times for different sources?**  
A: Yes! Create separate workflows or use conditional scheduling.

**Q: Can I filter articles by topic before processing?**  
A: Yes! Add an If node after validation to filter based on keywords or categories.

### Troubleshooting Questions

**Q: Why are some articles not being extracted?**  
A: Likely due to HTML structure differences. Update the parser selectors to match the site's current structure.

**Q: Why is the AI summary in English instead of Bangla?**  
A: Check the AI prompt ensures "Bangla summary" is requested first. Also verify the model supports Bangla.

**Q: How do I handle articles that can't be summarized?**  
A: The workflow includes fallbacks. If AI fails, default values are used. Check Format Final Data node.

**Q: Can I recover from failed executions?**  
A: Yes! Check n8n execution history, identify the failure point, fix the issue, and re-run from that node.

---

## 📚 Learning Resources

### n8n Documentation
- [n8n Docs](https://docs.n8n.io/)
- [AI Agents](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/)
- [Code Node](https://docs.n8n.io/code/builtin/code-node/)
- [HTTP Request](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/)

### Web Scraping
- [Cheerio Documentation](https://cheerio.js.org/)
- [CSS Selectors Guide](https://www.w3schools.com/cssref/css_selectors.php)
- [Web Scraping Best Practices](https://www.scrapehero.com/web-scraping-best-practices/)

### OpenAI
- [GPT-4o Mini](https://platform.openai.com/docs/models/gpt-4o-mini)
- [Prompt Engineering](https://platform.openai.com/docs/guides/prompt-engineering)
- [API Reference](https://platform.openai.com/docs/api-reference)

### Bangla Computing
- [Bangla Unicode](https://unicode.org/charts/PDF/U0980.pdf)
- [Bangla Typography](https://w3c.github.io/typography/gap-analysis/beng-gap)

---

## 🤝 Contributing

Want to improve this workflow? Contributions are welcome!

**Ideas for Contributions:**
- Add more Bangla news sources
- Improve article extraction accuracy
- Add full article content extraction
- Create visualization dashboards
- Add WhatsApp/Telegram notifications
- Implement article categorization
- Add multi-language support
- Create mobile app integration

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines.

---

## 📄 License

This workflow is part of the n8n Hacktoberfest Workflow Collection.

MIT License - See [LICENSE](../LICENSE) for details.

---

## 🙏 Acknowledgments

- **n8n Team** - For the automation platform
- **OpenAI** - For GPT-4o Mini model
- **Bangla News Sources** - For providing valuable content
- **Cheerio Team** - For the HTML parsing library
- **Community Contributors** - For feedback and improvements

---

## 📊 Changelog

### Version 3.0 (Current - Dynamic Multi-Source)
- ✨ **MAJOR:** Configuration-based source management
- ✨ **MAJOR:** Add unlimited sources without adding nodes
- ✨ **MAJOR:** Universal parser works with any source
- ✅ Streamlined from 17 nodes to 12 nodes
- ✅ 6 default sources (expandable to unlimited)
- ✅ Enhanced duplicate detection (URL + similarity)
- ✅ 18-column Google Sheets output (added Weekday, Language, etc.)
- ✅ Improved documentation with step-by-step source addition
- ✅ Advanced Levenshtein distance similarity matching
- ✅ Automatic fallback parsing strategy
- ✅ Source-specific article limits
- ✅ Enable/disable sources with single flag
- ✅ Comprehensive statistics dashboard
- ✅ Better performance monitoring

### Version 2.0 (AI-Enhanced - Deprecated)
- ✅ AI-powered summarization with GPT-4o Mini
- ✅ Bilingual summaries (Bangla + English)
- ✅ Sentiment analysis
- ✅ Topic extraction
- ✅ Structured JSON output
- ✅ Duplicate detection with similarity matching
- ✅ Comprehensive data validation
- ✅ Google Sheets integration with 14 columns
- ✅ Summary statistics generation
- ✅ 2 hardcoded sources (Prothom Alo, Kaler Kantho)
- ❌ Required adding nodes for each source

### Version 1.0 (Basic - Deprecated)
- Basic web scraping
- Simple article extraction
- No AI processing
- Limited data storage

---

## 📞 Support & Community

### Get Help
- **n8n Community**: [community.n8n.io](https://community.n8n.io)
- **GitHub Issues**: [Report bugs](https://github.com/tarikmanoar/n8n-hacktober-workflow/issues)
- **Discord**: Join n8n Discord server

### Share Your Results
- Tag us on Twitter with #n8n #BanglaNews
- Share your customizations in n8n community
- Contribute improvements via pull requests

---

**Made with ❤️ for the Bangla-speaking community**

**Current Version:** 3.0 (Dynamic Multi-Source)  
*Last Updated: October 2025*
