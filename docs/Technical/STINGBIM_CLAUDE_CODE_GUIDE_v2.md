# STINGBIM V2.0 - CLAUDE CODE INTEGRATION GUIDE
## Optimizing Development with AI-Powered Agentic Coding

**Date:** January 31, 2026  
**Version:** 2.0 Claude Code Edition  
**Platform:** Claude Code + C# .NET Framework 4.8

---

## 📖 TABLE OF CONTENTS

1. [Claude Code Overview](#claude-code-overview)
2. [Project Setup](#project-setup)
3. [Custom Slash Commands](#custom-slash-commands)
4. [MCP Server Integration](#mcp-server-integration)
5. [Development Workflows](#development-workflows)
6. [CI/CD Integration](#cicd-integration)
7. [Testing Automation](#testing-automation)
8. [Documentation Generation](#documentation-generation)

---

## 🤖 CLAUDE CODE OVERVIEW

### **What is Claude Code?**

Claude Code is Anthropic's agentic coding tool that enables autonomous software development through:

- **Agentic Workflow**: Gather context → Take action → Verify → Repeat
- **Native IDE Integration**: VS Code, Cursor, Windsurf, JetBrains
- **MCP Integration**: Model Context Protocol for external data access
- **Automatic Context Compaction**: Efficient long-conversation handling
- **Custom Commands**: Project-specific slash commands

### **Why Claude Code for StingBIM?**

1. **Complex Codebase**: 100,000+ lines of C# across 500+ files
2. **Multiple Technologies**: Revit API, ML.NET, ONNX Runtime, ILGPU
3. **AI Model Integration**: LLM, computer vision, ML pipelines
4. **Extensive Documentation**: Auto-generate from code
5. **Test-Driven Development**: Automated test generation
6. **CI/CD Pipeline**: GitHub Actions automation

---

## 🚀 PROJECT SETUP

### **Directory Structure**

```
StingBIM/
├── .claude/                          # Claude Code configuration
│   ├── commands/                     # Custom slash commands
│   │   ├── param-manager.md         # Parameter Manager commands
│   │   ├── dwg-import.md            # DWG Import commands
│   │   ├── ai-models.md             # AI Model commands
│   │   ├── testing.md               # Testing commands
│   │   └── deployment.md            # Deployment commands
│   ├── mcp.json                     # MCP server configuration
│   └── settings.json                # Claude Code settings
├── .github/                         # GitHub Actions workflows
│   └── workflows/
│       ├── build.yml
│       ├── test.yml
│       ├── deploy.yml
│       └── claude-review.yml
├── Source/                          # C# source code
│   ├── Core/
│   ├── ParameterManager/
│   ├── DWGImporter/
│   ├── AIEngine/
│   └── UI/
├── Tests/                           # Unit and integration tests
├── Models/                          # AI models (ONNX, GGUF)
├── Documentation/                   # Auto-generated docs
└── README.md
```

### **Initial Setup**

```bash
# 1. Initialize Claude Code in project
cd StingBIM
claude init

# 2. Configure project
claude config set project-name "StingBIM"
claude config set language "C#"
claude config set framework ".NET Framework 4.8"
claude config set test-framework "xUnit"

# 3. Set up custom commands
mkdir -p .claude/commands
```

---

## ⚡ CUSTOM SLASH COMMANDS

### **Command Structure**

Create `.claude/commands/<name>.md` files with this format:

```markdown
# Command Name

**Description:** Brief description

**Usage:**
/command-name [parameters]

**Parameters:**
- param1: Description
- param2: Description

**Examples:**
```language
example code
```

**Output:**
Expected output description
```

### **Parameter Manager Commands**

**File:** `.claude/commands/param-manager.md`

```markdown
# Parameter Manager Development Commands

## /param-create-class
Generate a new parameter management class

**Usage:**
/param-create-class [class-name] [functionality]

**Examples:**
/param-create-class ParameterValidator "Validates parameter formulas and dependencies"

## /param-add-feature
Add a feature to existing parameter manager

**Usage:**
/param-add-feature [feature-name] [description]

**Examples:**
/param-add-feature "genealogy-rollback" "Add rollback functionality to parameter genealogy system"

## /param-generate-tests
Generate comprehensive tests for parameter features

**Usage:**
/param-generate-tests [class-name] [coverage-target]

**Examples:**
/param-generate-tests ParameterInferenceEngine 90%

## /param-optimize
Optimize parameter processing performance

**Usage:**
/param-optimize [class-name] [target-metric]

**Examples:**
/param-optimize BatchOperationsEngine "Process 100k elements in <5 seconds"
```

### **DWG Import Commands**

**File:** `.claude/commands/dwg-import.md`

```markdown
# DWG Import Development Commands

## /dwg-create-converter
Create a new DWG entity converter

**Usage:**
/dwg-create-converter [entity-type] [target-revit-category]

**Examples:**
/dwg-create-converter "Polyline" "Walls"
/dwg-create-converter "Block" "Families"

## /dwg-add-ai-classification
Add AI classification for DWG entities

**Usage:**
/dwg-add-ai-classification [entity-type] [model-type]

**Examples:**
/dwg-add-ai-classification "Layer" "LayoutLM"
/dwg-add-ai-classification "Block" "YOLO"

## /dwg-generate-parser
Generate DWG file parser

**Usage:**
/dwg-generate-parser [file-format] [output-format]

**Examples:**
/dwg-generate-parser "DWG2024" "RevitElements"
```

### **AI Model Commands**

**File:** `.claude/commands/ai-models.md`

```markdown
# AI Model Development Commands

## /ai-create-pipeline
Create ML.NET or ONNX inference pipeline

**Usage:**
/ai-create-pipeline [model-type] [input-output]

**Examples:**
/ai-create-pipeline "YOLOv9" "Image→WallDetections"
/ai-create-pipeline "ML.NET" "ProjectFeatures→CostPrediction"

## /ai-optimize-model
Optimize model for production deployment

**Usage:**
/ai-optimize-model [model-path] [target]

**Examples:**
/ai-optimize-model "yolov9.onnx" "inference-time<200ms"
/ai-optimize-model "cost-model.zip" "accuracy>0.95"

## /ai-generate-training
Generate model training code

**Usage:**
/ai-generate-training [model-type] [dataset]

**Examples:**
/ai-generate-training "WallDetector" "floor-plans-dataset"
```

### **Testing Commands**

**File:** `.claude/commands/testing.md`

```markdown
# Testing Development Commands

## /test-generate-unit
Generate unit tests for a class

**Usage:**
/test-generate-unit [class-name] [coverage]

**Examples:**
/test-generate-unit ParameterMapper 95%
/test-generate-unit DWGImporter 90%

## /test-generate-integration
Generate integration tests for workflow

**Usage:**
/test-generate-integration [workflow-name]

**Examples:**
/test-generate-integration "DWG-Import-Complete-Workflow"
/test-generate-integration "Parameter-Sync-Multi-Model"

## /test-generate-benchmark
Generate performance benchmarks

**Usage:**
/test-generate-benchmark [class-name] [metrics]

**Examples:**
/test-generate-benchmark BatchOperationsEngine "throughput,latency,memory"
```

---

## 🔌 MCP SERVER INTEGRATION

### **MCP Configuration**

**File:** `.claude/mcp.json`

```json
{
  "mcpServers": {
    "revit-api": {
      "command": "node",
      "args": ["mcp-servers/revit-api/index.js"],
      "description": "Revit API documentation and code examples",
      "disabled": false
    },
    "stingbim-database": {
      "command": "node",
      "args": ["mcp-servers/database/index.js"],
      "env": {
        "DATABASE_PATH": "./StingBIM.db"
      },
      "description": "Access StingBIM parameter database",
      "disabled": false
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      },
      "description": "GitHub repository access",
      "disabled": false
    },
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "${PROJECT_ROOT}/Source",
        "${PROJECT_ROOT}/Tests",
        "${PROJECT_ROOT}/Documentation"
      ],
      "description": "Local filesystem access",
      "disabled": false
    }
  }
}
```

### **Custom MCP Server: Revit API**

**File:** `mcp-servers/revit-api/index.js`

```javascript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
} from "@modelcontextprotocol/sdk/types.js";
import fs from "fs";
import path from "path";

// Revit API documentation database
const REVIT_API_DOCS = {
  "Document": {
    description: "Represents a Revit document",
    namespace: "Autodesk.Revit.DB",
    methods: [
      {
        name: "Create.NewWall",
        signature: "Wall Create.NewWall(Document doc, Curve curve, ElementId wallTypeId, ElementId levelId, double height, double offset, bool flip, bool structural)",
        description: "Creates a new wall",
        example: `var wall = Wall.Create(
  doc,
  line,
  wallType.Id,
  level.Id,
  3000,
  0,
  false,
  false
);`
      },
      // ... more methods
    ]
  },
  // ... more classes
};

const server = new Server(
  {
    name: "revit-api-server",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {},
    },
  }
);

// Tool: Search Revit API
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: "search_revit_api",
        description: "Search Revit API documentation and examples",
        inputSchema: {
          type: "object",
          properties: {
            query: {
              type: "string",
              description: "Search query (class name, method, or keyword)",
            },
          },
          required: ["query"],
        },
      },
      {
        name: "get_revit_example",
        description: "Get code example for Revit API usage",
        inputSchema: {
          type: "object",
          properties: {
            task: {
              type: "string",
              description: "Task description (e.g., 'create wall', 'filter elements')",
            },
          },
          required: ["task"],
        },
      },
    ],
  };
});

server.setRequestHandler(CallToolRequestSchema, async (request) => {
  const { name, arguments: args } = request.params;

  if (name === "search_revit_api") {
    const query = args.query.toLowerCase();
    const results = searchRevitAPI(query);
    return {
      content: [
        {
          type: "text",
          text: JSON.stringify(results, null, 2),
        },
      ],
    };
  }

  if (name === "get_revit_example") {
    const example = getRevitExample(args.task);
    return {
      content: [
        {
          type: "text",
          text: example,
        },
      ],
    };
  }

  throw new Error(`Unknown tool: ${name}`);
});

function searchRevitAPI(query) {
  // Search implementation
  const results = [];
  
  for (const [className, classInfo] of Object.entries(REVIT_API_DOCS)) {
    if (className.toLowerCase().includes(query)) {
      results.push({
        class: className,
        description: classInfo.description,
        namespace: classInfo.namespace,
      });
    }
    
    for (const method of classInfo.methods) {
      if (method.name.toLowerCase().includes(query) || 
          method.description.toLowerCase().includes(query)) {
        results.push({
          class: className,
          method: method.name,
          signature: method.signature,
          description: method.description,
          example: method.example,
        });
      }
    }
  }
  
  return results;
}

function getRevitExample(task) {
  // Example generation based on task
  const examples = {
    "create wall": `using Autodesk.Revit.DB;
using Autodesk.Revit.UI;

public void CreateWall(Document doc)
{
    using (Transaction trans = new Transaction(doc, "Create Wall"))
    {
        trans.Start();
        
        // Get level
        Level level = new FilteredElementCollector(doc)
            .OfClass(typeof(Level))
            .FirstElement() as Level;
        
        // Create line
        XYZ start = new XYZ(0, 0, 0);
        XYZ end = new XYZ(10, 0, 0);
        Line line = Line.CreateBound(start, end);
        
        // Get wall type
        WallType wallType = new FilteredElementCollector(doc)
            .OfClass(typeof(WallType))
            .FirstElement() as WallType;
        
        // Create wall
        Wall wall = Wall.Create(
            doc,
            line,
            wallType.Id,
            level.Id,
            3000,  // height in mm
            0,     // offset
            false, // flip
            false  // structural
        );
        
        trans.Commit();
    }
}`,
    // ... more examples
  };
  
  for (const [key, example] of Object.entries(examples)) {
    if (task.toLowerCase().includes(key)) {
      return example;
    }
  }
  
  return "No example found for task: " + task;
}

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("Revit API MCP server running");
}

main().catch((error) => {
  console.error("Server error:", error);
  process.exit(1);
});
```

---

## 🔄 DEVELOPMENT WORKFLOWS

### **Workflow 1: Implementing New Feature**

```bash
# Step 1: Research similar implementations
claude "Search the codebase for similar parameter management features to what I want to implement"

# Step 2: Design the feature
/param-create-class ParameterGenealogySystem "Version control and history tracking for parameters"

# Step 3: Generate tests first (TDD)
/test-generate-unit ParameterGenealogySystem 95%

# Step 4: Implement the feature
claude "Implement ParameterGenealogySystem class with SQLite backend for version storage"

# Step 5: Run tests
claude "Run all tests for ParameterGenealogySystem and fix any failures"

# Step 6: Optimize performance
/param-optimize ParameterGenealogySystem "Retrieve history for 10k parameters in <1 second"

# Step 7: Generate documentation
claude "Generate XML documentation comments for all public methods in ParameterGenealogySystem"

# Step 8: Create pull request
claude "Create a pull request for ParameterGenealogySystem feature with detailed description"
```

### **Workflow 2: Debugging Complex Issue**

```bash
# Step 1: Analyze error logs
claude "Analyze the stack trace and identify the root cause"

# Step 2: Search for similar issues
claude "Search GitHub issues and Stack Overflow for similar errors"

# Step 3: Reproduce the issue
claude "Create a minimal reproduction test case for this bug"

# Step 4: Fix the bug
claude "Implement a fix for the identified issue in ParameterSyncEngine"

# Step 5: Add regression test
claude "Create a regression test to prevent this bug from happening again"

# Step 6: Verify fix
claude "Run all affected tests and verify the fix doesn't break anything"
```

### **Workflow 3: Performance Optimization**

```bash
# Step 1: Profile the code
claude "Profile the BatchOperationsEngine and identify performance bottlenecks"

# Step 2: Generate benchmarks
/test-generate-benchmark BatchOperationsEngine "throughput,latency,memory"

# Step 3: Baseline measurements
claude "Run benchmarks and save baseline measurements"

# Step 4: Optimize hot paths
claude "Optimize the identified bottlenecks in BatchOperationsEngine"

# Step 5: Compare results
claude "Run benchmarks again and compare with baseline"

# Step 6: Document improvements
claude "Generate performance improvement report with before/after metrics"
```

---

## 🔧 CI/CD INTEGRATION

### **GitHub Actions Workflow**

**File:** `.github/workflows/claude-code-ci.yml`

```yaml
name: Claude Code CI/CD

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

env:
  ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
  DOTNET_VERSION: '4.8'

jobs:
  claude-review:
    name: Claude Code Review
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      
      - name: Setup Claude Code
        run: |
          npm install -g @anthropic-ai/claude-code
          claude auth ${{ secrets.ANTHROPIC_API_KEY }}
      
      - name: Run Claude Code Review
        run: |
          claude review \
            --diff "origin/main...HEAD" \
            --output review-report.md \
            --fail-on-issues
      
      - name: Upload Review Report
        uses: actions/upload-artifact@v3
        with:
          name: claude-review-report
          path: review-report.md
      
      - name: Comment PR with Review
        if: github.event_name == 'pull_request'
        uses: actions/github-script@v6
        with:
          script: |
            const fs = require('fs');
            const review = fs.readFileSync('review-report.md', 'utf8');
            
            github.rest.issues.createComment({
              owner: context.repo.owner,
              repo: context.repo.repo,
              issue_number: context.issue.number,
              body: '## 🤖 Claude Code Review\n\n' + review
            });

  claude-test-generation:
    name: Generate Missing Tests
    runs-on: ubuntu-latest
    needs: claude-review
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Claude Code
        run: |
          npm install -g @anthropic-ai/claude-code
          claude auth ${{ secrets.ANTHROPIC_API_KEY }}
      
      - name: Analyze Test Coverage
        run: |
          claude analyze-coverage \
            --source ./Source \
            --tests ./Tests \
            --min-coverage 80 \
            --output coverage-gaps.json
      
      - name: Generate Missing Tests
        run: |
          claude generate-tests \
            --gaps coverage-gaps.json \
            --output ./Tests/Generated \
            --framework xUnit
      
      - name: Create PR with Tests
        if: github.event_name == 'push'
        run: |
          git config --global user.name "Claude Code Bot"
          git config --global user.email "bot@stingbim.com"
          git checkout -b claude-generated-tests
          git add Tests/Generated/
          git commit -m "Add Claude-generated tests for improved coverage"
          git push origin claude-generated-tests
          
          claude create-pr \
            --base main \
            --head claude-generated-tests \
            --title "Claude-Generated Tests" \
            --body "Automatically generated tests to improve code coverage"

  claude-documentation:
    name: Generate Documentation
    runs-on: ubuntu-latest
    needs: claude-review
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Claude Code
        run: |
          npm install -g @anthropic-ai/claude-code
          claude auth ${{ secrets.ANTHROPIC_API_KEY }}
      
      - name: Generate API Documentation
        run: |
          claude generate-docs \
            --source ./Source \
            --output ./Documentation/API \
            --format markdown
      
      - name: Generate User Guide
        run: |
          claude generate-guide \
            --commands ./Source/Commands \
            --output ./Documentation/UserGuide.md \
            --examples ./Examples
      
      - name: Deploy Documentation
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./Documentation

  build-and-test:
    name: Build and Test
    runs-on: windows-latest
    needs: claude-test-generation
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '4.8'
      
      - name: Restore Dependencies
        run: nuget restore StingBIM.sln
      
      - name: Build
        run: msbuild StingBIM.sln /p:Configuration=Release
      
      - name: Run Tests
        run: |
          dotnet test Tests/StingBIM.Tests.csproj \
            --configuration Release \
            --logger "trx;LogFileName=test-results.trx" \
            --collect:"XPlat Code Coverage"
      
      - name: Upload Test Results
        uses: actions/upload-artifact@v3
        with:
          name: test-results
          path: "**/test-results.trx"
      
      - name: Upload Coverage
        uses: codecov/codecov-action@v3
        with:
          files: "**/coverage.cobertura.xml"

  claude-release-notes:
    name: Generate Release Notes
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    needs: build-and-test
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      
      - name: Setup Claude Code
        run: |
          npm install -g @anthropic-ai/claude-code
          claude auth ${{ secrets.ANTHROPIC_API_KEY }}
      
      - name: Generate Release Notes
        run: |
          claude generate-release-notes \
            --from-tag $(git describe --tags --abbrev=0) \
            --to-ref HEAD \
            --output RELEASE_NOTES.md
      
      - name: Create Release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: v${{ github.run_number }}
          release_name: Release v${{ github.run_number }}
          body_path: RELEASE_NOTES.md
          draft: false
          prerelease: false
```

---

## 📊 TESTING AUTOMATION

### **Automated Test Generation**

```bash
# Generate unit tests for all classes
claude "Scan the Source/ directory and generate unit tests for all classes that don't have tests yet. Target 90% coverage."

# Generate integration tests for workflows
claude "Generate integration tests for the complete DWG import workflow including layer mapping, block conversion, and wall creation"

# Generate benchmark tests
claude "Generate BenchmarkDotNet tests for all performance-critical classes with targets from requirements"
```

### **Test Templates**

**Unit Test Template:**

```csharp
// Generated by Claude Code
using Xunit;
using Moq;
using FluentAssertions;

namespace StingBIM.Tests.ParameterManager
{
    public class ParameterInferenceEngineTests
    {
        private readonly Mock<ILLMEngine> _mockLLM;
        private readonly Mock<IParameterDatabase> _mockDatabase;
        private readonly ParameterInferenceEngine _sut;
        
        public ParameterInferenceEngineTests()
        {
            _mockLLM = new Mock<ILLMEngine>();
            _mockDatabase = new Mock<IParameterDatabase>();
            _sut = new ParameterInferenceEngine(_mockLLM.Object, _mockDatabase.Object);
        }
        
        [Fact]
        public async Task InferParameters_WithValidCategory_ReturnsSuggestions()
        {
            // Arrange
            var category = "Walls";
            var context = "office building";
            var expectedSuggestions = new List<ParameterSuggestion>
            {
                new ParameterSuggestion
                {
                    Name = "Fire_Rating",
                    Type = ParameterType.Number,
                    Confidence = 0.95
                }
            };
            
            _mockLLM.Setup(x => x.GenerateSuggestionsAsync(category, context))
                .ReturnsAsync(expectedSuggestions);
            
            // Act
            var result = await _sut.InferParametersAsync(category, context);
            
            // Assert
            result.Should().NotBeNull();
            result.Should().HaveCount(1);
            result[0].Name.Should().Be("Fire_Rating");
            result[0].Confidence.Should().Be(0.95);
        }
        
        [Theory]
        [InlineData("", "context")]
        [InlineData("category", "")]
        [InlineData(null, "context")]
        [InlineData("category", null)]
        public async Task InferParameters_WithInvalidInputs_ThrowsArgumentException(
            string category, 
            string context)
        {
            // Act & Assert
            await Assert.ThrowsAsync<ArgumentException>(
                () => _sut.InferParametersAsync(category, context));
        }
    }
}
```

---

## 📚 DOCUMENTATION GENERATION

### **Automated Documentation**

```bash
# Generate API documentation
claude "Generate comprehensive API documentation from XML comments in all public classes. Include examples and usage notes."

# Generate user guide
claude "Create a user guide for the Parameter Manager module with step-by-step instructions, screenshots, and best practices"

# Generate technical architecture document
claude "Analyze the codebase and generate a technical architecture document explaining the system design, patterns used, and data flow"

# Generate deployment guide
claude "Create a deployment guide with prerequisites, installation steps, configuration, and troubleshooting"
```

---

*StingBIM V2.0 - Claude Code Integration Guide*
*Optimizing Development with AI-Powered Agentic Coding*
