# STINGBIM V2.0 - DWG-TO-BIM AI CONVERSION
## Complete Command Reference & Technical Guide
## Intelligent CAD Import with Computer Vision

**Date:** January 31, 2026  
**Version:** 2.0 DWG-to-BIM Edition  
**Platform:** C# .NET Framework 4.8 + ONNX Runtime + netDXF

---

## 📖 TABLE OF CONTENTS

1. [DWG Import Commands](#dwg-import-commands)
2. [Layer Management](#layer-management)
3. [Block Conversion](#block-conversion)
4. [Annotation Processing](#annotation-processing)
5. [Room Detection](#room-detection)
6. [Advanced AI Features](#advanced-ai-features)
7. [Hybrid Image+DWG Workflows](#hybrid-imagedwg-workflows)
8. [Batch Processing](#batch-processing)
9. [Quality Control](#quality-control)
10. [Technical Reference](#technical-reference)

---

## 🎨 DWG IMPORT COMMANDS

### **dwg-import** - Import DWG File

**Syntax:**
```bash
dwg-import file=<path> [scale=<auto|1:50|1:100|custom>] [origin=<x,y,z>] [rotation=<degrees>] [layers=<layer1,layer2,...>] [convert-blocks=true] [ai-enhanced=true]
```

**Description:**  
Imports AutoCAD DWG file with intelligent layer mapping and AI-powered entity recognition.

**Parameters:**
- `file` - DWG file path
- `scale` - Scale detection method (default: auto)
- `origin` - Import origin point (default: 0,0,0)
- `rotation` - Rotation angle in degrees (default: 0)
- `layers` - Specific layers to import (default: all)
- `convert-blocks` - Convert blocks to families (default: true)
- `ai-enhanced` - Use AI for classification (default: true)

**Examples:**
```bash
# Simple import with auto-detection
dwg-import file="Floor_Plan.dwg"

# Import specific layers
dwg-import file="Site_Plan.dwg" layers="WALLS,DOORS,WINDOWS"

# Import with custom scale
dwg-import file="Detail.dwg" scale="1:20"

# Import without block conversion
dwg-import file="Reference.dwg" convert-blocks=false

# Full control import
dwg-import file="Plan.dwg" scale=auto origin="0,0,0" rotation=90 ai-enhanced=true
```

**Output:**
```
╔════════════════════════════════════════════════════════════════╗
║              STINGBIM DWG-TO-BIM AI IMPORT                      ║
╚════════════════════════════════════════════════════════════════╝

[1/7] Loading DWG File...
  File: Floor_Plan.dwg
  Size: 12.4 MB
  Version: AutoCAD 2024
  Units: Millimeters
  Status: ✓ Loaded successfully

[2/7] Analyzing DWG Structure...
  Layers found: 45
  Blocks found: 128
  Entities found: 12,450
  Text objects: 850
  Dimensions: 420
  
  Layer Classification (AI):
    WALLS → Walls (confidence: 99.2%)
    DOORS → Doors (confidence: 98.5%)
    WINDOWS → Windows (confidence: 97.8%)
    FURNITURE → Furniture (confidence: 96.3%)
    ELECTRICAL → Electrical Fixtures (confidence: 95.7%)
    ... (40 more layers)

[3/7] Detecting Scale...
  Title block found: Yes
  Scale notation: "1:100"
  Drawing units: mm
  Calculated scale: 1:100
  Validation: ✓ Confirmed
  
[4/7] Converting Entities...
  
  Walls:
    [██████████████████████] 100% (285 polylines)
    Created: 285 walls
    Average accuracy: 99.2%
    
  Doors:
    [██████████████████████] 100% (68 blocks)
    Created: 68 door instances
    Families created: 12
    Average accuracy: 98.5%
    
  Windows:
    [██████████████████████] 100% (142 blocks)
    Created: 142 window instances
    Families created: 8
    Average accuracy: 97.8%
    
  Rooms:
    [██████████████████████] 100% (48 spaces)
    Detected: 48 rooms
    Room boundaries: 48
    Room labels: 46 (96%)
    
  Furniture:
    [██████████████████████] 100% (95 blocks)
    Created: 95 furniture instances
    Families created: 24
    
[5/7] Processing Annotations...
  Text notes: 850 → 842 converted (99%)
  Dimensions: 420 → 415 converted (99%)
  Leaders: 125 → 123 converted (98%)
  
[6/7] Quality Control...
  
  Validation Checks:
    ✓ No overlapping walls
    ✓ All doors have host walls
    ✓ All windows have host walls
    ✓ Room boundaries closed
    ⚠ 3 rooms missing labels
    ⚠ 12 dimensions couldn't be converted
    
  Accuracy Metrics:
    Wall placement: 99.2% accurate
    Door placement: 98.5% accurate
    Window placement: 97.8% accurate
    Room detection: 96% accurate
    
[7/7] Finalizing Import...
  
  Import Summary:
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Category         │ DWG      │ Revit    │ Success
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    Walls            │ 285      │ 285      │ 100%
    Doors            │ 68       │ 68       │ 100%
    Windows          │ 142      │ 142      │ 100%
    Rooms            │ 48       │ 48       │ 100%
    Furniture        │ 95       │ 95       │ 100%
    Text Notes       │ 850      │ 842      │ 99%
    Dimensions       │ 420      │ 415      │ 99%
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    TOTAL            │ 1,908    │ 1,895    │ 99.3%
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  
  Processing Time:
    Analysis: 1.2 seconds
    AI inference: 2.8 seconds
    Conversion: 8.5 seconds
    Validation: 1.5 seconds
    Total: 14.0 seconds
    
  Performance:
    Average: 136 elements/second
    Peak GPU utilization: 87%
    
Status: ✓ Import completed successfully

Warnings (3):
  1. 3 rooms missing labels - review room names
  2. 12 dimensions couldn't be converted - manual review required
  3. 2 blocks had low confidence (<90%) - verify placement

Report saved: DWG_Import_Report_20260131_145030.pdf
```

---

### **dwg-analyze** - Analyze DWG Structure

**Syntax:**
```bash
dwg-analyze file=<path> [detailed=true] [export-report=true]
```

**Description:**  
Analyzes DWG file structure and provides recommendations before import.

**Examples:**
```bash
# Quick analysis
dwg-analyze file="Floor_Plan.dwg"

# Detailed analysis with report
dwg-analyze file="Complex_Plan.dwg" detailed=true export-report=true
```

**Output:**
```
DWG File Analysis Report:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE INFORMATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
File: Floor_Plan.dwg
Size: 12.4 MB
Version: AutoCAD 2024
Created: 2026-01-15 10:30:00
Modified: 2026-01-30 16:45:00
Units: Millimeters
Bounds: (0, 0) to (25000, 18000)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LAYER ANALYSIS (45 layers)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Standard Layers (AIA Convention):
  ✓ A-WALL - Architectural walls (285 entities)
  ✓ A-DOOR - Doors (68 entities)
  ✓ A-WIND - Windows (142 entities)
  ✓ A-GLAZ - Glazing (48 entities)
  ✓ A-FURN - Furniture (95 entities)
  ✓ A-FLOR - Floor patterns (12 entities)
  
Custom Layers (Non-standard):
  ⚠ WALLS_INTERNAL - Internal walls (120 entities)
    Recommendation: Rename to A-WALL-INTL
    
  ⚠ EXT_WALLS - External walls (85 entities)
    Recommendation: Rename to A-WALL-EXTL
    
  ⚠ DOORS-FIRE - Fire-rated doors (24 entities)
    Recommendation: Use A-DOOR with attribute
    
Frozen/Off Layers:
  ⚠ CONSTRUCTION - 45 entities (will be skipped)
  ⚠ REFERENCE - 120 entities (will be skipped)
  
Empty Layers: 8
  (Can be safely ignored)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BLOCK ANALYSIS (128 unique blocks)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Doors (12 types):
  DOOR_900x2100 - 45 instances
  DOOR_800x2100 - 18 instances
  DOOR_1200x2100 - 5 instances
  ... (9 more)
  
  Attributes found:
    - DOOR_NUMBER (text)
    - FIRE_RATING (text)
    - MANUFACTURER (text)
  
  Conversion confidence: 98.5%
  Recommended family template: Generic Door

Windows (8 types):
  WINDOW_1200x1500 - 85 instances
  WINDOW_900x1200 - 42 instances
  WINDOW_600x900 - 15 instances
  ... (5 more)
  
  Attributes found:
    - WINDOW_TYPE (text)
    - GLAZING (text)
  
  Conversion confidence: 97.8%
  Recommended family template: Generic Window

Furniture (24 types):
  DESK_1800x900 - 35 instances
  CHAIR_OFFICE - 120 instances
  TABLE_CONFERENCE_3000 - 8 instances
  ... (21 more)
  
  Conversion confidence: 96.3%
  Recommended family template: Generic Furniture

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ENTITY ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Polylines: 485
  Closed: 333 (likely walls/rooms)
  Open: 152 (likely walls/details)
  
Lines: 8,450
  Likely use: Detail lines
  
Arcs/Circles: 2,140
  Likely use: Curved walls, details
  
Text (MTEXT): 650
  Font: Arial
  Heights: 2.5mm, 3.5mm, 5mm
  
Text (TEXT): 200
  Font: Romans
  Heights: 2.5mm, 3mm
  
Dimensions: 420
  Linear: 385
  Aligned: 25
  Angular: 10
  
Hatches: 95
  Pattern "ANSI31" (concrete): 45
  Pattern "AR-CONC" (concrete): 30
  Pattern "SOLID" (fills): 20

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SCALE DETECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Title Block Found: Yes
  Location: (1000, 500)
  Size: 297mm x 210mm (A4)
  
Scale Notation Found: Yes
  Text: "SCALE 1:100"
  Location: (1050, 520)
  Confidence: 99.5%
  
Calculated Scale: 1:100
  Method: Title block notation
  Validation: ✓ Consistent with drawing size
  
Drawing Units: Millimeters
Real-world dimensions: 25m x 18m

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROOM DETECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Closed Polylines: 48 potential rooms
Room Labels Found: 46 (96%)

Sample Rooms:
  1. "OFFICE 201" - 15.2 m² (3.8m × 4.0m)
  2. "CONFERENCE 202" - 42.5 m² (6.5m × 6.5m)
  3. "CORRIDOR" - 85.0 m² (25.0m × 3.4m)
  ... (45 more)
  
Missing Labels: 2 rooms
  - Room at (8500, 4200) - 12.5 m²
  - Room at (12000, 9800) - 8.5 m²

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUALITY ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Drawing Quality: EXCELLENT (Score: 92/100)

✓ Strengths:
  - Standard layer naming (AIA)
  - Consistent block usage
  - Clear scale notation
  - Complete title block
  - Proper dimensioning
  - Closed room boundaries
  
⚠ Areas for Improvement:
  - Some non-standard layer names (3 layers)
  - 2 rooms missing labels
  - 8 empty layers (cleanup recommended)
  
Conversion Readiness: HIGH
Expected accuracy: 99%+

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECOMMENDATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Before Import:
  1. Rename non-standard layers to AIA convention
  2. Add labels to 2 rooms without names
  3. Purge 8 empty layers (optional)
  4. Turn on frozen layers if needed
  
Import Settings:
  Recommended command:
  dwg-import file="Floor_Plan.dwg" 
             scale=auto 
             convert-blocks=true 
             ai-enhanced=true
             
Expected Results:
  Elements to create: ~1,900
  Estimated time: 12-15 seconds
  Expected accuracy: 99.3%

Report saved: DWG_Analysis_Report_20260131.pdf
```

---

## 📋 LAYER MANAGEMENT

### **dwg-layers-map** - Map DWG Layers to Revit Categories

**Syntax:**
```bash
dwg-layers-map file=<path> [auto-detect=true] [save-mapping=true] [mapping-file=<path>]
```

**Description:**  
Creates or loads layer-to-category mapping for DWG import.

**Examples:**
```bash
# Auto-detect layer mapping
dwg-layers-map file="Plan.dwg" auto-detect=true save-mapping=true

# Load custom mapping
dwg-layers-map file="Plan.dwg" mapping-file="custom_mapping.json"
```

**Output:**
```
Layer Mapping Configuration:

DWG File: Floor_Plan.dwg
Layers: 45
Auto-Detection: Enabled

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AUTOMATIC LAYER MAPPING (AI-Powered)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Standard AIA Layers (Automatic):
  A-WALL      → Walls           (Confidence: 99.8%)
  A-DOOR      → Doors           (Confidence: 99.5%)
  A-WIND      → Windows         (Confidence: 99.2%)
  A-FURN      → Furniture       (Confidence: 98.7%)
  A-GLAZ      → Curtain Panels  (Confidence: 98.2%)
  A-FLOR      → Floors          (Confidence: 97.5%)
  A-CLNG      → Ceilings        (Confidence: 97.0%)
  
Custom Layers (AI Classification):
  WALLS_INT   → Walls           (Confidence: 95.2%)
  WALLS_EXT   → Walls           (Confidence: 94.8%)
  ELEC_POWER  → Electrical Fix. (Confidence: 96.5%)
  PLUMB_FIXT  → Plumbing Fix.   (Confidence: 95.8%)
  
Annotation Layers:
  A-ANNO-TEXT → Text Notes      (Confidence: 99.0%)
  A-ANNO-DIMS → Dimensions      (Confidence: 98.5%)
  A-ANNO-SYMB → Generic Annot.  (Confidence: 97.2%)
  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MANUAL REVIEW REQUIRED (Low Confidence)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Layer: MISC_01
  AI Suggestion: Generic Models (Confidence: 62%)
  Entities: 45 lines, 12 polylines
  Recommended action: Manual classification
  
Layer: TEMP_LAYER
  AI Suggestion: Skip import (Confidence: 85%)
  Entities: 8 text objects
  Recommended action: Exclude from import

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MAPPING SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Total Layers: 45
Automatically Mapped: 41 (91%)
Manual Review Required: 2 (4%)
Recommended to Skip: 2 (4%)

Revit Categories:
  Walls: 5 layers
  Doors: 1 layer
  Windows: 1 layer
  Furniture: 3 layers
  Electrical Fixtures: 2 layers
  Plumbing Fixtures: 2 layers
  ... (8 more categories)

Save mapping? [Y/N]: Y
Mapping saved: Floor_Plan_mapping.json

Next Steps:
  1. Review 2 layers with low confidence
  2. Run: dwg-import file="Floor_Plan.dwg" mapping="Floor_Plan_mapping.json"
```

---

### **dwg-layers-edit** - Edit Layer Mapping

**Syntax:**
```bash
dwg-layers-edit mapping=<path> layer=<name> category=<category>
```

**Description:**  
Edits layer-to-category mapping.

**Examples:**
```bash
# Change layer mapping
dwg-layers-edit mapping="Floor_Plan_mapping.json" layer="MISC_01" category="Generic Models"

# Map to skip
dwg-layers-edit mapping="Floor_Plan_mapping.json" layer="TEMP_LAYER" category="SKIP"
```

---

## 🏢 BLOCK CONVERSION

### **dwg-blocks-convert** - Convert Blocks to Families

**Syntax:**
```bash
dwg-blocks-convert file=<path> [blocks=<block1,block2,...>] [auto-classify=true] [create-types=true] [preserve-attributes=true]
```

**Description:**  
Converts DWG blocks to Revit families with intelligent classification.

**Examples:**
```bash
# Convert all blocks
dwg-blocks-convert file="Plan.dwg"

# Convert specific blocks
dwg-blocks-convert file="Plan.dwg" blocks="DOOR_900,WINDOW_1200"

# Manual classification
dwg-blocks-convert file="Plan.dwg" auto-classify=false
```

**Output:**
```
Block-to-Family Conversion:

DWG File: Floor_Plan.dwg
Blocks Found: 128 unique blocks
Total Instances: 530

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AI BLOCK CLASSIFICATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Doors (12 blocks, 68 instances):
  
  DOOR_900x2100 (45 instances)
    Classification: Door Family
    Confidence: 99.2%
    Attributes: DOOR_NUMBER, FIRE_RATING, MANUFACTURER
    Suggested Family: Single-Flush Door
    Width: 900mm, Height: 2100mm
    
  DOOR_800x2100 (18 instances)
    Classification: Door Family
    Confidence: 98.8%
    Attributes: DOOR_NUMBER, FIRE_RATING
    Suggested Family: Single-Flush Door
    Width: 800mm, Height: 2100mm
    
  ... (10 more door blocks)
  
Windows (8 blocks, 142 instances):
  
  WINDOW_1200x1500 (85 instances)
    Classification: Window Family
    Confidence: 98.5%
    Attributes: WINDOW_TYPE, GLAZING
    Suggested Family: Fixed Window
    Width: 1200mm, Height: 1500mm
    
  ... (7 more window blocks)
  
Furniture (24 blocks, 95 instances):
  
  DESK_1800x900 (35 instances)
    Classification: Furniture Family
    Confidence: 97.2%
    Suggested Family: Table-Desk
    Dimensions: 1800mm × 900mm × 750mm
    
  CHAIR_OFFICE (120 instances)
    Classification: Furniture Family
    Confidence: 96.8%
    Suggested Family: Seating-Chair
    Dimensions: 600mm × 600mm × 900mm
    
  ... (22 more furniture blocks)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CONVERSION PROCESS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[1/4] Creating Family Documents...
  [████████████████████████] 100% (44 families)
  
[2/4] Converting Geometry...
  Doors:     [████████████████████████] 100% (12 families)
  Windows:   [████████████████████████] 100% (8 families)
  Furniture: [████████████████████████] 100% (24 families)
  
[3/4] Transferring Attributes to Parameters...
  
  Door Families:
    DOOR_NUMBER → Mark (Type)
    FIRE_RATING → Fire Rating (Type)
    MANUFACTURER → Manufacturer (Type)
    
  Window Families:
    WINDOW_TYPE → Type Comments (Type)
    GLAZING → Glazing Material (Type)
    
[4/4] Placing Instances...
  [████████████████████████] 100% (530 instances)
  
  Doors placed: 68 / 68 (100%)
  Windows placed: 142 / 142 (100%)
  Furniture placed: 95 / 95 (100%)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CONVERSION RESULTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Families Created: 44
  Doors: 12
  Windows: 8
  Furniture: 24
  
Instances Placed: 530 / 530 (100%)
  Doors: 68
  Windows: 142
  Furniture: 95
  
Parameters Created: 156
  From attributes: 156
  Auto-generated: 0
  
Accuracy:
  Geometry conversion: 98.7%
  Placement accuracy: 99.2%
  Attribute preservation: 100%
  
Time:
  Classification: 1.5 seconds
  Family creation: 12.8 seconds
  Instance placement: 3.2 seconds
  Total: 17.5 seconds

Status: ✓ Block conversion completed successfully

Family library saved: Floor_Plan_Families/
  - Doors/
  - Windows/
  - Furniture/
```

---

## 🏠 ROOM DETECTION

### **dwg-rooms-detect** - Detect Rooms from Polylines

**Syntax:**
```bash
dwg-rooms-detect file=<path> [min-area=<m2>] [max-area=<m2>] [create-rooms=true] [extract-labels=true]
```

**Description:**  
Detects room boundaries from closed polylines and creates Room elements.

**Examples:**
```bash
# Detect all rooms
dwg-rooms-detect file="Plan.dwg"

# Filter by area
dwg-rooms-detect file="Plan.dwg" min-area=5 max-area=100

# Detect without creating
dwg-rooms-detect file="Plan.dwg" create-rooms=false
```

**Output:**
```
Room Detection & Creation:

DWG File: Floor_Plan.dwg

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DETECTION PHASE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Closed Polylines Found: 52

Filtering:
  Min area: 5.0 m²
  Max area: 100.0 m²
  
  Valid rooms: 48
  Too small: 3 (< 5.0 m²)
  Too large: 1 (> 100.0 m²)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LABEL EXTRACTION (AI-Powered OCR)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Text Objects Near Room Boundaries: 850
Potential Room Labels: 52

Label Matching:
  [████████████████████████] 100% (48 rooms)
  
  Matched: 46 / 48 (96%)
  Unmatched: 2 / 48 (4%)

Sample Matches:
  Room 1: "OFFICE 201" (15.2 m²)
    Label location: (2500, 4800)
    Confidence: 99.5%
    
  Room 2: "CONFERENCE 202" (42.5 m²)
    Label location: (6500, 4800)
    Confidence: 98.8%
    
  Room 3: "CORRIDOR" (85.0 m²)
    Label location: (12500, 9000)
    Confidence: 97.2%
    
  ... (45 more rooms)

Unmatched Rooms:
  Room at (8500, 4200) - 12.5 m²
    Suggested name: "Room 47" (auto-generated)
    
  Room at (12000, 9800) - 8.5 m²
    Suggested name: "Room 48" (auto-generated)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROOM CREATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Creating Rooms:
  [████████████████████████] 100% (48 rooms)
  
  Created: 48 / 48 rooms
  
Room Parameters:
  Name: Extracted from labels
  Number: Auto-generated (201-248)
  Area: Calculated from boundaries
  Level: Ground Floor
  
Validation:
  ✓ All room boundaries closed
  ✓ No overlapping rooms
  ✓ All rooms on valid level
  
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
STATISTICS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Rooms by Type (inferred from names):
  Offices: 18 (37.5%)
  Conference Rooms: 4 (8.3%)
  Corridors: 3 (6.3%)
  Restrooms: 6 (12.5%)
  Storage: 4 (8.3%)
  Other: 13 (27.1%)

Area Distribution:
  < 10 m²: 8 rooms (16.7%)
  10-20 m²: 22 rooms (45.8%)
  20-40 m²: 14 rooms (29.2%)
  40-60 m²: 3 rooms (6.3%)
  > 60 m²: 1 room (2.1%)
  
  Total area: 1,245 m²
  Average room area: 25.9 m²
  
Time:
  Detection: 0.8 seconds
  Label extraction: 2.2 seconds
  Room creation: 1.5 seconds
  Total: 4.5 seconds

Status: ✓ Room detection completed successfully

Recommendations:
  - Review 2 rooms without labels
  - Assign room types/departments for better organization
```

---

## 📐 ANNOTATION PROCESSING

### **dwg-annotations-import** - Import Annotations

**Syntax:**
```bash
dwg-annotations-import file=<path> [text=true] [dimensions=true] [leaders=true] [preserve-formatting=true]
```

**Description:**  
Imports text, dimensions, and leaders from DWG file.

**Examples:**
```bash
# Import all annotations
dwg-annotations-import file="Plan.dwg"

# Import only dimensions
dwg-annotations-import file="Plan.dwg" text=false leaders=false

# Import with formatting
dwg-annotations-import file="Plan.dwg" preserve-formatting=true
```

**Output:**
```
Annotation Import:

DWG File: Floor_Plan.dwg

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TEXT IMPORT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Text Objects Found: 850
  MTEXT: 650
  TEXT: 200

Processing:
  [████████████████████████] 100% (850 objects)
  
  Converted to Text Notes: 842 (99.1%)
  Skipped (too small): 5 (0.6%)
  Failed: 3 (0.4%)
  
Text Formatting Preserved:
  Font families: 3 (Arial, Romans, Times)
  Text heights: 2.5mm, 3.5mm, 5mm
  Bold: 125 instances
  Italic: 48 instances
  
Sample Conversions:
  "GROUND FLOOR PLAN" → Text Note (5mm, Bold)
  "OFFICE 201" → Text Note (3.5mm, Regular)
  "SCALE 1:100" → Text Note (2.5mm, Regular)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DIMENSION IMPORT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Dimensions Found: 420
  Linear: 385
  Aligned: 25
  Angular: 10

Processing:
  [████████████████████████] 100% (420 dimensions)
  
  Successfully Converted: 415 (98.8%)
    Linear: 382 (99.2%)
    Aligned: 24 (96.0%)
    Angular: 9 (90.0%)
    
  Failed Conversions: 5 (1.2%)
    Reason: No reference elements found
    
Dimension Linking:
  Linked to walls: 285 dimensions
  Linked to doors: 68 dimensions
  Linked to windows: 42 dimensions
  Stand-alone: 20 dimensions
  
Constraints Applied:
  Locked dimensions: 185 (preserve design intent)
  Unlocked dimensions: 230 (allow flexibility)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LEADER IMPORT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Leaders Found: 125

Processing:
  [████████████████████████] 100% (125 leaders)
  
  Converted to Tags: 98 (78.4%)
    Door Tags: 45
    Window Tags: 32
    Generic Tags: 21
    
  Converted to Text Notes: 25 (20.0%)
  Failed: 2 (1.6%)
  
Tag Assignments:
  Automatically assigned tags based on leader target:
    - Leaders pointing to doors → Door Tags
    - Leaders pointing to windows → Window Tags
    - Other leaders → Generic Annotation

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
IMPORT SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Total Annotations: 1,395
Successfully Imported: 1,355 (97.1%)
Failed: 10 (0.7%)
Skipped: 30 (2.1%)

Created Elements:
  Text Notes: 867
  Dimensions: 415
  Door Tags: 45
  Window Tags: 32
  Generic Tags: 21
  
Time: 8.5 seconds
Average speed: 159 annotations/second

Status: ✓ Annotation import completed successfully

Warnings:
  - 5 dimensions had no reference elements
  - 2 leaders couldn't be converted
  - 5 text objects too small (< 1mm) were skipped
```

---

## 🤖 ADVANCED AI FEATURES

### **dwg-ai-enhance** - AI Enhancement Pass

**Syntax:**
```bash
dwg-ai-enhance [fix-overlaps=true] [detect-missing=true] [suggest-types=true] [optimize-placement=true]
```

**Description:**  
Runs AI analysis to enhance and fix imported elements.

**Examples:**
```bash
# Full AI enhancement
dwg-ai-enhance

# Fix overlaps only
dwg-ai-enhance fix-overlaps=true detect-missing=false

# Detect missing elements
dwg-ai-enhance detect-missing=true
```

**Output:**
```
AI Enhancement Analysis:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OVERLAP DETECTION & CORRECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Scanning for Overlaps:
  [████████████████████████] 100%
  
  Overlapping walls found: 12
  Overlapping elements: 3
  
Auto-Correction:
  
  Wall Overlap #1:
    Wall A (id:123456) and Wall B (id:123457)
    Overlap distance: 15mm
    Action: Trim Wall A
    Result: ✓ Corrected
    
  Wall Overlap #2:
    Wall C (id:123458) and Wall D (id:123459)
    Overlap distance: 8mm
    Action: Adjust join
    Result: ✓ Corrected
    
  ... (10 more corrections)
  
  Successfully corrected: 12 / 12 (100%)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MISSING ELEMENT DETECTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AI Analysis:
  
  Potential Missing Doors:
    Location: (5200, 3800)
    Reason: Wall opening detected, no door found
    Confidence: 92%
    Suggestion: Add door (900mm wide)
    
  Potential Missing Windows:
    Location: (8500, 6200)
    Reason: Wall segment analysis suggests window
    Confidence: 87%
    Suggestion: Add window (1200mm wide)
    
  ... (3 more suggestions)
  
  Total suggestions: 5

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TYPE SUGGESTIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AI Type Classification:
  
  Walls:
    External walls: 85 elements
      Suggested type: "Exterior - Brick on Block"
      Confidence: 94%
      
    Internal walls: 120 elements
      Suggested type: "Interior - Partition"
      Confidence: 91%
      
    Fire-rated walls: 24 elements
      Suggested type: "Interior - Fire Rated 2Hr"
      Confidence: 96%
      
  Doors:
    Standard doors: 45 elements
      Suggested type: "Single-Flush: 900x2100mm"
      
    Fire doors: 18 elements
      Suggested type: "Single-Flush Fire Rated: 900x2100mm"
      
  ... (more categories)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PLACEMENT OPTIMIZATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Analyzing Element Placement:
  
  Doors:
    Misaligned doors: 3
      Door id:234567 - 15mm off centerline
      Suggested action: Align to wall centerline
      
  Windows:
    Inconsistent sill heights: 8
      Suggested sill height: 900mm (most common)
      
  Furniture:
    Irregular spacing: 12
      Suggested action: Align to grid
      
Optimization Applied:
  ✓ 3 doors realigned
  ✓ 8 windows adjusted to uniform sill height
  ✓ 12 furniture pieces aligned to grid

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ENHANCEMENT SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Corrections Applied: 35
  Overlap fixes: 12
  Alignment corrections: 3
  Height adjustments: 8
  Grid alignments: 12
  
Suggestions Generated: 5
  Missing doors: 2
  Missing windows: 3
  
Type Assignments: 268
  Walls: 229
  Doors: 63
  Windows: 142
  
Time: 5.2 seconds

Status: ✓ AI enhancement completed successfully
```

---

## 🔄 BATCH PROCESSING

### **dwg-batch-import** - Batch Import Multiple DWG Files

**Syntax:**
```bash
dwg-batch-import folder=<path> [pattern="*.dwg"] [recursive=true] [parallel=true] [threads=<n>]
```

**Description:**  
Imports multiple DWG files in batch mode with parallel processing.

**Examples:**
```bash
# Import all DWG files in folder
dwg-batch-import folder="C:\Plans"

# Import with pattern filter
dwg-batch-import folder="C:\Plans" pattern="Floor_*.dwg"

# Recursive import
dwg-batch-import folder="C:\Project" recursive=true

# Parallel processing
dwg-batch-import folder="C:\Plans" parallel=true threads=8
```

**Output:**
```
Batch DWG Import:

Source Folder: C:\Plans
Pattern: *.dwg
Recursive: Yes
Parallel Processing: Yes (8 threads)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE DISCOVERY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Scanning folder...
  [████████████████████████] 100%
  
DWG Files Found: 24

Files by Type:
  Floor plans: 12
  Elevations: 4
  Sections: 4
  Details: 4
  
Total size: 285 MB

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BATCH IMPORT PROGRESS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Thread 1] Ground_Floor.dwg      [████████████████] 100% ✓ (12.5s)
[Thread 2] First_Floor.dwg       [████████████████] 100% ✓ (13.2s)
[Thread 3] Second_Floor.dwg      [████████████████] 100% ✓ (11.8s)
[Thread 4] Third_Floor.dwg       [████████████████] 100% ✓ (12.1s)
[Thread 5] North_Elevation.dwg   [████████████████] 100% ✓ (8.5s)
[Thread 6] South_Elevation.dwg   [████████████████] 100% ✓ (8.2s)
[Thread 7] Section_A.dwg         [████████████████] 100% ✓ (9.1s)
[Thread 8] Section_B.dwg         [████████████████] 100% ✓ (9.3s)
...

Progress: [████████████████████████] 100% (24/24 files)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BATCH IMPORT RESULTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Successfully Imported: 22 / 24 files (91.7%)
Failed: 2 files (8.3%)

Elements Created:
  Walls: 3,420
  Doors: 812
  Windows: 1,685
  Rooms: 480
  Furniture: 1,140
  Annotations: 8,450
  
  Total: 15,987 elements
  
Failed Files:
  1. Corrupt_File.dwg - File corrupted
  2. Wrong_Version.dwg - Unsupported DWG version
  
Processing Time:
  Total time: 42.5 seconds
  Average per file: 1.8 seconds
  Speedup (8 threads): 5.4x
  
  Sequential estimate: 228 seconds
  Actual time: 42.5 seconds
  Time saved: 185.5 seconds (81%)

Status: ✓ Batch import completed with 2 failures

Report saved: Batch_Import_Report_20260131.pdf
```

---

*[Document continues with sections on Quality Control, Hybrid Workflows, and Technical Reference...]*

---

## 🎯 USAGE EXAMPLES

### **Complete Workflow: Floor Plan Import**

```bash
# Step 1: Analyze DWG file
dwg-analyze file="Floor_Plan.dwg" detailed=true export-report=true

# Step 2: Create layer mapping
dwg-layers-map file="Floor_Plan.dwg" auto-detect=true save-mapping=true

# Step 3: Import DWG
dwg-import file="Floor_Plan.dwg" 
           scale=auto 
           convert-blocks=true 
           ai-enhanced=true

# Step 4: Detect and create rooms
dwg-rooms-detect file="Floor_Plan.dwg" 
                 min-area=5 
                 create-rooms=true 
                 extract-labels=true

# Step 5: Import annotations
dwg-annotations-import file="Floor_Plan.dwg" 
                       text=true 
                       dimensions=true 
                       leaders=true

# Step 6: AI enhancement
dwg-ai-enhance fix-overlaps=true 
               detect-missing=true 
               suggest-types=true

# Step 7: Quality check
dwg-quality-check detailed=true export-report=true
```

### **Batch Import Workflow**

```bash
# Import all floor plans
dwg-batch-import folder="C:\Project\Floor Plans" 
                 pattern="Floor_*.dwg"
                 parallel=true 
                 threads=8

# Import elevations
dwg-batch-import folder="C:\Project\Elevations" 
                 pattern="Elevation_*.dwg"

# Import details
dwg-batch-import folder="C:\Project\Details" 
                 pattern="Detail_*.dwg"
```

---

*StingBIM V2.0 - DWG-to-BIM AI Conversion*
*Complete Technical Guide & Command Reference*
