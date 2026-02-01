# STINGBIM v7 - WEEK 1 STARTER PACKAGE
**Foundation Setup + First AI Experiment**

**Date:** February 1, 2026  
**Duration:** 5 days  
**Goal:** Working development environment + First ML.NET model  
**Prerequisites:** Windows 11, Admin rights  

---

## 📋 WEEK 1 OVERVIEW

```
DAY 1: Environment Setup (3 hours)
├── Visual Studio 2022 Community
├── Revit 2025
├── Claude Code extension
├── Git for Windows
└── Extract StingBIM foundation

DAY 2: Foundation Build (4 hours)
├── Configure VS solution
├── Add Week1 standards
├── Update references
├── Build and test
└── Verify Cable Sizing

DAY 3: ML.NET Setup (4 hours)
├── Install NuGet packages
├── Create ML infrastructure
├── Build parameter dataset
├── Train first model
└── Test predictions

DAY 4: AI Integration (4 hours)
├── Add AI to Cable Sizing
├── Create enhanced dialog
├── Test AI suggestions
├── Collect feedback
└── Measure accuracy

DAY 5: Documentation (3 hours)
├── Document learnings
├── Commit to Git
├── Plan Week 2
├── Demo to stakeholders
└── Celebrate success! 🎉
```

---

## 🚀 DAY 1: ENVIRONMENT SETUP

### **Task 1.1: Install Visual Studio 2022 Community (45 min)**

**CRITICAL: Use official Microsoft installer ONLY**

```
Step 1: Download
├── Go to: https://visualstudio.microsoft.com/downloads/
├── Click "Free download" under "Community 2022"
└── Save: vs_community__*.exe

Step 2: Run Installer
├── Right-click downloaded file → Run as Administrator
├── Wait for Visual Studio Installer to initialize
└── You'll see the workload selection screen

Step 3: Select Workloads
├── Check: ".NET desktop development"
│   ├── ✅ .NET Framework 4.8 development tools
│   ├── ✅ .NET Framework 4.8 targeting pack
│   └── ✅ C# and Visual Basic Roslyn compilers
│
├── Check: "Desktop development with C++"
│   └── (Only if you plan to build native extensions)
│
└── Individual Components tab:
    ├── ✅ .NET Framework 4.8 SDK
    ├── ✅ NuGet package manager
    └── ✅ Git for Windows

Step 4: Install
├── Click "Install" (bottom right)
├── Installation size: ~10-15 GB
├── Time: 30-60 minutes
└── ☕ Coffee break!

Step 5: Verify
├── Launch Visual Studio 2022
├── Sign in (or skip)
├── Choose theme (Dark/Light/Blue)
├── File → New → Project
├── Should see "Class Library (.NET Framework)"
└── Cancel (we'll use existing solution)
```

**Troubleshooting:**
```
Issue: ".NET desktop development" not showing
Fix: Update Visual Studio Installer first

Issue: .NET Framework 4.8 missing
Fix: Individual Components tab → search "4.8" → check all

Issue: Installation fails
Fix: Free up disk space (need 20GB free)
```

---

### **Task 1.2: Install Revit 2025 (30 min)**

```
Step 1: Get Revit 2025
├── Autodesk Account required
├── Education license (if student)
├── Or trial version
└── Download installer

Step 2: Install
├── Run installer as Administrator
├── Select components:
│   ├── ✅ Revit 2025
│   ├── ❌ Revit Content (unless needed)
│   └── ❌ Collaboration (unless needed)
│
├── Installation path: C:\Program Files\Autodesk\Revit 2025\
└── Time: 20-40 minutes

Step 3: Verify
├── Launch Revit 2025
├── Create new project (Architecture)
├── File → Open → Should see recent projects
├── Close Revit
└── ✅ Revit ready!
```

**Important Paths:**
```
Revit Installation: C:\Program Files\Autodesk\Revit 2025\
RevitAPI.dll: C:\Program Files\Autodesk\Revit 2025\RevitAPI.dll
RevitAPIUI.dll: C:\Program Files\Autodesk\Revit 2025\RevitAPIUI.dll
Add-ins: C:\ProgramData\Autodesk\Revit\Addins\2025\
```

---

### **Task 1.3: Install Claude Code Extension (15 min)**

```
Step 1: Install VS Code (if not already installed)
├── Download: https://code.visualstudio.com/
├── Install with default options
└── Launch VS Code

Step 2: Install Claude Code Extension
├── Open Extensions (Ctrl+Shift+X)
├── Search: "Claude Code"
├── Install (by Anthropic)
└── Reload VS Code

Step 3: Configure
├── Sign in with Anthropic account
├── Set API preferences
└── Test with simple prompt
```

**Alternative:** Use Claude via web interface (claude.ai)

---

### **Task 1.4: Install Git for Windows (15 min)**

```
Step 1: Download
├── Go to: https://git-scm.com/download/win
├── Download 64-bit installer
└── Run installer

Step 2: Install Options
├── ✅ Windows Explorer integration
├── ✅ Git Bash Here
├── ✅ Git GUI Here
├── Default editor: Visual Studio Code
├── Line ending: Windows (CRLF)
└── Install

Step 3: Configure
Open Git Bash and run:

git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global core.autocrlf true
```

---

### **Task 1.5: Extract StingBIM Foundation (30 min)**

```
Step 1: Create Development Folder
mkdir C:\Dev\StingBIM
cd C:\Dev\StingBIM

Step 2: Extract Foundation Files
├── Download: StingBIM_Complete_FRESH.tar.gz
├── Extract to: C:\Dev\StingBIM\
└── Should create structure:
    C:\Dev\StingBIM\
    ├── src\
    │   ├── StingBIM.Revit\
    │   ├── StingBIM.Standards\
    │   └── StingBIM.UI\
    ├── data\
    │   ├── Parameters\
    │   ├── Schedules\
    │   └── Materials\
    └── StingBIM.sln

Step 3: Verify Structure
dir /S
Should see:
├── 31 files
├── 20,635 lines total
├── StingBIM.sln file
└── All project folders
```

---

### **Task 1.6: Initialize Git Repository (15 min)**

```
cd C:\Dev\StingBIM

# Initialize Git
git init

# Create .gitignore
echo "bin/
obj/
.vs/
*.user
*.suo
packages/
*.log" > .gitignore

# Initial commit
git add .
git commit -m "Initial commit: StingBIM v7 foundation (20,635 lines)"

# Create development branch
git checkout -b dev/week1

# Verify
git log
git status
```

---

### **Day 1 Checklist:**
```
✅ Visual Studio 2022 installed
✅ .NET Framework 4.8 working
✅ Revit 2025 installed and tested
✅ Claude Code extension ready
✅ Git configured
✅ StingBIM foundation extracted
✅ Git repository initialized
✅ Can open StingBIM.sln in VS 2022
```

---

## 🔧 DAY 2: FOUNDATION BUILD

### **Task 2.1: Open Solution in Visual Studio (15 min)**

```
Step 1: Launch VS 2022
├── File → Open → Project/Solution
├── Navigate to: C:\Dev\StingBIM\
├── Select: StingBIM.sln
└── Wait for solution to load

Step 2: Explore Solution
Solution Explorer should show:
├── 📁 StingBIM.Revit (Main add-in)
│   ├── App.cs (718 lines)
│   ├── StingBIM.addin
│   └── References
│
├── 📁 StingBIM.Standards
│   ├── Electrical/ (NEC, IEC standards)
│   ├── HVAC/ (CIBSE, ASHRAE)
│   ├── Plumbing/ (IPC)
│   └── 18,143 lines total
│
└── 📁 StingBIM.UI
    ├── Dialogs/
    └── 232 lines total

Step 3: Check References
Right-click StingBIM.Revit → Properties → References
Should see:
├── ⚠️ RevitAPI (broken - needs update)
├── ⚠️ RevitAPIUI (broken - needs update)
└── ✅ System references
```

---

### **Task 2.2: Update Revit References (30 min)**

```
Step 1: Remove Old References
├── Right-click StingBIM.Revit → References
├── Find "RevitAPI" → Delete
├── Find "RevitAPIUI" → Delete
└── Any yellow warnings → Delete

Step 2: Add Revit 2025 References
├── Right-click References → Add Reference
├── Click "Browse..."
├── Navigate to: C:\Program Files\Autodesk\Revit 2025\
├── Select: RevitAPI.dll → Add
├── Select: RevitAPIUI.dll → Add
└── Click OK

Step 3: Set Copy Local = False
├── Select RevitAPI in References
├── Properties window (F4)
├── Copy Local: False
├── Repeat for RevitAPIUI
└── ✅ Both should show in References

Step 4: Verify Target Framework
├── Right-click StingBIM.Revit → Properties
├── Application tab
├── Target framework: .NET Framework 4.8
└── ✅ Correct
```

---

### **Task 2.3: Copy Week1 Standards (45 min)**

**You have these standards files available in /mnt/project/:**

```
From your provided data:
├── FORMULAS_WITH_DEPENDENCIES.csv (52 rows)
├── MASTER_PARAMETERS.csv (181 rows)
├── PARAMETER_CATEGORIES.csv (819 rows)
├── MEP_ELECTRICAL_STANDARDS_.xlsx
├── MEP_MECHANICAL_STANDARD.xlsx
├── MEP_PLUMBING_STANDARDS.xlsx
└── BLE_MATERIALS.xlsx
```

**Copy these into your solution:**

```
Step 1: Create Standards Folders
C:\Dev\StingBIM\src\StingBIM.Standards\
├── Data\
│   ├── Parameters\
│   ├── Formulas\
│   └── Materials\

Step 2: Copy Files
Use the view tool to read each file from /mnt/project/
and save to corresponding folders:

MASTER_PARAMETERS.csv → Data\Parameters\
FORMULAS_WITH_DEPENDENCIES.csv → Data\Formulas\
MEP_ELECTRICAL_STANDARDS_.xlsx → Data\Standards\Electrical\
MEP_MECHANICAL_STANDARD.xlsx → Data\Standards\Mechanical\
MEP_PLUMBING_STANDARDS.xlsx → Data\Standards\Plumbing\
BLE_MATERIALS.xlsx → Data\Materials\

Step 3: Add to Project
├── In Solution Explorer
├── Right-click StingBIM.Standards
├── Add → Existing Item
├── Select all copied files
└── Build Action: Content, Copy if newer
```

---

### **Task 2.4: Build Solution (30 min)**

```
Step 1: Clean Solution
├── Build → Clean Solution
├── Wait for completion
└── Output window should show "Clean succeeded"

Step 2: Restore NuGet Packages
├── Tools → NuGet Package Manager
├── → Package Manager Console
├── Run: Update-Package -Reinstall
└── Wait for packages to restore