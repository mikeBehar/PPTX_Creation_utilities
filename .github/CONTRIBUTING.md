# Contributing to PPTX Course Materials

Thank you for your interest in contributing! This project helps educators worldwide create better course materials.

## How to Contribute

### Ways to Help

1. **Report Issues**
   - Found a bug? Open an issue
   - Documentation unclear? Let us know
   - Have a question? Ask!

2. **Improve Documentation**
   - Fix typos
   - Clarify confusing sections
   - Add examples
   - Translate to other languages

3. **Share Your Experience**
   - Lessons learned from your own projects
   - New troubleshooting solutions
   - Performance optimizations
   - Design improvements

4. **Add Code Examples**
   - Template variations
   - New slide types
   - Helper functions
   - Automation scripts

## Getting Started

### Small Contributions (No Coding Required)

**For typos and documentation fixes:**
1. Click the "Edit" button (pencil icon) on the file in GitHub
2. Make your changes
3. Scroll down and describe what you changed
4. Click "Propose changes"
5. We'll review and merge!

**That's it! No Git knowledge required for small fixes.**

### Larger Contributions

1. **Fork the repository**
   - Click "Fork" button on GitHub
   - Creates your own copy

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/pptx-course-materials.git
   cd pptx-course-materials
   ```

3. **Create a branch**
   ```bash
   git checkout -b feature/your-improvement
   ```

4. **Make your changes**
   - Edit files locally
   - Test your changes
   - Follow our [style guide](#style-guide)

5. **Commit your changes**
   ```bash
   git add .
   git commit -m "Brief description of changes"
   ```

6. **Push to your fork**
   ```bash
   git push origin feature/your-improvement
   ```

7. **Open a Pull Request**
   - Go to your fork on GitHub
   - Click "New Pull Request"
   - Describe your changes
   - Submit!

## Contribution Guidelines

### Code of Conduct

**Be respectful and constructive:**
- Welcome newcomers
- Assume good intentions
- Provide constructive feedback
- Focus on the idea, not the person
- No harassment or discrimination

### Documentation Standards

When adding or updating documentation:

- **Clear and concise** - Get to the point
- **Examples** - Show, don't just tell
- **Tested** - Verify instructions work
- **Organized** - Use headers and structure
- **Proofread** - Check spelling and grammar

**Format:**
```markdown
## Clear Header

Brief introduction explaining what this covers.

### Step-by-Step Instructions

1. First step with explanation
2. Second step
   - Sub-point if needed

**Example:**
```language
code example here
```

**Common mistakes:**
- What to avoid
- Why it's a problem
```

### Code Standards

If contributing code:

- **Comment liberally** - Explain the "why"
- **Follow existing patterns** - Match the style
- **Test thoroughly** - Verify it works
- **Document edge cases** - Note limitations
- **Keep it simple** - Clarity over cleverness

**JavaScript Style:**
```javascript
// Good: Clear variable names
const speakerNotes = allNotes[slideNumber];

// Bad: Cryptic abbreviations
const spkNts = notes[num];

// Good: Comments explain why
// Using immediate addNotes() to prevent corruption
result.slide.addNotes(speakerNotes);

// Bad: No explanation
result.slide.addNotes(speakerNotes);
```

### Commit Message Format

**Structure:**
```
Short summary (50 chars or less)

Longer explanation if needed:
- What changed
- Why it changed
- Any side effects

Fixes #123 (if applicable)
```

**Examples:**
```
✅ Good:
Fix text overflow in title slide positioning

Added 0.4" gap between title and subtitle elements
to prevent overlap during generation. Addresses
common error in #45.

❌ Bad:
fixed bug
```

### Pull Request Checklist

Before submitting:

- [ ] Changes tested locally
- [ ] Documentation updated (if needed)
- [ ] Examples added/updated (if needed)
- [ ] No breaking changes (or clearly noted)
- [ ] Commit messages clear
- [ ] Branch up to date with main

## Types of Contributions

### 🐛 Bug Reports

**Use this template:**
```markdown
**Describe the bug**
Clear description of what went wrong

**To Reproduce**
1. Step 1
2. Step 2
3. See error

**Expected behavior**
What should happen

**Actual behavior**
What actually happened

**Environment:**
- Node.js version:
- pptxgenjs version:
- OS:

**Additional context**
Error messages, screenshots, etc.
```

### 💡 Feature Requests

**Use this template:**
```markdown
**Is your feature request related to a problem?**
Describe the problem or limitation

**Describe the solution you'd like**
What would make it better?

**Describe alternatives you've considered**
Other approaches you thought about

**Use case**
How would you use this feature?

**Additional context**
Examples, mockups, etc.
```

### 📚 Documentation Improvements

**What to include:**
- Which document needs improvement
- What's unclear or missing
- Suggested changes or additions
- Why it's important

### 🎨 Design Examples

**If sharing design work:**
- Screenshots of slides
- Color palettes used
- Typography choices
- What course/context it was for
- What worked well / what didn't

## Review Process

### What Happens Next

1. **Acknowledgment** (24-48 hours)
   - We'll comment to confirm we saw it
   
2. **Discussion** (if needed)
   - Questions about approach
   - Suggestions for improvements
   - Clarifications

3. **Review** (3-7 days)
   - Check quality and fit
   - Test changes
   - Request modifications if needed

4. **Merge** (or explanation)
   - If accepted: merged and credited
   - If not: explanation of why

### Acceptance Criteria

We accept contributions that:
- ✅ Improve the project
- ✅ Follow guidelines
- ✅ Are well-documented
- ✅ Don't break existing functionality
- ✅ Align with project goals

We may decline contributions that:
- ❌ Are out of scope
- ❌ Duplicate existing work
- ❌ Lack documentation
- ❌ Break existing features
- ❌ Add unnecessary complexity

## Recognition

### Contributors

All contributors are recognized in:
- README.md Contributors section
- GitHub contributors page
- Release notes (for significant contributions)

### Types of Recognition

- 🎖️ Listed in Contributors section
- 📝 Mentioned in release notes
- 🏆 Badge if significant contributions
- 💬 Public thank you on social media (if desired)

## Questions?

**Need help?**
- Open an issue with label "question"
- Ask in Pull Request comments
- Check existing discussions

**Want to discuss before contributing?**
- Open an issue describing your idea
- We'll discuss approach
- Then you can implement

## Examples of Great Contributions

### Documentation Fix
```markdown
Fix: Clarify speaker notes format

Changed wording in speaker-notes-format.md to make
the click cue format more explicit. Added example
showing exact emoji to use.

Fixes confusion mentioned in #12.
```

### New Example
```markdown
Add: Week 5 governance structure example

Includes 40-slide outline for governance and regulation
topic, following same format as Week 3-4 examples.

Useful for others teaching similar content.
```

### Bug Fix
```markdown
Fix: Text positioning formula

Corrected spacing formula in best-practices.md.
Was using 0.2" gap, now correctly recommends 0.3-0.5".

Prevents "content overflow" errors.
```

## Getting Credit

Your contributions help educators worldwide. Here's how we'll credit you:

**In README.md:**
```markdown
## Contributors

Thanks to these wonderful people:

- [@yourname](github.com/yourname) - Fixed text positioning bug
```

**In CHANGELOG.md:**
```markdown
## v1.1.0

### Improvements
- Fixed text positioning formula (Thanks @yourname!)
```

**On social media:**
```
Big thanks to @yourname for improving our documentation!
Check out their contribution: [link]
```

## Thank You!

Every contribution makes this project better for educators worldwide. Whether you:
- Fix a typo
- Report a bug
- Share an example
- Improve documentation
- Add a feature

**You're helping advance open education. Thank you!** 🎓

---

**Document Version:** 1.0  
**Last Updated:** November 2025  
**Questions?** Open an issue!
