# STINGBIM PROMPT LIBRARY - QUICK REFERENCE GUIDE
**One-Page Cheat Sheet - Find Any Prompt in Seconds**

---

## 🎯 PROMPT FINDER - BY TASK

**I need to...**

### Setup & Infrastructure
- **Create Visual Studio solution** → [P1.1] Visual Studio Solution Generator
- **Setup configuration system** → [P1.2] Core Configuration System
- **Add logging** → [P1.3] Logging System (NLog)
- **Manage Revit transactions** → [P1.4] Transaction Manager
- **Add helper methods** → [P1.5] Helper Classes & Extensions

### Load Data
- **Load parameters (818)** → [P1.6] Parameter Loader
- **Load schedules (146)** → [P1.7] Schedule Loader
- **Load materials (2,450+)** → [P1.8] Material Loader
- **Load formulas (52)** → [P1.9] Formula Loader
- **Add engineering standards** → [P1.10] Standards Integration

### Parameter Operations
- **CRUD operations on parameters** → [P2.1] Parameter Engine Core
- **Process 30,000+ elements/sec** → [P2.1] + [P2.2] GPU Batch Processor
- **AI parameter suggestions** → [P2.3] ML Parameter Classifier
- **Sync across multiple models** → [P2.4] Multi-Model Sync
- **Build parameter UI** → [P2.5] Parameter Manager UI

### Schedule & Material Automation
- **Auto-generate schedules** → [P2.6] Schedule Generator
- **Auto-assign materials** → [P2.7] Material Engine
- **Calculate formulas** → [P2.8] Formula Calculator

### Intelligent Tagging (GENIUS TAG)
- **Intelligent tag placement** → [P3.1] Core Tagging Engine
- **Self-learning tagging** → [P3.2] Learning System
- **Pre-tag quality prediction** → [P3.3] Advisory System
- **Auto-correct tags** → [P3.4] Auto-Correction Engine

### DWG/CAD Conversion
- **Parse DWG files** → [P4.1] DWG Parser
- **Classify layers with AI** → [P4.2] AI Layer Classifier
- **Convert DWG to Revit** → [P4.3] DWG-to-Revit Converter

### Image-to-BIM Conversion
- **Preprocess images for AI** → [P4.4] Image Vision System
- **Detect walls in images** → [P4.5] YOLOv9 Wall Detector
- **Segment floor plans** → [P4.6] SAM Segmentation
- **Extract text from images** → [P4.7] OCR & Layout Analysis
- **Reconstruct floor plans** → [P4.8] Floor Plan Reconstruction

### User Interface
- **Add command console** → [P5.1] Command Console
- **Implement 500+ commands** → [P5.2] Command System
- **Build Revit ribbon** → [P5.3] Ribbon Interface
- **Create sheet manager** → [P5.4] Sheet Manager
- **Add analytics dashboard** → [P5.5] Analytics Dashboard

---

## 📋 PROMPT FINDER - BY WEEK

**Week 1:** [P1.1] [P1.2] [P1.3] - Setup + Config + Logging  
**Week 2:** [P1.4] [P1.5] [P1.6] - Transactions + Helpers + Parameters  
**Week 3:** [P1.7] [P1.8] [P1.9] [P1.10] - Schedules + Materials + Formulas + Standards  

**Week 4:** [P2.1] [P2.2] - Parameter Engine + GPU Acceleration  
**Week 5:** [P2.3] [P2.4] - ML Classifier + Multi-Model Sync  
**Week 6:** [P2.5] [P2.6] - Parameter UI + Schedule Generator  
**Week 7-9:** [P2.7] [P2.8] - Materials + Formulas  

**Week 10-12:** [P3.1] [P3.2] - GENIUS TAG Core + Learning  
**Week 13-14:** [P3.3] [P3.4] - Advisory + Auto-Correction  

**Week 15-16:** [P4.1] [P4.2] [P4.3] - DWG Parser + Classifier + Converter  
**Week 17-19:** [P4.4] [P4.5] [P4.6] [P4.7] [P4.8] - Image-to-BIM (all components)  

**Week 20-22:** [P5.1] [P5.2] [P5.3] [P5.4] [P5.5] - UI + Integration  

---

## 🚀 USAGE PATTERNS

### **Basic Workflow:**
```
1. Find prompt in library (use Ctrl+F)
2. Copy ENTIRE prompt (select all text)
3. Open Claude Code
4. Paste prompt
5. Wait 60-90 seconds
6. Copy generated code
7. Paste into Visual Studio
8. Build & Test
```

### **Advanced Workflow (Multiple Files):**
```
1. Use prompt to generate code
2. Claude Code returns multiple files
3. Create each file in correct project
4. Build solution
5. Fix any compilation errors
6. Run unit tests
7. Commit to Git
```

### **Debugging Workflow:**
```
If code doesn't compile:
1. Copy error message
2. Ask Claude Code: "Fix this error: [paste error]"
3. Get fix
4. Apply fix
5. Rebuild

If tests fail:
1. Review test output
2. Ask Claude Code: "Why does this test fail: [paste test]"
3. Get explanation + fix
4. Update code
5. Re-run tests
```

---

## ⚡ QUICK WINS - START HERE

**Day 1:** Generate entire Visual Studio solution  
→ Use [P1.1] → Get 15 projects ready in 5 minutes

**Day 2:** Add core infrastructure  
→ Use [P1.2] [P1.3] [P1.4] → Get Config + Logging + Transactions in 1 hour

**Day 3:** Load all data  
→ Use [P1.6] [P1.7] [P1.8] → Load 818 params + 146 schedules + 2,450 materials

**Week 1 Complete:** Foundation ready! ✅

---

## 🎓 LEARNING PATH

**Beginner** (Week 1-3):
- Start with Foundation prompts [P1.1 - P1.10]
- Learn Visual Studio, C#, Revit API basics
- Get comfortable with copy-paste workflow

**Intermediate** (Week 4-9):
- Move to Automation prompts [P2.1 - P2.8]
- Learn about ML.NET, ILGPU, WPF
- Understand multi-threading, GPU acceleration

**Advanced** (Week 10-19):
- Tackle AI systems [P3.1 - P4.8]
- Learn machine learning, computer vision
- Master ONNX Runtime, YOLOv9, SAM

**Expert** (Week 20-22):
- Build UI & integration [P5.1 - P5.5]
- Polish and optimize everything
- Deploy production version

---

## 📊 PROGRESS TRACKER

**Print this and check off as you complete:**

### Phase 1: Foundation ☐
- [ ] P1.1 - Visual Studio Solution
- [ ] P1.2 - Configuration
- [ ] P1.3 - Logging
- [ ] P1.4 - Transactions
- [ ] P1.5 - Helpers
- [ ] P1.6 - Parameters
- [ ] P1.7 - Schedules
- [ ] P1.8 - Materials
- [ ] P1.9 - Formulas
- [ ] P1.10 - Standards

### Phase 2: Automation ☐
- [ ] P2.1 - Parameter Engine
- [ ] P2.2 - GPU Batch Processor
- [ ] P2.3 - ML Classifier
- [ ] P2.4 - Multi-Model Sync
- [ ] P2.5 - Parameter UI
- [ ] P2.6 - Schedule Generator
- [ ] P2.7 - Material Engine
- [ ] P2.8 - Formula Calculator

### Phase 3: GENIUS TAG ☐
- [ ] P3.1 - Core Tagging Engine
- [ ] P3.2 - Learning System
- [ ] P3.3 - Advisory System
- [ ] P3.4 - Auto-Correction

### Phase 4: Advanced AI ☐
- [ ] P4.1 - DWG Parser
- [ ] P4.2 - AI Layer Classifier
- [ ] P4.3 - DWG-to-Revit
- [ ] P4.4 - Image Vision
- [ ] P4.5 - YOLOv9 Detector
- [ ] P4.6 - SAM Segmentation
- [ ] P4.7 - OCR & Layout
- [ ] P4.8 - Floor Plan Reconstruction

### Phase 5: UI & Integration ☐
- [ ] P5.1 - Command Console
- [ ] P5.2 - Command System
- [ ] P5.3 - Ribbon Interface
- [ ] P5.4 - Sheet Manager
- [ ] P5.5 - Analytics Dashboard

**COMPLETED:** ___ / 50 prompts

---

## 💡 PRO TIPS

### **Maximize Claude Code Efficiency:**

1. **Copy the full prompt** - Don't skip sections
2. **Be patient** - Complex prompts take 60-90 seconds
3. **Verify before implementing** - Read generated code first
4. **Test immediately** - Don't defer testing
5. **Keep prompts organized** - Use bookmarks in PDF/browser

### **Common Mistakes to Avoid:**

❌ Modifying prompts (use as-is)  
❌ Skipping testing (test everything)  
❌ Accumulating untested code (test immediately)  
❌ Ignoring compilation warnings (fix all warnings)  
❌ Deferring documentation (document as you go)  

### **Time Savers:**

✅ Use Visual Studio snippets  
✅ Setup code templates  
✅ Use ReSharper for refactoring  
✅ Automate builds (MSBuild scripts)  
✅ Use Git for version control  

---

## 🆘 TROUBLESHOOTING

**Problem:** "Code doesn't compile"  
**Solution:** Copy error → Ask Claude Code for fix

**Problem:** "NuGet package won't install"  
**Solution:** Check .NET Framework version, update NuGet, restart VS

**Problem:** "Revit API not found"  
**Solution:** Check Revit 2024 installed, verify DLL paths

**Problem:** "Tests fail"  
**Solution:** Check test dependencies, verify test data, debug test

**Problem:** "Performance too slow"  
**Solution:** Profile code, optimize hot paths, use benchmarks

**Problem:** "Out of memory"  
**Solution:** Process in batches, dispose resources, use streaming

---

## 📞 NEED HELP?

**Resources:**

- **Claude Code:** Ask for debugging help
- **Revit API Docs:** https://www.revitapidocs.com
- **Stack Overflow:** Search "revit api [your issue]"
- **Revit Forums:** https://forums.autodesk.com/t5/revit-api-forum/bd-p/160
- **YouTube:** Search for Revit API tutorials

**Ask Claude Code:**

- "Explain this code: [paste code]"
- "Debug this error: [paste error]"
- "Optimize this method: [paste method]"
- "Add unit tests for: [paste code]"
- "Document this class: [paste class]"

---

## ✅ SUCCESS CHECKLIST

**Before Moving to Next Phase:**

- [ ] All prompts generated successfully
- [ ] All code compiles (0 errors)
- [ ] All tests pass (>90% coverage)
- [ ] Performance benchmarks met
- [ ] Documentation complete
- [ ] Code reviewed
- [ ] Git commits organized
- [ ] Ready for production

---

## 🎉 YOU'RE READY TO BUILD!

**Start with:** [P1.1] Visual Studio Solution Generator

**Good luck! 🚀**
