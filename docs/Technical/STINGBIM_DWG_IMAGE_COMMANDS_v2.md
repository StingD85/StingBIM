# STINGBIM V2.0 - DWG-TO-BIM + IMAGE-TO-BIM
## Complete AI Conversion Command Reference
## 150+ Commands for CAD/Image Import with AI Intelligence

**Date:** January 31, 2026  
**Version:** 2.0 DWG/Image Import Edition  
**Platform:** C# .NET Framework 4.8 (Revit Add-in)

---

## 📖 TABLE OF CONTENTS

1. [DWG Import & Analysis](#dwg-import--analysis)
2. [Layer Recognition & Mapping](#layer-recognition--mapping)
3. [Block-to-Family Conversion](#block-to-family-conversion)
4. [Entity-to-Element Conversion](#entity-to-element-conversion)
5. [Annotation Preservation](#annotation-preservation)
6. [Image-to-BIM Integration](#image-to-bim-integration)
7. [Hybrid CAD + Image Workflows](#hybrid-cad--image-workflows)
8. [AI Model Training](#ai-model-training)
9. [Batch Processing](#batch-processing)
10. [Quality Control](#quality-control)

---

## 📥 DWG IMPORT & ANALYSIS

### **dwg-import** - Intelligent DWG Import

**Syntax:**
```bash
dwg-import file=<path> [scale=<auto|1:100|1:50|...>] [layers=<all|filter>] [blocks=<convert|link|ignore>] [annotations=<preserve|ignore>] [ai-classify=true] [preview=true]
```

**Description:**  
Imports AutoCAD DWG files with AI-powered entity classification and intelligent conversion.

**Parameters:**
- `file` - Path to DWG file
- `scale` - Drawing scale (auto-detect or specify)
- `layers` - Layer import strategy
- `blocks` - Block handling strategy
- `annotations` - Annotation handling
- `ai-classify` - Use AI for entity classification
- `preview` - Show preview before import

**Examples:**
```bash
# Basic import with auto-detection
dwg-import file="Floor_Plan.dwg" scale=auto ai-classify=true

# Import with block conversion
dwg-import file="Electrical_Plan.dwg" blocks=convert annotations=preserve

# Selective layer import
dwg-import file="Architectural.dwg" layers=filter scale=1:100 preview=true

# Full conversion with AI
dwg-import file="Complete_Set.dwg" scale=auto layers=all blocks=convert annotations=preserve ai-classify=true
```

**Output:**
```
DWG Import Analysis:

Source File: Floor_Plan.dwg
File Size: 12.5 MB
DWG Version: AutoCAD 2024
Units: Millimeters

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AI ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Scale Detection:
  Title block found: Yes
  Scale indicator: "1:100"
  AI confidence: 98.5%
  Detected scale: 1:100 ✓

Layer Analysis (42 layers detected):
  
  WALLS (Architecture):
    Entities: 485 polylines, 127 lines
    AI Classification: Walls (confidence: 99.2%)
    Suggested Revit category: Walls
    Recommended action: Convert to walls
    
  DOORS (Architecture):
    Entities: 68 blocks
    AI Classification: Doors (confidence: 97.8%)
    Suggested Revit category: Doors
    Recommended action: Convert to door families
    
  WINDOWS (Architecture):
    Entities: 142 blocks
    AI Classification: Windows (confidence: 96.5%)
    Suggested Revit category: Windows
    Recommended action: Convert to window families
    
  FURNITURE (Interiors):
    Entities: 234 blocks
    AI Classification: Furniture (confidence: 94.2%)
    Suggested Revit category: Furniture
    Recommended action: Convert to furniture families
    
  ... (38 more layers)

Block Analysis (512 blocks detected):
  
  Standard Blocks (68):
    DOOR-900: 42 instances → Door family (900mm width)
    DOOR-1200: 26 instances → Door family (1200mm width)
    
  Custom Blocks (234):
    DESK-1400x700: 89 instances → Furniture family
    CHAIR-STD: 145 instances → Furniture family
    
  Title Block (1):
    A0-TITLE: 1 instance → Import as annotation
    
  Symbols (209):
    Various electrical/plumbing symbols
    Recommended: Convert to Revit symbols

Annotation Count:
  Text entities: 847
  Dimensions: 234
  Leaders: 89
  Hatches: 156

Conversion Estimate:
  Walls: 285 walls
  Doors: 68 doors (2 families)
  Windows: 142 windows (4 families)
  Rooms: 48 rooms
  Furniture: 234 items (12 families)
  Annotations: 1,170 items
  
  Total elements: 1,947
  Estimated time: 4.2 minutes
  Success rate estimate: 96.8%

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
IMPORT PREVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Thumbnail image showing detected elements with color coding]

  ■ Walls (green)
  ■ Doors (blue)
  ■ Windows (cyan)
  ■ Furniture (yellow)
  ■ Annotations (white)
  ■ Unclassified (red - 3.2%)

Confidence Distribution:
  High (>95%): 1,884 entities (96.8%)
  Medium (85-95%): 48 entities (2.5%)
  Low (<85%): 15 entities (0.8%)

Proceed with import? [Y/N]
```

---

### **dwg-analyze** - Analyze DWG File

**Syntax:**
```bash
dwg-analyze file=<path> [deep=true] [export-report=<format>]
```

**Description:**  
Analyzes DWG file structure without importing.

**Examples:**
```bash
# Quick analysis
dwg-analyze file="Plan.dwg"

# Deep analysis with report
dwg-analyze file="Complex_Set.dwg" deep=true export-report=pdf

# Analysis for multiple files
dwg-analyze file="Sheet_*.dwg" export-report=xlsx
```

**Output:**
```
DWG File Analysis:

File: Floor_Plan.dwg
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

FILE PROPERTIES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Size: 12.5 MB
DWG Version: AutoCAD 2024 (AC1032)
Created: 2025-11-15 09:30:00
Modified: 2026-01-28 16:45:00
Author: Design Team
Units: Millimeters
Coordinate System: World

STATISTICS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Layers: 42
Blocks: 512
Polylines: 485
Lines: 1,247
Arcs: 234
Circles: 89
Texts: 847
MTexts: 156
Dimensions: 234
Leaders: 89
Hatches: 156
Splines: 34
Xrefs: 3

LAYER BREAKDOWN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Layer Name             | Entities | Color  | Frozen | Locked
─────────────────────────────────────────────────────────────
WALLS                 | 612      | 7      | No     | No
DOORS                 | 68       | 3      | No     | No
WINDOWS               | 142      | 4      | No     | No
FURNITURE             | 234      | 6      | No     | No
ELECTRICAL-LIGHTING   | 89       | 5      | No     | No
PLUMBING-FIXTURES     | 45       | 2      | No     | No
DIMENSIONS            | 234      | 8      | No     | Yes
TEXT                  | 847      | 7      | No     | Yes
HATCHES               | 156      | 9      | No     | No
... (33 more layers)

BLOCK DEFINITIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Block Name            | Instances | Attributes | Complexity
──────────────────────────────────────────────────────────────
DOOR-900             | 42        | 3          | Simple
DOOR-1200            | 26        | 3          | Simple
WINDOW-1200x1500     | 89        | 2          | Simple
WINDOW-900x1200      | 53        | 2          | Simple
DESK-1400x700        | 89        | 1          | Medium
CHAIR-STD            | 145       | 0          | Simple
... (506 more blocks)

XREF ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Structural_Plan.dwg
   Status: Attached
   Path: ./Xrefs/Structural_Plan.dwg
   
2. MEP_Plan.dwg
   Status: Attached
   Path: ./Xrefs/MEP_Plan.dwg
   
3. Site_Plan.dwg
   Status: Missing
   Path: ./Xrefs/Site_Plan.dwg

QUALITY ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Overlapping lines: 23 (needs cleanup)
Duplicate entities: 12 (needs cleanup)
Invalid polylines: 0 ✓
Missing blocks: 0 ✓
Broken dimensions: 3 (needs repair)
Empty layers: 5

CONVERSION READINESS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Score: 87/100 (Good)

Issues:
  ⚠ 23 overlapping lines should be cleaned
  ⚠ 3 broken dimensions need repair
  ⚠ 1 missing xref needs to be resolved
  ✓ Layer naming follows AIA convention
  ✓ No coordinate system issues
  ✓ Scale properly defined

Recommendations:
  1. Run dwg-cleanup to fix overlaps
  2. Repair broken dimensions
  3. Resolve missing xref or remove reference
  
Estimated import success rate: 96.8%
```

---

### **dwg-scale-detect** - Auto-Detect Drawing Scale

**Syntax:**
```bash
dwg-scale-detect file=<path> [method=<ai|titleblock|dimension>] [confidence-threshold=0.85]
```

**Description:**  
Uses AI to automatically detect drawing scale from various indicators.

**Examples:**
```bash
# AI-based detection
dwg-scale-detect file="Plan.dwg" method=ai

# Title block detection
dwg-scale-detect file="Sheet.dwg" method=titleblock

# Multi-method detection
dwg-scale-detect file="Complex.dwg" method=all confidence-threshold=0.90
```

**Output:**
```
Scale Detection Analysis:

File: Floor_Plan.dwg

METHOD 1: AI SCALE DETECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AI Model: LayoutLMv3 + Custom OCR
Processing time: 1.2 seconds

Title Block Analysis:
  Title block detected: Yes (A0 format)
  Location: Lower right corner
  
  Text extraction:
    "SCALE: 1:100" (confidence: 98.5%)
    "DRAWN TO SCALE 1/100" (confidence: 92.3%)
    "1:100" in scale box (confidence: 99.1%)
  
  Conclusion: 1:100
  Confidence: 98.5% (HIGH)

METHOD 2: DIMENSION ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Dimensions analyzed: 234

Sample measurements:
  Dimension text: "4200"
  Line length in drawing: 42mm
  Implied scale: 1:100
  
  Dimension text: "3600"
  Line length in drawing: 36mm
  Implied scale: 1:100
  
  Dimension text: "7200"
  Line length in drawing: 72mm
  Implied scale: 1:100

Consistency check: 234/234 dimensions match (100%)
  
Conclusion: 1:100
Confidence: 99.8% (VERY HIGH)

METHOD 3: FEATURE SIZE ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Known features detected:
  - Standard door width: 900mm
    Drawing width: 9mm
    Implied scale: 1:100
    
  - Room dimensions: ~4200x3600mm
    Drawing size: 42x36mm
    Implied scale: 1:100
    
  - Wall thickness: 200mm
    Drawing thickness: 2mm
    Implied scale: 1:100

Conclusion: 1:100
Confidence: 96.2% (HIGH)

FINAL RESULT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Detected Scale: 1:100

Confidence Summary:
  AI Title Block: 98.5%
  Dimension Analysis: 99.8%
  Feature Analysis: 96.2%
  
  Overall Confidence: 98.2% (VERY HIGH)

Recommendation: Use 1:100 scale for import

Alternative scales detected: None
Conflicts: None

Status: ✓ Scale detection successful
```

---

## 🗺️ LAYER RECOGNITION & MAPPING

### **dwg-layers-analyze** - Analyze Layer Structure

**Syntax:**
```bash
dwg-layers-analyze file=<path> [convention=<aia|bs1192|iso13567|auto>] [ai-classify=true]
```

**Description:**  
Analyzes DWG layers and suggests Revit category mappings.

**Examples:**
```bash
# Auto-detect convention
dwg-layers-analyze file="Plan.dwg" convention=auto

# AIA layer standards
dwg-layers-analyze file="US_Project.dwg" convention=aia ai-classify=true

# British standards
dwg-layers-analyze file="UK_Project.dwg" convention=bs1192
```

**Output:**
```
Layer Analysis:

File: Floor_Plan.dwg
Convention: AIA (auto-detected)
Total Layers: 42

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LAYER CLASSIFICATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AIA Standard Layers (28):

A-WALL (Architecture - Walls):
  Entities: 612 (485 polylines, 127 lines)
  AI Classification: Walls (99.2% confidence)
  Revit Category: Walls
  Mapping: ✓ Automatic
  Wall Type Detection:
    - Exterior walls: 142 entities (thickness ≥200mm)
    - Interior walls: 470 entities (thickness <200mm)
  
A-DOOR (Architecture - Doors):
  Entities: 68 blocks
  AI Classification: Doors (97.8% confidence)
  Revit Category: Doors
  Mapping: ✓ Automatic
  Door Type Detection:
    - Single doors: 42 blocks (DOOR-900)
    - Double doors: 26 blocks (DOOR-1200)
  
A-WIND (Architecture - Windows):
  Entities: 142 blocks
  AI Classification: Windows (96.5% confidence)
  Revit Category: Windows
  Mapping: ✓ Automatic
  Window Type Detection:
    - Standard windows: 89 blocks (1200x1500)
    - Small windows: 53 blocks (900x1200)
  
A-FLOR-FNSH (Architecture - Floor Finishes):
  Entities: 156 hatches
  AI Classification: Floor materials (94.8% confidence)
  Revit Category: Floors
  Mapping: ✓ Automatic
  Material Detection:
    - Tile: 67 hatches (ANSI31 pattern)
    - Carpet: 45 hatches (AR-SAND pattern)
    - Wood: 44 hatches (AR-WOOD pattern)
  
... (24 more AIA layers)

Custom Layers (14):

FURNITURE (Non-standard):
  Entities: 234 blocks
  AI Classification: Furniture (94.2% confidence)
  Revit Category: Furniture
  Mapping: ⚠ Manual review recommended
  
ELECTRICAL-LIGHTING (Non-standard):
  Entities: 89 blocks
  AI Classification: Lighting Fixtures (92.5% confidence)
  Revit Category: Lighting Fixtures
  Mapping: ⚠ Manual review recommended
  
... (12 more custom layers)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MAPPING RECOMMENDATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Automatic Mappings (28 layers):
  DWG Layer → Revit Category

  A-WALL → Walls
  A-DOOR → Doors
  A-WIND → Windows
  A-FLOR → Floors
  A-CLNG → Ceilings
  A-ROOF → Roofs
  ... (22 more)

Manual Review Required (14 layers):
  Layer | Reason | Suggested Action
  ───────────────────────────────────────────────────
  FURNITURE | Non-standard name | Map to Furniture
  ELEC-LIGHT | Non-standard name | Map to Lighting Fixtures
  ... (12 more)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Total Layers: 42
  - AIA Standard: 28 (66.7%)
  - Custom: 14 (33.3%)

Mapping Confidence:
  - High (>95%): 28 layers
  - Medium (85-95%): 12 layers
  - Low (<85%): 2 layers

Recommended Actions:
  1. Accept 28 automatic mappings
  2. Review 14 custom layer mappings
  3. Verify 2 low-confidence layers

Next Steps:
  - Run: dwg-layers-map to apply mappings
  - Or: dwg-layers-edit to modify mappings manually
```

---

### **dwg-layers-map** - Create Layer Mappings

**Syntax:**
```bash
dwg-layers-map file=<path> [mapping-file=<path>] [auto=true] [save-template=true]
```

**Description:**  
Creates DWG layer to Revit category mappings.

**Examples:**
```bash
# Auto-generate mappings
dwg-layers-map file="Plan.dwg" auto=true

# Use custom mapping file
dwg-layers-map file="Plan.dwg" mapping-file="custom_mappings.json"

# Create and save template
dwg-layers-map file="Plan.dwg" auto=true save-template=true
```

**Output:**
```
Layer Mapping:

Source File: Floor_Plan.dwg
Mapping Strategy: Automatic (AI-powered)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MAPPING TABLE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

DWG Layer          | Revit Category       | Confidence | Status
─────────────────────────────────────────────────────────────────
A-WALL            | Walls                | 99.2%      | ✓ Auto
A-WALL-EXT        | Walls (Exterior)     | 98.5%      | ✓ Auto
A-WALL-INT        | Walls (Interior)     | 98.8%      | ✓ Auto
A-DOOR            | Doors                | 97.8%      | ✓ Auto
A-DOOR-EXT        | Doors (Exterior)     | 96.5%      | ✓ Auto
A-WIND            | Windows              | 96.5%      | ✓ Auto
A-FLOR            | Floors               | 95.2%      | ✓ Auto
A-FLOR-FNSH       | Floors (Finish)      | 94.8%      | ✓ Auto
A-CLNG            | Ceilings             | 96.8%      | ✓ Auto
A-ROOF            | Roofs                | 97.2%      | ✓ Auto
FURNITURE         | Furniture            | 94.2%      | ⚠ Review
ELECTRICAL-LIGHT  | Lighting Fixtures    | 92.5%      | ⚠ Review
PLUMBING-FIX      | Plumbing Fixtures    | 93.8%      | ⚠ Review
... (29 more mappings)

Summary:
  Total mappings: 42
  Automatic: 28 (confidence >95%)
  Manual review: 14 (confidence 85-95%)
  Failed: 0

Mapping file saved: Floor_Plan_mappings.json

Template saved: AIA_Standard_Mappings.json
  (Can be reused for similar projects)

Apply mappings during import? [Y/N]
```

---

## 🏗️ BLOCK-TO-FAMILY CONVERSION

### **dwg-blocks-convert** - Convert Blocks to Families

**Syntax:**
```bash
dwg-blocks-convert file=<path> [blocks=<all|filter>] [template-selection=<auto|manual>] [preserve-attributes=true] [create-library=true]
```

**Description:**  
Converts DWG blocks to Revit family files with intelligent template selection.

**Examples:**
```bash
# Convert all blocks
dwg-blocks-convert file="Plan.dwg" blocks=all template-selection=auto

# Convert specific blocks
dwg-blocks-convert file="Furniture.dwg" blocks="DESK*,CHAIR*" preserve-attributes=true

# Create family library
dwg-blocks-convert file="Symbols.dwg" create-library=true
```

**Output:**
```
Block to Family Conversion:

Source File: Floor_Plan.dwg
Blocks Found: 512
Unique Block Definitions: 24

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AI BLOCK CLASSIFICATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Analyzing block geometry and attributes...
[████████████████████████████████] 100%

Block: DOOR-900 (42 instances)
  Classification: Door family
  Confidence: 99.1%
  Template: Generic Model.rft → Door (Metric).rft ✓
  Width: 900mm (from block name and geometry)
  Height: 2100mm (from geometry)
  Swing: Right-hand (from arc geometry)
  Attributes:
    - MARK → Mark parameter
    - TYPE → Type Mark parameter
    - FIRE_RATING → Fire Rating parameter
  Conversion: Ready ✓

Block: WINDOW-1200x1500 (89 instances)
  Classification: Window family
  Confidence: 98.3%
  Template: Window (Metric).rft ✓
  Width: 1200mm (from block name)
  Height: 1500mm (from block name)
  Sill height: 900mm (from insertion point)
  Attributes:
    - MARK → Mark parameter
    - GLAZING_TYPE → Glazing Type parameter
  Conversion: Ready ✓

Block: DESK-1400x700 (89 instances)
  Classification: Furniture family
  Confidence: 96.5%
  Template: Furniture (Metric).rft ✓
  Length: 1400mm
  Width: 700mm
  Height: 750mm
  Attributes:
    - DEPARTMENT → Department parameter
  Conversion: Ready ✓

Block: CHAIR-STD (145 instances)
  Classification: Furniture family
  Confidence: 95.8%
  Template: Furniture (Metric).rft ✓
  Width: 600mm
  Depth: 600mm
  Height: 900mm
  Conversion: Ready ✓

... (20 more blocks)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CONVERSION PROCESS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Converting blocks to families...

[Step 1/4] Creating family documents
  [████████████████████████████████] 24/24
  Time: 8.5 seconds

[Step 2/4] Converting geometry
  Converting DOOR-900...
    - Lines: 12 → Model lines
    - Arcs: 2 → Model arcs (swing)
    - Insertion point: Reference plane
  
  Converting WINDOW-1200x1500...
    - Rectangles: 2 → Extrusions
    - Lines: 8 → Model lines (mullions)
    - Hatches: Converted to filled regions
  
  Converting DESK-1400x700...
    - Solid geometry: 3D extrusion
    - Detail lines: Preserved
  
  [████████████████████████████████] 24/24
  Time: 45.2 seconds

[Step 3/4] Converting attributes to parameters
  Creating shared parameters...
  Mapping block attributes...
  [████████████████████████████████] 24/24
  Time: 6.8 seconds

[Step 4/4] Loading families into project
  Loading DOOR-900.rfa...
  Loading WINDOW-1200x1500.rfa...
  Loading DESK-1400x700.rfa...
  [████████████████████████████████] 24/24
  Time: 12.3 seconds

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
INSTANCE PLACEMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Placing family instances at original block locations...
[████████████████████████████████] 512/512

Placement Summary:
  Doors: 68 placed (2 families)
  Windows: 142 placed (2 families)
  Furniture: 234 placed (10 families)
  Fixtures: 68 placed (10 families)
  
  Total instances: 512
  Successful: 512 (100%)
  Failed: 0

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FAMILY LIBRARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Families saved to: C:\StingBIM\Libraries\Converted_Families\

Doors/
  ├── DOOR-900.rfa
  └── DOOR-1200.rfa

Windows/
  ├── WINDOW-1200x1500.rfa
  └── WINDOW-900x1200.rfa

Furniture/
  ├── DESK-1400x700.rfa
  ├── DESK-1200x600.rfa
  ├── CHAIR-STD.rfa
  ... (7 more)

Fixtures/
  ├── SINK-SINGLE.rfa
  ├── TOILET-STD.rfa
  ... (8 more)

Total families created: 24
Library size: 85.6 MB

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Conversion Time: 1 minute 12 seconds
Success Rate: 100%

Quality Metrics:
  Geometry accuracy: 99.8%
  Attribute preservation: 100%
  Placement accuracy: 100%

Status: ✓ Block conversion completed successfully
```

---

## 🔄 ENTITY-TO-ELEMENT CONVERSION

### **dwg-walls-create** - Convert Polylines to Walls

**Syntax:**
```bash
dwg-walls-create file=<path> [layer=<layer_name>] [wall-type=<auto|specify>] [height=<auto|value>] [detect-rooms=true]
```

**Description:**  
Converts DWG polylines and lines to Revit walls with intelligent type assignment.

**Examples:**
```bash
# Auto-detect everything
dwg-walls-create file="Plan.dwg" layer="A-WALL" wall-type=auto height=auto

# Specific wall type and height
dwg-walls-create file="Plan.dwg" layer="A-WALL-EXT" wall-type="Exterior - Brick" height=3000

# Create walls and detect rooms
dwg-walls-create file="Plan.dwg" detect-rooms=true
```

**Output:**
```
Wall Creation from DWG:

Source File: Floor_Plan.dwg
Layer: A-WALL
Polylines/Lines: 612

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WALL TYPE DETECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Analyzing polyline thicknesses...

Thickness Distribution:
  200mm: 142 polylines (23.2%) → Exterior walls
  150mm: 285 polylines (46.6%) → Interior partitions
  100mm: 185 polylines (30.2%) → Light partitions

Wall Type Assignments:
  Exterior - 200mm Brick: 142 polylines
  Interior - 150mm Block: 285 polylines
  Interior - 100mm Stud: 185 polylines

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HEIGHT DETECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Analyzing floor plan context...

Level Detection:
  Base level: Level 1 (elevation: 0mm)
  Top level: Level 2 (elevation: 3000mm)
  
  Default wall height: 3000mm
  
Special Cases:
  - Parapet walls: 4200mm (detected from context)
  - Low partition: 1200mm (detected from thickness <100mm)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WALL CREATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Creating walls from polylines...
[████████████████████████████████] 612/612

Walls Created:
  Exterior walls: 142
  Interior partitions: 285
  Light partitions: 185
  
  Total: 612 walls
  Total length: 2,847 meters

Cleanup Operations:
  - Joined wall ends: 485 connections
  - Merged collinear walls: 23 walls
  - Cleaned up overlaps: 8 overlaps

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROOM DETECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Detecting closed polylines for room boundaries...

Closed Polylines: 48
Room Creation: 48 rooms

Room Sample:
  Room 1: 4200 x 3600mm (15.12 m²)
  Room 2: 3600 x 3000mm (10.80 m²)
  Room 3: 7200 x 4800mm (34.56 m²)
  ... (45 more)

Total Room Area: 687.5 m²

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Conversion Time: 18.5 seconds
Success Rate: 100%

Elements Created:
  Walls: 612
  Rooms: 48
  
Quality:
  Wall placement accuracy: ±1mm
  Join success rate: 100%
  
Status: ✓ Wall creation completed successfully
```

---

*[Document continues with 100+ more commands for annotations, hybrid workflows, AI training, batch processing, and quality control...]*

---

## 🎯 COMPLETE WORKFLOW EXAMPLES

### **Workflow 1: Complete Floor Plan Import**

```bash
# Step 1: Analyze DWG file
dwg-analyze file="Floor_Plan_L02.dwg" deep=true

# Step 2: Detect and verify scale
dwg-scale-detect file="Floor_Plan_L02.dwg" method=ai

# Step 3: Analyze layers
dwg-layers-analyze file="Floor_Plan_L02.dwg" convention=auto ai-classify=true

# Step 4: Create layer mappings
dwg-layers-map file="Floor_Plan_L02.dwg" auto=true save-template=true

# Step 5: Import DWG with full conversion
dwg-import file="Floor_Plan_L02.dwg" 
           scale=1:100 
           layers=all 
           blocks=convert 
           annotations=preserve 
           ai-classify=true

# Step 6: Create walls from polylines
dwg-walls-create file="Floor_Plan_L02.dwg" detect-rooms=true

# Step 7: Convert blocks to families
dwg-blocks-convert file="Floor_Plan_L02.dwg" 
                   blocks=all 
                   create-library=true

# Step 8: Preserve annotations
dwg-annotations-convert file="Floor_Plan_L02.dwg" 
                        types="text,dimensions,leaders"

# Step 9: Quality control
dwg-validate-conversion report=pdf

# Step 10: Export results
conversion-report-generate export=pdf
```

### **Workflow 2: Hybrid Image + DWG Import**

```bash
# Step 1: Import scanned floor plan image
image-import file="Scanned_Plan.jpg" scale=auto

# Step 2: AI detection on image
image-detect-walls confidence=0.90

# Step 3: Import DWG overlay
dwg-import file="Original_CAD.dwg" scale=1:100 preview=true

# Step 4: Hybrid calibration (align DWG with image)
hybrid-calibrate image="Scanned_Plan.jpg" dwg="Original_CAD.dwg" 
                 method=feature-matching

# Step 5: Cross-reference validation
hybrid-validate compare="image,dwg" highlight-differences=true

# Step 6: Merge results (use DWG precision, image context)
hybrid-merge source-priority="dwg" 
             fill-gaps-from="image"
             confidence-threshold=0.85

# Step 7: Final conversion
convert-to-revit merged-result optimize=true
```

---

*StingBIM V2.0 - DWG-to-BIM + Image-to-BIM Complete Reference*
*150+ Commands for Intelligent CAD/Image Conversion*
