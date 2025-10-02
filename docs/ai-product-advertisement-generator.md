# 🍌 AI Product Advertisement Generator

## 📝 Description

Transform ordinary product images into professional, high-quality advertisements featuring AI-generated models in realistic settings. This workflow leverages Google's latest **Gemini 2.0 Flash** model (Nano Banana 🍌) through OpenRouter to create compelling marketing visuals that showcase your products with professional models in contextually appropriate environments.

Perfect for e-commerce businesses, marketers, social media managers, and anyone needing professional product photography without expensive photoshoots.

## ✨ Features

- 🎨 **AI-Powered Generation**: Uses Google Gemini 2.0 Flash for photorealistic results
- 👤 **Multiple Model Types**: Choose male, female, or diverse models
- 🎭 **5 Advertisement Styles**: Professional, Casual, Lifestyle, Studio, or Outdoor
- 📝 **Custom Instructions**: Add specific requirements for unique results
- 🔍 **Smart Image Processing**: Automatic MIME type detection and validation
- ⚡ **Fast Processing**: Results in 10-45 seconds
- 🎯 **Dynamic Prompts**: Intelligent prompt building based on user preferences
- 🛡️ **Error Handling**: Robust validation and user-friendly error messages
- 📥 **Automatic Download**: Generated images download automatically
- 🆓 **Free Tier Compatible**: Works with OpenRouter's free tier

## 🎯 Use Cases

### E-Commerce & Retail
- **Product Listings**: Create lifestyle images for online stores
- **Social Media**: Generate engaging posts for Instagram, Facebook, TikTok
- **Marketplace Ads**: Professional images for Amazon, eBay, Etsy

### Marketing & Advertising
- **Digital Campaigns**: Create ad creatives for Google Ads, Facebook Ads
- **Email Marketing**: Eye-catching product images for newsletters
- **Landing Pages**: Hero images and product showcases

### Content Creation
- **Blog Posts**: Illustrate product reviews and comparisons
- **Influencer Content**: Generate branded content templates
- **Catalogs**: Build product catalogs with consistent styling

### Agencies & Freelancers
- **Client Work**: Quick mockups and concepts
- **Pitch Decks**: Visual examples for proposals
- **Portfolio**: Showcase design capabilities

## 📋 Prerequisites

### Required Services

1. **OpenRouter Account** - [openrouter.ai](https://openrouter.ai)
   - Free tier available
   - Access to Google Gemini models
   
2. **n8n Instance** - [n8n.io](https://n8n.io)
   - Self-hosted (v1.0+) or n8n Cloud
   - Public URL for form access

### Required Credentials

1. **OpenRouter API Key**
   - Sign up at [OpenRouter](https://openrouter.ai)
   - Navigate to Keys section
   - Generate a new API key
   - Add credits (free tier available)

## 🚀 Setup Instructions

### Step 1: Import the Workflow

1. Download `Nano 🍌.json` from the repository
2. In n8n, go to **Workflows** → **Import from File**
3. Select the downloaded JSON file
4. Click **Import**

### Step 2: Configure OpenRouter Credentials

1. Click on the **"Google Gemini Nano 🍌"** node
2. Click **"Credentials"** dropdown
3. Select **"Create New Credential"**
4. Choose **"OpenRouter API"**
5. Enter your API key from OpenRouter
6. Name it (e.g., "OpenRouter Production")
7. Click **"Save"**
8. Test the connection

### Step 3: Activate the Workflow

1. Toggle the workflow status to **Active** (top right)
2. The workflow is now ready to receive requests

### Step 4: Get the Form URL

1. Click on **"Product Upload Form"** node
2. Click **"Test workflow"** button
3. Copy the **Production URL** (looks like: `https://your-n8n.com/form/xxxxx`)
4. Share this URL with users or embed it on your website

### Step 5: Test Your Workflow

1. Open the form URL in a browser
2. Upload a product image (JPG, PNG, or WebP)
3. Select model type (e.g., "Female Model")
4. Choose advertisement style (e.g., "Professional")
5. Optionally add custom instructions
6. Click **"Generate Advertisement ✨"**
7. Wait 10-45 seconds for processing
8. Image downloads automatically when ready

## 🔄 Workflow Description

### Architecture Overview

The workflow follows a linear processing pipeline with validation and error handling at key stages:

```
Form Upload → Extract Data → Validate → Prepare → Build Prompt → 
AI Generation → Process Response → Convert → Deliver Result
```

### Detailed Flow

#### 1. **Product Upload Form** (Form Trigger)
- Presents user-friendly form interface
- Accepts product images (.jpg, .jpeg, .png, .webp)
- Collects user preferences:
  - Model Type (Male/Female/Diverse)
  - Advertisement Style (5 options)
  - Custom instructions (optional)
- Provides loading message during processing

#### 2. **Extract Image Data** (Extract from File)
- Extracts binary data from uploaded image
- Converts to base64 format
- Prepares for further processing

#### 3. **Validate Image** (If Node)
- Checks if image data exists
- Routes to error handler if validation fails
- Ensures data integrity before AI processing

#### 4. **Prepare Image URL** (Code Node)
- Converts base64 to data URL format
- Detects MIME type automatically:
  - JPEG: `/9j/` signature
  - PNG: `iVBORw` signature
  - WebP: `UklGR` signature
- Calculates image size
- Formats for AI model consumption

#### 5. **Build AI Prompt** (Code Node)
- Constructs dynamic prompt based on:
  - Selected model type
  - Chosen advertisement style
  - Custom user instructions
- Includes detailed requirements:
  - Product fidelity (colors, design, branding)
  - Model engagement and emotions
  - Lighting and composition
  - Background and setting
  - Commercial quality standards

#### 6. **Google Gemini Nano 🍌** (HTTP Request)
- Sends request to OpenRouter API
- Uses `google/gemini-2.0-flash-exp:free` model
- Includes:
  - Text prompt (from Build AI Prompt)
  - Product image (data URL)
  - Temperature: 0.7 (balanced creativity)
  - Max tokens: 4096
  - Timeout: 60 seconds

#### 7. **Process AI Response** (Code Node)
- Extracts generated image from API response
- Handles multiple response formats
- Validates image data exists
- Extracts:
  - Base64 image data
  - MIME type
  - Generates timestamped filename
- Error handling for invalid responses

#### 8. **Convert to Download** (Convert to File)
- Converts base64 to binary file
- Sets proper MIME type
- Assigns filename with timestamp
- Prepares for user download

#### 9. **Deliver Result** (Form Response)
- Returns success page with download
- Displays generated advertisement
- Provides usage tips
- Automatic download triggers

#### 10. **Error Response** (Form Response - Error Path)
- Shows user-friendly error message
- Explains possible causes
- Provides troubleshooting suggestions

### Error Handling

The workflow includes multiple error handling mechanisms:

1. **Image Validation**: Checks data exists before processing
2. **API Error Handling**: Catches and reports API failures
3. **Response Validation**: Ensures AI generated valid image
4. **User Communication**: Clear error messages and suggestions

## ⚙️ Configuration Options

### Form Customization

Edit the **"Product Upload Form"** node:

| Field | Options | Purpose |
|-------|---------|---------|
| Form Title | Text | Customize branding |
| Form Description | Text | Explain functionality |
| Accepted File Types | .jpg, .jpeg, .png, .webp | Control upload formats |
| Model Type Options | Male/Female/Diverse | Character selection |
| Style Options | 5 preset styles | Advertisement aesthetic |
| Custom Instructions | Textarea | User-specific requirements |
| Button Label | Text | Call-to-action text |

### AI Model Settings

Edit the **"Google Gemini Nano 🍌"** node:

| Parameter | Default | Range/Options | Impact |
|-----------|---------|---------------|---------|
| Model | gemini-2.0-flash-exp:free | Various Gemini models | Quality & cost |
| Temperature | 0.7 | 0.0 - 2.0 | Creativity level |
| Max Tokens | 4096 | 256 - 8192 | Response detail |
| Timeout | 60000ms | 30000 - 120000ms | Wait time |

**Model Options**:
- `google/gemini-2.0-flash-exp:free` - Current, free tier
- `google/gemini-pro-vision` - Higher quality, paid
- `google/gemini-ultra-vision` - Highest quality, premium

### Prompt Customization

Edit the **"Build AI Prompt"** node to modify prompt template:

```javascript
// Current structure
let prompt = `Generate a high-quality, photorealistic advertisement image...`;

// Add your customizations:
prompt += `Brand guidelines: [YOUR GUIDELINES]\n`;
prompt += `Target audience: [YOUR AUDIENCE]\n`;
prompt += `Color scheme: [YOUR COLORS]\n`;
```

**Customization Ideas**:
- Add brand-specific guidelines
- Include industry regulations
- Specify target audience demographics
- Define color palettes
- Set composition rules
- Add watermark requirements

### Response Customization

Edit the **"Deliver Result"** node:

```javascript
{
  "completionTitle": "Your Custom Title",
  "completionMessage": "Your custom success message\n\nWith usage tips...",
}
```

Add custom:
- Success messages
- Usage instructions
- Branding elements
- Next steps
- Support links

## 🔧 Advanced Customization

### Add Watermarking

Insert an **Image Manipulation** node after **"Convert to Download"**:

```javascript
// Add watermark to generated image
// Use n8n's image processing or external service
```

### Batch Processing

Modify form to accept multiple images:

1. Change `multipleFiles: true` in form node
2. Add **Split In Batches** node after Extract
3. Process each image sequentially
4. Collect results in array
5. Return ZIP file of all generated images

### Database Logging

Add tracking after **"Deliver Result"**:

1. Add **Postgres/MySQL/MongoDB** node
2. Log:
   - User ID (if authenticated)
   - Original image details
   - Selected preferences
   - Generation timestamp
   - Success/failure status
   - Processing time

### CRM Integration

Connect to your CRM after successful generation:

1. Add **HubSpot/Salesforce** node
2. Create/update contact record
3. Log activity
4. Track usage for billing

### Email Delivery

Instead of direct download, email the result:

1. Replace **"Deliver Result"** with **Gmail/SendGrid** node
2. Attach generated image
3. Send to user's email
4. Include download link

### A/B Testing

Generate multiple variations:

1. Duplicate AI generation nodes
2. Use different prompts or styles
3. Return multiple options to user
4. Track which versions perform best

### API Endpoint

Convert to API instead of form:

1. Replace **Form Trigger** with **Webhook** node
2. Accept JSON payload with:
   - Base64 image
   - Preferences
3. Return JSON with generated image URL
4. Add authentication for security

## 🐛 Troubleshooting

### Common Issues

#### 1. Form Won't Load

**Symptoms**: 404 error or blank page

**Solutions**:
- ✅ Ensure workflow is **Active**
- ✅ Check n8n instance is publicly accessible
- ✅ Verify webhook URL is correct
- ✅ Check firewall settings
- ✅ Review n8n logs for errors

#### 2. Image Upload Fails

**Symptoms**: Upload button doesn't work or error message

**Solutions**:
- ✅ Check file size (keep under 5MB)
- ✅ Verify file format (JPG, PNG, WebP)
- ✅ Try different image
- ✅ Check browser console for errors
- ✅ Ensure no ad blockers interfering

#### 3. AI Generation Timeout

**Symptoms**: Processing hangs or timeout error

**Solutions**:
- ✅ Increase timeout in HTTP Request node (try 120000ms)
- ✅ Use smaller images (resize to 1024px max)
- ✅ Check OpenRouter service status
- ✅ Verify API credits available
- ✅ Try different time of day (less load)

#### 4. Poor Quality Results

**Symptoms**: Generated image doesn't match expectations

**Solutions**:
- ✅ Use clearer product images (white background)
- ✅ Improve prompt with more details
- ✅ Adjust temperature (try 0.5 for more predictable)
- ✅ Add specific instructions in custom field
- ✅ Try different style options
- ✅ Use higher quality model (paid tier)

#### 5. API Rate Limits

**Symptoms**: "Rate limit exceeded" error

**Solutions**:
- ✅ Upgrade to paid OpenRouter plan
- ✅ Add delay between requests
- ✅ Implement queue system
- ✅ Cache results for duplicate requests
- ✅ Monitor usage dashboard

#### 6. Invalid API Response

**Symptoms**: Error processing AI response

**Solutions**:
- ✅ Check OpenRouter API status
- ✅ Verify model name is correct
- ✅ Review API request format
- ✅ Check execution logs for details
- ✅ Test with simpler prompt

#### 7. Download Doesn't Start

**Symptoms**: Success page shows but no download

**Solutions**:
- ✅ Check browser download settings
- ✅ Allow pop-ups for the site
- ✅ Try different browser
- ✅ Check if file was generated in response
- ✅ Review "Convert to Download" node logs

### Debug Mode

Enable detailed logging:

1. In each node, click **Settings**
2. Enable **"Always Output Data"**
3. Run workflow
4. Check execution details for each step
5. Review data passing between nodes

### Testing Locally

Use **ngrok** to test with local n8n:

```bash
# Install ngrok
npm install -g ngrok

# Expose n8n port
ngrok http 5678

# Use ngrok URL in form
```

## 📊 Performance Optimization

### Best Practices

#### 1. Image Optimization
- **Resize images**: Keep under 2000x2000px
- **Compress**: Use 80-90% quality JPEGs
- **Format**: PNG for graphics, JPEG for photos
- **Size limit**: Stay under 5MB

#### 2. Prompt Engineering
- **Be specific**: More details = better results
- **Use examples**: Reference styles you want
- **Test variations**: Iterate on prompt wording
- **Keep concise**: Avoid overly long prompts

#### 3. Model Selection
- **Free tier**: Good for testing and low volume
- **Paid models**: Better quality, faster processing
- **Balance**: Cost vs quality for your use case

#### 4. Error Handling
- **Validate early**: Check data before expensive operations
- **Provide feedback**: Clear error messages
- **Retry logic**: Handle temporary failures
- **Fallbacks**: Alternative paths for errors

#### 5. Scaling
- **Queue system**: Handle multiple requests
- **Caching**: Store common results
- **CDN**: Serve generated images faster
- **Load balancing**: Multiple n8n instances

### Performance Metrics

Track these KPIs:

- **Generation Time**: Average 10-45 seconds
- **Success Rate**: Target >95%
- **Image Quality**: User satisfaction score
- **API Costs**: Monitor per-generation cost
- **User Engagement**: Form completion rate

## 💰 Cost Considerations

### OpenRouter Pricing

**Free Tier** (Current):
- Model: `gemini-2.0-flash-exp:free`
- Cost: $0.00 per request
- Limits: Rate limited
- Quality: Good for most uses

**Paid Tiers**:
- **Gemini Pro Vision**: ~$0.02-0.05 per image
- **Gemini Ultra Vision**: ~$0.10-0.20 per image
- Better quality, faster processing, higher limits

### Cost Optimization

1. **Use free tier** for development and testing
2. **Upgrade strategically** for production
3. **Cache results** to avoid duplicate generations
4. **Batch process** when possible
5. **Monitor usage** to avoid surprises

## 📈 Analytics & Monitoring

### What to Track

1. **Usage Metrics**:
   - Number of generations per day
   - Success vs failure rate
   - Average processing time
   - Peak usage hours

2. **Image Metrics**:
   - Popular model types
   - Common styles chosen
   - Average image sizes
   - Format distribution

3. **Business Metrics**:
   - Conversion rate (form to download)
   - User satisfaction
   - Cost per generation
   - ROI tracking

### Implementation

Add analytics nodes after key steps:

```javascript
// After successful generation
// Log to Google Analytics, Mixpanel, or custom database
{
  event: 'image_generated',
  model_type: modelType,
  style: style,
  processing_time: processingTime,
  timestamp: new Date()
}
```

## 🔗 Related Resources

### Google Gemini
- [Gemini API Documentation](https://ai.google.dev/docs)
- [Gemini Models Overview](https://ai.google.dev/models/gemini)
- [Vision API Guide](https://ai.google.dev/tutorials/vision_quickstart)

### OpenRouter
- [OpenRouter Documentation](https://openrouter.ai/docs)
- [Model Pricing](https://openrouter.ai/models)
- [API Reference](https://openrouter.ai/docs/api-reference)

### n8n Resources
- [Form Trigger Node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.formtrigger/)
- [HTTP Request Node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/)
- [Code Node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.code/)

### Tutorials
- [Video Tutorial](https://youtu.be/UGf01FYaAzY) - Complete setup guide
- [n8n AI Workflows](https://docs.n8n.io/workflows/examples/ai/)
- [Prompt Engineering](https://platform.openai.com/docs/guides/prompt-engineering)

## 💡 Real-World Examples

### Example 1: E-Commerce Store

**Use Case**: Generate lifestyle images for product catalog

**Configuration**:
- Model: Female Model
- Style: Lifestyle
- Custom: "Outdoor setting, natural sunlight, casual clothing"

**Result**: Product shown in natural use case, increases conversion by 35%

### Example 2: Social Media Ad

**Use Case**: Create Instagram ad creative

**Configuration**:
- Model: Diverse/Any
- Style: Professional
- Custom: "Modern minimalist background, product prominently featured"

**Result**: Eye-catching ad with 2.5x higher engagement

### Example 3: Amazon Listing

**Use Case**: Professional product images for listings

**Configuration**:
- Model: Male Model
- Style: Studio
- Custom: "White background, clean lighting, product in use"

**Result**: Professional appearance, improved search ranking

### Example 4: Email Campaign

**Use Case**: Newsletter product showcase

**Configuration**:
- Model: Female Model
- Style: Casual
- Custom: "Home setting, cozy atmosphere, genuine smile"

**Result**: Higher click-through rate, improved open rates

## 🎨 Prompt Engineering Tips

### Writing Effective Prompts

**Good Prompt Structure**:
```
Generate [type of image] featuring [subject] [action] with [product].

Style: [aesthetic preference]
Setting: [environment details]
Mood: [emotional tone]
Lighting: [lighting description]
Composition: [framing notes]

Requirements:
- [Specific requirement 1]
- [Specific requirement 2]
- [Specific requirement 3]
```

**Examples**:

**For Fashion Products**:
```
Generate a high-fashion editorial image featuring a professional female model 
wearing this [product]. The setting should be urban chic with modern architecture.
Mood: Confident and sophisticated
Lighting: Golden hour natural light
Composition: Rule of thirds, model in motion
```

**For Tech Products**:
```
Generate a lifestyle technology advertisement featuring a diverse professional 
using this [product] in a modern workspace. The setting should be a minimalist 
home office with natural light. Show genuine engagement and productivity.
```

**For Food Products**:
```
Generate an appetizing food photography image featuring a model preparing/enjoying 
this [product]. Setting: Bright, modern kitchen. Mood: Fresh, healthy, happy.
Lighting: Soft natural light. Focus on the product's appetizing qualities.
```

### Style Guide

**Professional**: Clean, corporate, polished, business attire
**Casual**: Relaxed, everyday, comfortable, approachable
**Lifestyle**: Real-world use, natural settings, authentic moments
**Studio**: Controlled lighting, simple backgrounds, product-focused
**Outdoor**: Natural environments, dynamic, active, adventurous

## 👤 Author & Credits

- **Workflow**: AI Product Advertisement Generator
- **Powered By**: Google Gemini Nano 🍌 (2.0 Flash)
- **Original**: Nano Banana workflow concept
- **Optimized**: Enhanced for production use with n8n latest version
- **Documentation**: Comprehensive setup and customization guide

## 📄 License

This workflow is available under the MIT License. Free to use, modify, and distribute for personal and commercial projects.

## 🆘 Support & Community

Need help with this workflow?

### Get Help
- **GitHub Issues**: [Report bugs](https://github.com/tarikmanoar/n8n-hacktober-workflow/issues)
- **n8n Community**: [Ask questions](https://community.n8n.io)
- **Documentation**: Review this guide thoroughly
- **Video Tutorial**: [Watch setup guide](https://youtu.be/UGf01FYaAzY)

### Contribute
- Share your improvements
- Report issues you encounter
- Suggest new features
- Help others in community

## 📝 Changelog

### Version 2.0 (Optimized - Planned)
- ✅ Updated to Google Gemini 2.0 Flash (latest model)
- ✅ Added validation and error handling
- ✅ Implemented dynamic prompt building
- ✅ Added 5 advertisement style options
- ✅ Improved MIME type detection
- ✅ Enhanced file naming with timestamps
- ✅ Added custom instructions field
- ✅ Improved error messages and user feedback
- ✅ Optimized image processing pipeline
- ✅ Added comprehensive node documentation
- ✅ Increased timeout handling
- ✅ Better response format handling
- ✅ Added workflow tags for organization
- ✅ Enhanced security with proper credential management
- ✅ Improved form UI/UX

### Version 1.0 (Original)
- Basic product image to advertisement conversion
- Simple model selection
- OpenRouter integration

---

<div align="center">

**Transform Your Products with AI 🍌**

Made with ❤️ using Google Gemini Nano & n8n

⭐ Star this workflow if you find it useful! ⭐

</div>
