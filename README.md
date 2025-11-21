# PPTX Course Materials Generator
## Lessons Learned from AI in Society Course Development

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Course Level](https://img.shields.io/badge/Level-Higher%20Education-blue.svg)]()
[![Status](https://img.shields.io/badge/Status-Production%20Ready-green.svg)]()

> **A comprehensive guide to generating high-quality PowerPoint presentations programmatically using html2pptx and pptxgenjs, with detailed speaker notes for educational courses.**

Developed through real-world experience creating a 5-week AI ethics course at CT State Norwalk, this repository contains battle-tested best practices, common pitfalls, and proven solutions for programmatic PPTX generation.

---

## 🎯 What This Repository Offers

- **Design Guidelines**: Complete color palettes, typography specs, and layout standards
- **Technical Best Practices**: Proven workflows that prevent file corruption and generation errors
- **Speaker Notes System**: Comprehensive format with click cues, timing, and teaching tips
- **Troubleshooting Guide**: Solutions to every major issue we encountered
- **Real Examples**: Working code from actual course presentations (35-40 slides each)
- **Templates**: Ready-to-use structures for educational presentations

---

## 🚀 Quick Start

### Problem We Solve
You want to generate professional PowerPoint presentations programmatically with:
- Consistent design across 100+ slides
- Comprehensive speaker notes (200-300 words per slide)
- Proper animations and click cues
- Academic-quality citations
- No file corruption

### Our Solution
```javascript
const pptxgen = require("pptxgenjs");
const { html2pptx } = require("@ant/html2pptx");

// Generate slide
const result = await html2pptx("slide.html", pptx);

// ✅ CRITICAL: Add notes DURING generation (not after)
result.slide.addNotes(`SLIDE INTRODUCTION (2 minutes):
Content here...

🖱️ CLICK → Reveal Bullet 1: "Exact text"
[Detailed explanation]

TEACHING TIP: [Guidance]
SOURCES: [Citations]`);

// Save once at end
await pptx.writeFile({fileName: "output.pptx"});
```

**Key Insight**: Never mix python-pptx with pptxgenjs - it corrupts files. See [Best Practices](docs/best-practices.md) for details.

---

## 📚 Documentation

| Document | Purpose | Start Here? |
|----------|---------|-------------|
| [Design Guidelines](docs/design-guidelines.md) | Color palettes, typography, layouts | ⭐ Yes - Read First |
| [Best Practices](docs/best-practices.md) | Technical workflows and patterns | ⭐ Yes - Critical |
| [Speaker Notes Format](docs/speaker-notes-format.md) | Comprehensive notes structure | If adding notes |
| [Troubleshooting](docs/troubleshooting.md) | Common issues and solutions | When stuck |
| [Common Mistakes](lessons-learned/common-mistakes.md) | What NOT to do | Before starting |
| [Solutions Guide](lessons-learned/solutions.md) | How we fixed problems | When debugging |

---

## 🎓 Our Use Case: AI in Society Course

**Context:**
- 5-week online course for non-technical adult learners
- 2-hour sessions, Mondays 7-9 PM
- 35-40 slides per week with comprehensive speaker notes
- Evidence-based content with academic citations
- Interactive elements (polls, breakouts, debates)

**Challenges We Overcame:**
1. ❌ File corruption from mixing python-pptx and pptxgenjs
2. ❌ Text overflow causing rendering errors
3. ❌ Missing slides (script generating 7 instead of 40)
4. ❌ Speaker notes not appearing in presenter view
5. ✅ All solved - see [Troubleshooting Guide](docs/troubleshooting.md)

**Results:**
- ✅ 150+ slides generated successfully
- ✅ Zero file corruption issues after implementing best practices
- ✅ Consistent design across all weeks
- ✅ Comprehensive speaker notes (200-300 words per content slide)

---

## 🛠️ Technology Stack

**Core Libraries:**
- `pptxgenjs` - PowerPoint generation engine
- `@ant/html2pptx` - HTML to PPTX conversion
- `Node.js` - Runtime environment

**Why These Tools:**
- Native JavaScript (no Python dependencies)
- Programmatic control over every element
- Clean separation: design (HTML/CSS) → conversion → PPTX
- Strong community and documentation

**Alternatives We Tried:**
- ❌ `python-pptx` alone - Limited styling, can't mix with pptxgenjs
- ❌ Google Slides API - Limited offline access, harder automation
- ✅ `html2pptx + pptxgenjs` - Best combination we found

---

## 💡 Key Lessons Learned

### 1. Speaker Notes Must Be Added During Generation
**The #1 Rule** that prevents file corruption:

```javascript
// ❌ WRONG - Will corrupt file
await html2pptx("slide.html", pptx);
await pptx.writeFile("output.pptx");
// Then use python-pptx to add notes ← BREAKS FILE

// ✅ CORRECT
const result = await html2pptx("slide.html", pptx);
result.slide.addNotes("Your notes here"); // Add immediately
// Save at end
```

**Why?** Different libraries use incompatible internal structures. Details: [Best Practices](docs/best-practices.md#critical-rule)

### 2. Text Positioning Requires Careful Math
```javascript
// ❌ WRONG - Text overlaps
addText("Title", {y: 1.5, h: 1.5}); // ends at 3.0
addText("Subtitle", {y: 3.2, h: 0.8}); // starts at 3.2 - TOO CLOSE!

// ✅ CORRECT - Adequate spacing
addText("Title", {y: 1.2, h: 1.2}); // ends at 2.4
addText("Subtitle", {y: 2.8, h: 0.6}); // starts at 2.8 - 0.4" gap
```

**Formula**: Next Y = Previous Y + Previous Height + Gap (0.3-0.5")

### 3. Always Verify Slide Count
```javascript
console.log(`Total slides: ${pptx.slides.length}`);
if (pptx.slides.length !== expectedCount) {
  throw new Error(`Expected ${expectedCount}, got ${pptx.slides.length}`);
}
```

### 4. Comprehensive Speaker Notes Drive Quality
Our format includes:
- SLIDE INTRODUCTION (timing)
- 🖱️ CLICK cues for animations
- Estimated times per section
- TEACHING TIPS
- INTERACTIVE ELEMENTS
- TRANSITIONS
- SOURCES (full citations)

Full format: [Speaker Notes Documentation](docs/speaker-notes-format.md)

---

## 📖 Real-World Examples

### Week 3: Algorithmic Bias and Fairness (35 slides)
- Amazon hiring algorithm case study (3 slides)
- Six types of bias framework
- Three mathematical fairness definitions
- Interactive debate on college admissions
- Full example: [examples/week3-structure.md](examples/week3-structure.md)

### Week 4: AI and Work (40 slides)
- Three case studies (customer service, creative work, manufacturing)
- Two scenarios approach (with/without AGI)
- UBI and job guarantee policy discussions
- Full example: [examples/week4-structure.md](examples/week4-structure.md)

---

## 🎨 Design System

**Color Palette** (tested for accessibility):
```css
--color-primary: #1C2833        /* Deep Navy - main text, headers */
--color-secondary: #E74C3C      /* Coral/Red - emphasis, warnings */
--color-accent: #AAB7B8          /* Silver - supporting elements */
--color-surface: #F4F6F6         /* Off-white - slide backgrounds */
--color-muted: #D5DBDB           /* Light gray - cards, containers */
```

**Typography:**
- Font: Arial (universally available, web-safe)
- Titles: 36-48px, bold
- Body: 16-18px, regular
- Supporting: 12-14px

**Slide Dimensions:**
- 16:9 aspect ratio (960px × 540px)
- Generous padding: 48-72px on sides

Full specs: [Design Guidelines](docs/design-guidelines.md)

---

## 🚧 Common Pitfalls & Solutions

| Problem | Cause | Solution |
|---------|-------|----------|
| File corrupted/won't open | Mixed python-pptx with pptxgenjs | Use only addNotes() during generation |
| Text overflows slide | Insufficient spacing between elements | Use 0.3-0.5" gaps, check Y + H calculations |
| Only 7 slides instead of 40 | JavaScript error mid-generation | Add logging after each slide, verify count |
| Speaker notes missing | Added after file save | Call addNotes() immediately after html2pptx() |
| Inconsistent colors | Hardcoded values | Use CSS variables, reference design system |

Full troubleshooting: [Troubleshooting Guide](docs/troubleshooting.md)

---

## 📦 Repository Contents

```
pptx-course-materials/
├── README.md (this file)
├── LICENSE (CC BY-SA 4.0)
│
├── docs/
│   ├── design-guidelines.md           # Color palettes, typography, layouts
│   ├── best-practices.md              # Technical workflows and patterns
│   ├── speaker-notes-format.md        # Comprehensive notes structure
│   ├── troubleshooting.md             # Common issues and solutions
│   └── getting-started.md             # Step-by-step setup guide
│
├── examples/
│   ├── week3-structure.md             # 35-slide Algorithmic Bias course
│   ├── week4-structure.md             # 40-slide AI and Work course
│   ├── slide-examples/                # Individual slide code samples
│   └── speaker-notes-examples/        # Real speaker notes samples
│
├── templates/
│   ├── title-slide-template.js        # Gradient title slide
│   ├── content-slide-template.js      # Standard content slide
│   ├── case-study-template.js         # Case study introduction
│   ├── section-divider-template.js    # Part dividers
│   └── discussion-questions-template.js # Q&A slides
│
├── lessons-learned/
│   ├── common-mistakes.md             # What NOT to do
│   ├── solutions.md                   # How we fixed problems
│   └── evolution.md                   # How our process improved
│
└── .github/
    ├── CONTRIBUTING.md                # How to contribute
    └── ISSUE_TEMPLATE.md              # Bug report template
```

---

## 🤝 Contributing

We welcome contributions! This repository emerged from real-world challenges, and we know others face similar issues.

**Ways to Contribute:**
- 🐛 Report issues or bugs you've encountered
- 💡 Share your own lessons learned
- 📝 Improve documentation
- 🎨 Add design examples
- 🔧 Contribute code templates

See [CONTRIBUTING.md](.github/CONTRIBUTING.md) for guidelines.

---

## 📄 License

**Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)**

You are free to:
- **Share** — copy and redistribute the material
- **Adapt** — remix, transform, and build upon the material

Under these terms:
- **Attribution** — Give appropriate credit, provide link to license
- **ShareAlike** — Distribute your contributions under the same license

See [LICENSE](LICENSE) for full terms.

**Why CC BY-SA 4.0?**
- Encourages open educational resources
- Ensures improvements remain open
- Allows commercial use with attribution
- Standard license for educational materials

---

## 🎯 Use Cases

This repository is ideal for:
- **Educators** creating consistent course materials
- **Training departments** generating corporate presentations
- **Conference organizers** producing speaker slide templates
- **Researchers** creating reproducible presentation workflows
- **Anyone** who needs programmatic PPTX generation with speaker notes

---

## 🔗 Resources & References

**Documentation:**
- [pptxgenjs Documentation](https://gitbrent.github.io/PptxGenJS/)
- [html2pptx Library](https://www.npmjs.com/package/@ant/html2pptx)
- [PowerPoint Open XML Format](https://learn.microsoft.com/en-us/office/open-xml/structure-of-a-presentationml-document)

**Our Course Context:**
- Institution: CT State Norwalk
- Program: Workforce Development and Continuing Education
- Course: AI in Society: Ethical and Social Implications
- Format: 5 weeks, online, non-technical adult learners

**Related Projects:**
- [reveal.js](https://revealjs.com/) - Web-based presentations
- [Slidev](https://sli.dev/) - Markdown-based slides
- [Marp](https://marp.app/) - Markdown to PPTX

**Why Not These?** They're great for web presentations, but we needed:
- Native PowerPoint files (institutional requirement)
- Comprehensive speaker notes visible in presenter view
- Offline editing capability in PowerPoint/Google Slides
- Academic citation support
- Animation control compatible with Google Slides

---

## 📊 Project Statistics

**Development:**
- Weeks of development: 4
- Presentations generated: 4 (Week 1-4)
- Total slides: 150+
- Speaker notes: 30,000+ words
- Issues encountered and solved: 12+

**Quality Metrics:**
- File corruption rate after best practices: 0%
- Slide generation success rate: 100%
- Student engagement: High (anecdotal)
- Reusability: Complete course materials

---

## 💬 Contact & Support

**Questions or Issues?**
- Open a [GitHub Issue](../../issues)
- Check [Troubleshooting Guide](docs/troubleshooting.md)
- Review [Common Mistakes](lessons-learned/common-mistakes.md)

**Found this useful?**
- ⭐ Star this repository
- 🔄 Share with colleagues
- 📢 Reference in your work
- 🤝 Contribute improvements

---

## 🙏 Acknowledgments

**Developed by:**
- Mike (Course Instructor) - CT State Norwalk
- Claude (AI Assistant) - Anthropic

**Thanks to:**
- CT State Norwalk Workforce Development for supporting innovative course design
- Students who provided feedback on presentation quality
- Open source community for pptxgenjs and html2pptx
- Everyone who encounters these problems and shares solutions

---

## 📅 Version History

**v1.0.0** (November 2025)
- Initial release
- Complete documentation from Weeks 1-4
- All best practices and lessons learned
- Troubleshooting guide
- Templates and examples

**Future Plans:**
- Week 5 materials (Governance and Regulation)
- Video tutorials
- More code examples
- Community contributions
- Additional course materials

---

## 🌟 Featured In

- CT State Norwalk AI in Society Course (Fall 2025)
- *Your project here? Open a PR!*

---

**Built with ❤️ for educators who believe in open educational resources**

**Last Updated**: November 2025  
**Status**: Production Ready  
**Maintenance**: Active
