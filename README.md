# ⚡ N8N Workflow Collection & Documentation

<div align="center">

![N8N Logo](https://raw.githubusercontent.com/n8n-io/n8n/master/assets/n8n-logo.png)

**A curated collection of n8n workflows to automate your tasks and boost productivity**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![n8n](https://img.shields.io/badge/n8n-Workflows-orange)](https://n8n.io)

[Explore Workflows](#workflows) • [Getting Started](#getting-started) • [Contributing](#contributing) • [Documentation](#documentation)

</div>

---

## 📋 Table of Contents

- [About](#about)
- [What is n8n?](#what-is-n8n)
- [Workflows](#workflows)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Importing Workflows](#importing-workflows)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [Contributing](#contributing)
- [Workflow Categories](#workflow-categories)
- [Documentation](#documentation)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)
- [Community](#community)
- [License](#license)
- [Support](#support)

---

## 🎯 About

This repository serves as a comprehensive collection of **n8n workflows** designed to help users automate various tasks, integrate multiple services, and streamline their business processes. Whether you're looking to automate social media posts, sync data between applications, or create complex business logic, you'll find ready-to-use workflows here.

### ✨ Key Features

- 📦 **Ready-to-Use Workflows**: Pre-built workflows that you can import and use immediately
- 📚 **Comprehensive Documentation**: Detailed explanations for each workflow
- 🔧 **Easy Customization**: All workflows are designed to be easily modified for your needs
- 🌟 **Best Practices**: Learn n8n patterns and best practices through real examples
- 🤝 **Community-Driven**: Open for contributions from the community
- 🎨 **Organized by Category**: Workflows organized by use case for easy discovery

---

## 🤔 What is n8n?

[n8n](https://n8n.io) (pronounced "nodemation") is a free and open-source workflow automation tool. It's designed for technical users who want to build complex automations without the limitations of no-code tools, while still being accessible enough for those who prefer a visual interface.

### Why n8n?

- ✅ **Self-Hostable**: Full control over your data
- ✅ **Open Source**: Free to use and modify
- ✅ **Extensive Integrations**: 350+ integrations with popular services
- ✅ **Custom Code**: Write JavaScript when you need advanced logic
- ✅ **Fair-Code License**: Free for personal and commercial use
- ✅ **Active Community**: Large community of users and contributors

---

## 📂 Workflows

### Available Workflows

#### 🤖 **Facebook Automation**
- **[Facebook Messenger AI Chatbot](Facebook%20Automation/facebook-chatbot.json)** 
  - AI-powered chatbot for Facebook Messenger
  - Automated responses using GPT-4o-mini
  - Handles GET/POST webhook requests
  - Comprehensive error handling and validation
  - [📖 Documentation](docs/facebook-messenger-ai-chatbot.md)

#### 🎨 **Image Generation**
- **[AI Product Advertisement Generator](Image/Nano%20🍌.json)**
  - Convert product images to professional advertisements
  - Powered by Google Gemini 2.0 Flash (Nano Banana)
  - 5 customizable ad styles (Professional, Minimalist, Bold, Luxury, Eco-Friendly)
  - Dynamic prompt building and MIME type detection
  - [📖 Documentation](docs/ai-product-advertisement-generator.md)

#### 🦷 **Healthcare & Appointments**
- **[Tribeca Dental Care - AI Appointment System](AI%20Agent/Tribeca-Dental-Care-System-Refactored.json)**
  - Comprehensive dental appointment booking system
  - AI agents for availability checking and booking creation
  - Automated email confirmations with professional design
  - Slack team notifications and Google Sheets logging
  - Google Calendar integration with conflict detection
  - RESTful API with validation and error handling
  - [📖 Documentation](docs/tribeca-dental-care-system.md)

#### 📰 **Web Scraping & Data Collection**
- **[Bangla News Scraper & AI Summarizer](Scrapper/latest-bangla-news-scraper.json)** ⭐ **v3.0 - Dynamic Multi-Source**
  - ✨ **NEW:** Add unlimited news sources via simple configuration
  - ✨ **NEW:** 6 default sources (Prothom Alo, Kaler Kantho, Daily Star, Jugantor, Samakal, Bangladesh Pratidin)
  - ✨ **NEW:** Universal parser works with any news website
  - 🤖 AI-powered summarization in both Bangla and English
  - 📊 Sentiment analysis and topic extraction
  - 🔍 Advanced duplicate detection (URL + title similarity)
  - 💾 Google Sheets integration with 18-column structured storage
  - ⚙️ Configuration-based architecture - no new nodes needed for sources
  - 🔄 Automated scraping every 2 hours (~60 articles per run)
  - 🌐 Multilingual support (Bangla, English, expandable)
  - [📖 Documentation](docs/bangla-news-scraper.md)

### Workflow Categories

Workflows are organized into the following categories:

- **🤖 Social Media Automation**: Automate posting, monitoring, and engagement
- **📊 Data Integration**: Sync data between different platforms
- **📧 Email Automation**: Automated email workflows and notifications
- **🎯 Marketing Automation**: Lead generation, nurturing, and campaigns
- **💼 Business Operations**: CRM updates, task management, reporting
- **🔔 Notifications & Alerts**: Stay informed with automated notifications
- **📈 Analytics & Reporting**: Generate and distribute reports automatically
- **🔄 Data Processing**: Transform, clean, and process data
- **🌐 Web Scraping**: Extract and analyze data from websites
- **🎫 Customer Support**: Automate support ticket handling
- **🏥 Healthcare**: Appointment booking, patient management
- **🎨 AI & Creative Tools**: AI-powered content generation and image processing
- **📰 News & Media**: News aggregation, summarization, and analysis

> **Note**: This is a growing collection! All workflows have been refactored to use the latest n8n versions with comprehensive documentation. Check back regularly for new additions!

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following:

- **Node.js** (v14.15 or above)
- **npm** or **Docker** installed on your system
- Basic understanding of APIs and webhooks (helpful but not required)

### Installation

#### Option 1: Using npm

```bash
# Install n8n globally
npm install n8n -g

# Start n8n
n8n start
```

#### Option 2: Using Docker

```bash
# Pull the n8n Docker image
docker pull n8nio/n8n

# Run n8n
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

#### Option 3: Using npx

```bash
# Run n8n without installing
npx n8n
```

After starting n8n, open your browser and navigate to:
```
http://localhost:5678
```

### Importing Workflows

1. **Download the workflow**: Clone this repository or download individual workflow JSON files
2. **Open n8n**: Navigate to your n8n instance
3. **Import workflow**:
   - Click on the **"Workflows"** menu
   - Click **"Import from File"** or **"Import from URL"**
   - Select the downloaded JSON file
   - Click **"Import"**
4. **Configure credentials**: Set up any required credentials for the nodes used in the workflow
5. **Activate workflow**: Toggle the workflow to "Active" status

---

## 📁 Project Structure

```
n8n-hacktober-workflow/
├── workflows/                  # All workflow JSON files
│   ├── social-media/          # Social media automation workflows
│   ├── data-integration/      # Data integration workflows
│   ├── email/                 # Email automation workflows
│   ├── marketing/             # Marketing automation workflows
│   └── ...                    # Other categories
├── docs/                      # Documentation for workflows
│   ├── setup-guides/          # Setup and configuration guides
│   ├── tutorials/             # Step-by-step tutorials
│   └── best-practices/        # Best practices and tips
├── examples/                  # Example use cases
├── templates/                 # Workflow templates
├── assets/                    # Images and other assets
├── CONTRIBUTING.md            # Contribution guidelines
├── LICENSE                    # License information
└── README.md                  # This file
```

---

## 💡 Usage

### Basic Workflow Usage

1. **Import the workflow** following the steps in [Importing Workflows](#importing-workflows)
2. **Review the workflow**: Understand what each node does
3. **Configure credentials**: Add your API keys and authentication details
4. **Test the workflow**: Use the "Execute Workflow" button to test
5. **Activate**: Turn on the workflow to run automatically

### Customizing Workflows

All workflows in this collection are designed to be customizable:

- Modify node parameters to fit your use case
- Add or remove nodes as needed
- Change trigger conditions
- Adjust error handling
- Add your own custom code using Function nodes

---

## 🤝 Contributing

We welcome contributions from the community! Whether you want to add a new workflow, improve documentation, or fix bugs, your help is appreciated.

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-workflow`
3. **Add your workflow**: Place JSON files in the appropriate category folder
4. **Document your workflow**: Add documentation in the `docs/` folder
5. **Commit your changes**: `git commit -m 'Add amazing workflow'`
6. **Push to the branch**: `git push origin feature/amazing-workflow`
7. **Open a Pull Request**

### Contribution Guidelines

- Ensure your workflow is well-documented
- Include a README for complex workflows
- Test your workflow before submitting
- Follow the existing folder structure
- Use clear, descriptive names for nodes and workflows
- Remove sensitive information (API keys, passwords, etc.)

For detailed guidelines, please see [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 📚 Documentation

### Workflow Documentation

Each workflow should include:

- **Purpose**: What the workflow does
- **Prerequisites**: Required services and credentials
- **Setup Instructions**: How to configure the workflow
- **Trigger**: How the workflow is triggered
- **Flow Description**: Explanation of each step
- **Customization Options**: How to modify for different use cases
- **Troubleshooting**: Common issues and solutions

### Writing Documentation

When adding a new workflow, create a corresponding markdown file in the `docs/` folder with the same name as your workflow.

---

## 🎯 Best Practices

### Workflow Design

- **Keep it simple**: Start with simple workflows and add complexity gradually
- **Use error handling**: Add error nodes to handle failures gracefully
- **Add notes**: Document complex logic within the workflow using Sticky Notes
- **Test thoroughly**: Test all paths and edge cases before deployment
- **Use expressions**: Leverage n8n expressions for dynamic data handling

### Security

- **Never commit credentials**: Always use n8n's credential system
- **Use environment variables**: Store sensitive data in environment variables
- **Validate inputs**: Always validate external data before processing
- **Review permissions**: Ensure credentials have minimal required permissions
- **Regular updates**: Keep n8n and nodes updated

### Performance

- **Batch operations**: Process items in batches when possible
- **Use webhooks**: Prefer webhooks over polling for real-time triggers
- **Optimize HTTP requests**: Minimize unnecessary API calls
- **Error workflow**: Set up error workflows for monitoring

---

## 🔧 Troubleshooting

### Common Issues

#### Workflow Not Triggering

- Check if the workflow is activated
- Verify webhook URLs are correctly configured
- Ensure trigger conditions are met
- Check n8n logs for errors

#### Credential Errors

- Verify credentials are properly configured
- Check if API keys have necessary permissions
- Ensure credentials haven't expired
- Test credentials in isolation

#### Node Execution Errors

- Check node configuration
- Verify input data format
- Review error messages in execution logs
- Test nodes individually

### Getting Help

- **n8n Community Forum**: [community.n8n.io](https://community.n8n.io)
- **Documentation**: [docs.n8n.io](https://docs.n8n.io)
- **GitHub Issues**: Report bugs and request features
- **Discord**: Join the n8n Discord community

---

## 📖 Resources

### Official Resources

- [n8n Website](https://n8n.io)
- [n8n Documentation](https://docs.n8n.io)
- [n8n GitHub Repository](https://github.com/n8n-io/n8n)
- [n8n Community Forum](https://community.n8n.io)
- [n8n YouTube Channel](https://www.youtube.com/c/n8n-io)

### Learning Resources

- [n8n Courses](https://docs.n8n.io/courses/)
- [Workflow Templates](https://n8n.io/workflows)
- [Blog Posts](https://n8n.io/blog)
- [Use Case Guides](https://docs.n8n.io/integrations/)

### Community Resources

- [n8n Discord](https://discord.gg/n8n)
- [n8n Reddit](https://reddit.com/r/n8n)
- [n8n Twitter](https://twitter.com/n8n_io)

---

## 👥 Community

Join our growing community of automation enthusiasts!

- 💬 **Discussions**: Share ideas and get help in GitHub Discussions
- 🐛 **Issues**: Report bugs or request features in GitHub Issues
- 🌟 **Star this repo**: Show your support by starring this repository
- 🔔 **Watch**: Stay updated with new workflows and improvements
- 🤝 **Contribute**: Help make this collection even better

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### What This Means

- ✅ Commercial use allowed
- ✅ Modification allowed
- ✅ Distribution allowed
- ✅ Private use allowed
- ⚠️ License and copyright notice required
- ❌ Liability - The software is provided "as is"
- ❌ Warranty - No warranty provided

---

## 💖 Support

If you find this collection helpful, consider:

- ⭐ **Starring this repository**
- 🐦 **Sharing on social media**
- 🤝 **Contributing your own workflows**
- 💬 **Spreading the word about n8n**
- ☕ **Supporting the n8n project**

---

## 🙏 Acknowledgments

- Thanks to the [n8n team](https://n8n.io) for creating an amazing automation tool
- Thanks to all contributors who have shared their workflows
- Thanks to the n8n community for continuous support and inspiration

---

## 📞 Contact

- **Project Maintainer**: [tarikmanoar](https://github.com/tarikmanoar)
- **Repository**: [n8n-hacktober-workflow](https://github.com/tarikmanoar/n8n-hacktober-workflow)
- **Issues**: [GitHub Issues](https://github.com/tarikmanoar/n8n-hacktober-workflow/issues)

---

<div align="center">

**Made with ❤️ by the community, for the community**

⭐ Star this repo if you find it useful! ⭐

</div>
