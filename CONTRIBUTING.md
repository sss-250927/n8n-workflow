# 🤝 Contributing to N8N Workflow Collection

First off, thank you for considering contributing to the N8N Workflow Collection! It's people like you that make this project a valuable resource for the entire n8n community.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Getting Started](#getting-started)
- [Contribution Guidelines](#contribution-guidelines)
- [Workflow Submission Guidelines](#workflow-submission-guidelines)
- [Documentation Guidelines](#documentation-guidelines)
- [Pull Request Process](#pull-request-process)
- [Style Guide](#style-guide)
- [Community](#community)

---

## 📜 Code of Conduct

This project and everyone participating in it is governed by our commitment to providing a welcoming and inclusive environment. By participating, you are expected to uphold this code.

### Our Standards

**Examples of behavior that contributes to a positive environment:**

- ✅ Using welcoming and inclusive language
- ✅ Being respectful of differing viewpoints and experiences
- ✅ Gracefully accepting constructive criticism
- ✅ Focusing on what is best for the community
- ✅ Showing empathy towards other community members

**Examples of unacceptable behavior:**

- ❌ Trolling, insulting/derogatory comments, and personal or political attacks
- ❌ Public or private harassment
- ❌ Publishing others' private information without explicit permission
- ❌ Other conduct which could reasonably be considered inappropriate

---

## 🎯 How Can I Contribute?

There are many ways to contribute to this project:

### 1. 📦 Submit New Workflows

Share your n8n workflows with the community! Whether it's a simple automation or a complex integration, your workflow can help others.

### 2. 📚 Improve Documentation

- Fix typos or clarify existing documentation
- Add setup guides for complex workflows
- Create tutorials and how-to guides
- Translate documentation to other languages

### 3. 🐛 Report Bugs

Found a workflow that doesn't work as expected? Let us know by opening an issue!

### 4. 💡 Suggest Enhancements

Have ideas for new workflow categories or improvements? We'd love to hear them!

### 5. 🔍 Review Pull Requests

Help review and test workflows submitted by other contributors.

### 6. 🎨 Improve Design

Help improve the visual aspects, documentation templates, or repository structure.

---

## 🚀 Getting Started

### Prerequisites

Before you begin, make sure you have:

1. **GitHub Account**: You'll need this to fork the repository and submit pull requests
2. **n8n Instance**: Either locally installed or cloud-hosted to test workflows
3. **Git**: Installed on your local machine
4. **Text Editor**: VS Code, Sublime, or your preferred editor

### Setting Up Your Development Environment

1. **Fork the Repository**

   Click the "Fork" button at the top right of the repository page.

2. **Clone Your Fork**

   ```bash
   git clone https://github.com/YOUR-USERNAME/n8n-hacktober-workflow.git
   cd n8n-hacktober-workflow
   ```

3. **Add Upstream Remote**

   ```bash
   git remote add upstream https://github.com/tarikmanoar/n8n-hacktober-workflow.git
   ```

4. **Create a Branch**

   ```bash
   git checkout -b feature/your-workflow-name
   ```

---

## 📝 Contribution Guidelines

### General Guidelines

- ✅ **One workflow per pull request**: Keep PRs focused and manageable
- ✅ **Test thoroughly**: Ensure your workflow works before submitting
- ✅ **Document clearly**: Provide comprehensive documentation
- ✅ **Remove sensitive data**: Never commit API keys, passwords, or personal information
- ✅ **Follow naming conventions**: Use clear, descriptive names
- ✅ **Check for duplicates**: Search existing workflows before submitting

### Before You Submit

- [ ] Your workflow has been tested and works as expected
- [ ] All sensitive information has been removed
- [ ] Documentation is complete and clear
- [ ] Files are placed in the correct directory
- [ ] Workflow name is descriptive and follows naming conventions
- [ ] You've added any necessary setup instructions

---

## 🔄 Workflow Submission Guidelines

### Workflow Requirements

1. **Functionality**
   - Workflow must be fully functional
   - Must solve a real-world problem or use case
   - Should be reusable by others with minimal modifications

2. **Quality**
   - Well-organized nodes
   - Proper error handling
   - Clear node naming
   - Includes sticky notes for complex logic

3. **Security**
   - No hardcoded credentials
   - No API keys or tokens
   - No personal or sensitive information
   - Uses n8n's credential system

### File Structure

Place your workflow files in the appropriate category folder:

```
workflows/
├── social-media/
│   └── your-workflow-name.json
├── data-integration/
│   └── your-workflow-name.json
├── email/
│   └── your-workflow-name.json
└── ...
```

If your workflow doesn't fit existing categories, suggest a new one in your PR description.

### Workflow Naming Convention

Use descriptive, kebab-case names:

✅ **Good Examples:**
- `twitter-to-slack-automation.json`
- `google-sheets-crm-sync.json`
- `email-drip-campaign.json`

❌ **Bad Examples:**
- `workflow1.json`
- `my_workflow.json`
- `test.json`

### Exporting Your Workflow

1. Open your workflow in n8n
2. Click the "..." menu (three dots)
3. Select "Download"
4. Save the JSON file with an appropriate name

**Before exporting:**
- Remove or reset all credentials
- Clear any test data from nodes
- Add sticky notes to explain complex logic
- Ensure all nodes have descriptive names

---

## 📚 Documentation Guidelines

Every workflow submission **must** include documentation. Create a corresponding markdown file in the `docs/` folder.

### Documentation Template

```markdown
# Workflow Name

## 📝 Description

Brief description of what the workflow does and the problem it solves.

## ✨ Features

- Feature 1
- Feature 2
- Feature 3

## 🎯 Use Cases

- Use case 1
- Use case 2
- Use case 3

## 📋 Prerequisites

### Required Services

- Service 1 (with link)
- Service 2 (with link)

### Required Credentials

- API Key for Service 1
- OAuth credentials for Service 2

## 🚀 Setup Instructions

### Step 1: Import the Workflow

1. Download `workflow-name.json`
2. In n8n, go to Workflows > Import from File
3. Select the downloaded file

### Step 2: Configure Credentials

1. Click on the first node that requires credentials
2. Click "Create New Credential"
3. Enter your API key/credentials
4. Test the connection

### Step 3: Customize (Optional)

Describe any customization options or parameters users might want to adjust.

## 🔄 Workflow Description

### Trigger

Description of how the workflow is triggered.

### Flow

1. **Node 1**: Description of what this node does
2. **Node 2**: Description of what this node does
3. **Node 3**: Description of what this node does

## ⚙️ Configuration Options

| Parameter | Description | Default Value |
|-----------|-------------|---------------|
| param1    | Description | value1        |
| param2    | Description | value2        |

## 🔧 Customization

Explain how users can customize the workflow for their needs.

## 🐛 Troubleshooting

### Common Issues

**Issue 1: Error message**
- Solution: Steps to resolve

**Issue 2: Error message**
- Solution: Steps to resolve

## 📸 Screenshots

Include screenshots if helpful (optional but recommended).

## 📊 Workflow Diagram

Describe the flow visually or include a diagram.

## 🔗 Related Resources

- [Link to relevant documentation]
- [Link to API docs]

## 👤 Author

- Name: Your Name
- GitHub: [@yourusername](https://github.com/yourusername)

## 📄 License

This workflow is available under the MIT License.
```

### Documentation Best Practices

- **Be clear and concise**: Use simple language
- **Use examples**: Show real-world use cases
- **Add screenshots**: Visual guides are helpful
- **Test instructions**: Follow your own setup guide to ensure it works
- **Keep it updated**: Update docs if you modify the workflow

---

## 🔀 Pull Request Process

### 1. Update Your Fork

Before starting work, ensure your fork is up to date:

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### 2. Create a Feature Branch

```bash
git checkout -b feature/your-workflow-name
```

### 3. Make Your Changes

- Add your workflow JSON file to the appropriate folder
- Create documentation in the `docs/` folder
- Add any necessary assets to the `assets/` folder

### 4. Commit Your Changes

Use clear, descriptive commit messages:

```bash
git add .
git commit -m "Add [workflow name] for [use case]"
```

**Good commit messages:**
- ✅ `Add Twitter to Slack automation workflow`
- ✅ `Update documentation for email automation`
- ✅ `Fix credential issues in CRM sync workflow`

**Bad commit messages:**
- ❌ `Update`
- ❌ `Fix stuff`
- ❌ `Changes`

### 5. Push to Your Fork

```bash
git push origin feature/your-workflow-name
```

### 6. Create a Pull Request

1. Go to your fork on GitHub
2. Click "Compare & pull request"
3. Fill out the PR template
4. Submit the pull request

### Pull Request Template

When creating a PR, include:

```markdown
## Description

Brief description of the workflow and what it does.

## Type of Contribution

- [ ] New workflow
- [ ] Documentation improvement
- [ ] Bug fix
- [ ] Enhancement
- [ ] Other (please describe)

## Workflow Category

- Category: [e.g., Social Media, Data Integration]

## Checklist

- [ ] I have tested this workflow
- [ ] I have removed all sensitive information
- [ ] I have added documentation
- [ ] I have followed the naming conventions
- [ ] Files are in the correct directories
- [ ] Workflow includes error handling
- [ ] All nodes have descriptive names

## Screenshots (if applicable)

Add screenshots of your workflow in action.

## Additional Notes

Any additional information that reviewers should know.
```

### 7. Review Process

- A maintainer will review your PR
- They may request changes or ask questions
- Make requested changes and push updates to your branch
- Once approved, your PR will be merged!

### After Your PR is Merged

1. Delete your feature branch:
   ```bash
   git branch -d feature/your-workflow-name
   ```

2. Update your fork:
   ```bash
   git checkout main
   git pull upstream main
   git push origin main
   ```

---

## 🎨 Style Guide

### Workflow Design

1. **Node Naming**
   - Use descriptive names: "Fetch User Data from API" instead of "HTTP Request"
   - Be consistent with naming patterns
   - Use action verbs: "Send", "Fetch", "Process", "Transform"

2. **Node Organization**
   - Arrange nodes in a logical, left-to-right flow
   - Align nodes vertically when possible
   - Group related nodes together
   - Use appropriate spacing

3. **Sticky Notes**
   - Add notes to explain complex logic
   - Use different colors for different types of notes
   - Keep notes concise and relevant

4. **Error Handling**
   - Always include error handling for critical operations
   - Use the Error Trigger node when appropriate
   - Provide meaningful error messages

### Code Style (for Function Nodes)

```javascript
// Use clear variable names
const userData = items[0].json;

// Add comments for complex logic
// Calculate the discount based on user tier
const discount = userData.tier === 'premium' ? 0.2 : 0.1;

// Use consistent formatting
return items.map(item => ({
  json: {
    ...item.json,
    processedAt: new Date().toISOString(),
    discount: discount
  }
}));
```

### Documentation Style

- Use Markdown formatting
- Include code blocks with syntax highlighting
- Use tables for structured data
- Add emojis for visual appeal (but don't overdo it)
- Use proper heading hierarchy
- Include links to external resources

---

## 💬 Community

### Getting Help

If you need help with your contribution:

- **GitHub Discussions**: Ask questions in our discussions section
- **Issues**: Open an issue for bugs or feature requests
- **n8n Community**: Join the [n8n community forum](https://community.n8n.io)
- **Discord**: Connect with other contributors

### Communication Channels

- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General questions and discussions
- **Pull Requests**: Code and workflow reviews

### Recognition

Contributors will be recognized in:

- The project README
- Release notes (for significant contributions)
- Our contributors page (if applicable)

---

## 🎉 First Time Contributing?

Don't worry! Here are some tips:

1. **Start Small**: Begin with documentation improvements or simple workflows
2. **Ask Questions**: Don't hesitate to ask for help
3. **Learn from Others**: Review existing workflows and PRs
4. **Be Patient**: Reviews may take time
5. **Have Fun**: Contributing should be enjoyable!

### Good First Issues

Look for issues labeled:
- `good first issue`
- `help wanted`
- `documentation`

---

## 📜 License

By contributing to this project, you agree that your contributions will be licensed under the MIT License.

---

## 🙏 Thank You!

Thank you for taking the time to contribute! Your efforts help make this project better for everyone. Every contribution, no matter how small, is valuable and appreciated.

### Recognition

All contributors will be acknowledged. Significant contributions may be featured in:
- Project README
- Release notes
- Social media shoutouts

---

## 📞 Questions?

If you have questions about contributing, feel free to:

- Open a [GitHub Discussion](https://github.com/tarikmanoar/n8n-hacktober-workflow/discussions)
- Open an [Issue](https://github.com/tarikmanoar/n8n-hacktober-workflow/issues)
- Reach out to the maintainers

---

<div align="center">

**Happy Contributing! 🎉**

Made with ❤️ by the community

</div>
