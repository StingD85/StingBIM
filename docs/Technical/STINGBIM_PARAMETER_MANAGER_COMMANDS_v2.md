# STINGBIM V2.0 - REVOLUTIONARY PARAMETER MANAGER
## Complete Command Reference & Usage Guide
## 200+ Commands for Ultimate Parameter Control

**Date:** January 31, 2026  
**Version:** 2.0 Parameter Manager Edition  
**Platform:** C# .NET Framework 4.8 (Revit Add-in)

---

## 📖 TABLE OF CONTENTS

1. [AI Parameter Inference](#ai-parameter-inference)
2. [Parameter Creation & Management](#parameter-creation--management)
3. [Multi-Model Synchronization](#multi-model-synchronization)
4. [Parameter Combining & Linking](#parameter-combining--linking)
5. [Parameter Genealogy & History](#parameter-genealogy--history)
6. [Batch Operations](#batch-operations)
7. [Formula Wizard](#formula-wizard)
8. [Parameter Analytics](#parameter-analytics)
9. [Excel Integration](#excel-integration)
10. [Advanced Features](#advanced-features)

---

## 🤖 AI PARAMETER INFERENCE

### **param-suggest** - AI Parameter Suggestion

**Syntax:**
```bash
param-suggest category=<category> context=<context> [topk=<n>] [confidence=<threshold>]
```

**Description:**  
Uses AI to suggest relevant parameters based on category and context description.

**Parameters:**
- `category` - Revit category (Walls, Doors, Windows, Rooms, etc.)
- `context` - Project context description
- `topk` - Number of suggestions to return (default: 10)
- `confidence` - Minimum confidence threshold (default: 0.75)

**Examples:**
```bash
# Suggest parameters for office building walls
param-suggest category=Walls context="office building, fireproof, acoustic requirements"

# Get top 5 suggestions for hospital doors
param-suggest category=Doors context="hospital, infection control, accessibility" topk=5

# High-confidence suggestions only
param-suggest category=Windows context="residential, energy efficient" confidence=0.90
```

**Output:**
```
AI Parameter Suggestions for category 'Walls':

1. Fire_Resistance_Rating [Number] (Confidence: 0.95)
   Description: Fire resistance duration in hours
   Suggested Formula: if([Wall_Type_Contains_"Fire"], 2, 1)
   
2. Acoustic_Rating_STC [Number] (Confidence: 0.92)
   Description: Sound Transmission Class rating
   Suggested Formula: [Wall_Thickness_mm] * 0.08 + 25
   
3. Office_Zone_Classification [Text] (Confidence: 0.88)
   Description: Office zoning category
   Values: "Executive", "General", "Meeting", "Support"
   
4. Fire_Protection_Type [Text] (Confidence: 0.85)
   Description: Type of fire protection system
   Values: "Passive", "Active", "Both"
   
5. Acoustic_Treatment [Text] (Confidence: 0.82)
   Description: Special acoustic treatment applied
   Values: "None", "Basic", "Enhanced", "Premium"
```

---

### **param-create-ai** - Natural Language Parameter Creation

**Syntax:**
```bash
param-create-ai prompt="<description>" [apply-to=<category>] [preview=true]
```

**Description:**  
Creates parameters from natural language descriptions using AI.

**Parameters:**
- `prompt` - Natural language description of the parameter
- `apply-to` - Category to apply parameter to (optional)
- `preview` - Show preview before creating (default: true)

**Examples:**
```bash
# Create parameter from description
param-create-ai prompt="I need a parameter that calculates the total area of windows on each wall, excluding doors, in square meters"

# Create and immediately apply
param-create-ai prompt="Create a parameter for room occupancy count based on area divided by 10" apply-to=Rooms preview=false

# Complex calculation
param-create-ai prompt="Calculate the effective R-value of a wall assembly including all layers and air films"
```

**Output:**
```
AI Parameter Creation Preview:

Generated Parameter:
  Name: Net_Glazed_Area_m2
  Type: Area
  Data Type: Area
  Category: Walls
  Instance: Yes
  Formula: ([Wall_Area_m2] - [Door_Area_m2]) × [Glazing_Percentage] / 100
  
Description:
  Calculates the net glazed (window) area on each wall by subtracting
  door areas and applying the glazing percentage.
  
Dependencies:
  - Wall_Area_m2 (must exist)
  - Door_Area_m2 (must exist)
  - Glazing_Percentage (must exist)
  
Validation:
  ✓ Formula syntax valid
  ✓ No circular dependencies
  ✓ All dependencies available
  ✓ Units compatible
  
Create this parameter? [Y/N]
```

---

### **param-infer-type** - Infer Parameter Data Type

**Syntax:**
```bash
param-infer-type name=<parameter> [values=<sample_values>]
```

**Description:**  
Uses AI to infer the most appropriate data type for a parameter.

**Examples:**
```bash
# Infer from name
param-infer-type name="Wall_Height"
# Output: Length (confidence: 0.98)

# Infer from sample values
param-infer-type name="Room_Type" values="Office,Conference,Storage,Restroom"
# Output: Text (confidence: 0.99)

# Numeric detection
param-infer-type name="Occupancy_Load" values="10,15,20,25,30"
# Output: Number (confidence: 0.95)
```

---

### **param-auto-formula** - AI Formula Generation

**Syntax:**
```bash
param-auto-formula parameter=<name> description="<what it should calculate>"
```

**Description:**  
Automatically generates formulas for parameters based on descriptions.

**Examples:**
```bash
# Generate area calculation
param-auto-formula parameter="Total_Wall_Area" description="sum of all wall segments on this level"

# Generate cost calculation
param-auto-formula parameter="Material_Cost_UGX" description="area times unit price plus 15% waste factor"

# Generate complex formula
param-auto-formula parameter="Effective_U_Value" description="thermal transmittance accounting for all layers, air films, and thermal bridges"
```

**Output:**
```
AI Formula Generation:

Parameter: Total_Wall_Area
Description: sum of all wall segments on this level

Generated Formula:
  sum([Wall_Segment_Area])
  
Alternative Formulas:
  1. [Wall_Length] × [Wall_Height] (simplified)
  2. sum([Panel_Area]) where [Level] = [Current_Level] (filtered)
  
Formula Analysis:
  Complexity: Low
  Performance: O(n) - linear
  Dependencies: 1 (Wall_Segment_Area)
  Circular Check: ✓ No circular dependencies
  
Apply formula? [Y/N]
```

---

## 📝 PARAMETER CREATION & MANAGEMENT

### **param-create** - Create Parameter

**Syntax:**
```bash
param-create name=<name> type=<type> category=<category> [instance=true] [group=<group>] [formula=<formula>] [description=<desc>]
```

**Description:**  
Creates a new shared parameter with specified properties.

**Parameters:**
- `name` - Parameter name (must be unique)
- `type` - Data type (Text, Number, Length, Area, Volume, etc.)
- `category` - Revit category to bind to
- `instance` - Instance or Type parameter (default: true)
- `group` - Parameter group (default: Identity Data)
- `formula` - Optional formula
- `description` - Parameter description

**Examples:**
```bash
# Simple text parameter
param-create name="Room_Department" type=Text category=Rooms

# Calculated area parameter
param-create name="Net_Floor_Area_m2" type=Area category=Floors formula="[Gross_Area] - [Column_Area]" instance=true

# Number parameter with description
param-create name="Occupancy_Count" type=Number category=Rooms group="Analysis" description="Maximum occupant capacity"

# Length parameter for walls
param-create name="Effective_Height_mm" type=Length category=Walls formula="[Top_Offset] - [Base_Offset]"
```

**Output:**
```
Parameter Created Successfully:

Name: Net_Floor_Area_m2
GUID: 2b3c4d5e-6f7a-8b9c-0d1e-2f3a4b5c6d7e
Type: Area
Category: Floors
Instance: Yes
Group: Dimensions
Formula: [Gross_Area] - [Column_Area]
Description: (none)

Applied to 1 category:
  ✓ Floors (142 elements)
  
Status: Ready for use
```

---

### **param-modify** - Modify Parameter Definition

**Syntax:**
```bash
param-modify parameter=<name> [new-name=<name>] [new-type=<type>] [new-formula=<formula>] [new-description=<desc>]
```

**Description:**  
Modifies an existing parameter's properties.

**Examples:**
```bash
# Rename parameter
param-modify parameter="Old_Name" new-name="New_Name"

# Update formula
param-modify parameter="Total_Cost" new-formula="[Material_Cost] + [Labor_Cost] + [Equipment_Cost]"

# Change description
param-modify parameter="Fire_Rating" new-description="Fire resistance rating in hours per IBC 2024"

# Multiple changes
param-modify parameter="Room_Area" new-name="Room_Net_Area_m2" new-formula="[Gross_Area] * 0.85" new-description="Net usable area"
```

**Output:**
```
Parameter Modified:

Original:
  Name: Old_Name
  Formula: [Value_A] + [Value_B]
  
Updated:
  Name: New_Name
  Formula: [Value_A] + [Value_B] + [Value_C]
  
Changes Applied:
  ✓ Name changed
  ✓ Formula updated
  ✓ Version incremented (v1.2 → v1.3)
  ✓ Change logged to genealogy
  
Affected Elements: 1,247
Processing time: 0.8 seconds
```

---

### **param-delete** - Delete Parameter

**Syntax:**
```bash
param-delete parameter=<name> [force=false] [backup=true]
```

**Description:**  
Deletes a parameter after checking usage and dependencies.

**Examples:**
```bash
# Safe delete with checks
param-delete parameter="Unused_Param"

# Force delete (skip warnings)
param-delete parameter="Old_Calculation" force=true

# Delete without backup
param-delete parameter="Temporary_Param" backup=false
```

**Output:**
```
Parameter Deletion Analysis:

Parameter: Unused_Param
Usage Check:
  ✓ Not used in any formulas
  ✓ Not used in any schedules
  ✓ Not used in any filters
  ✓ Not used in any tags
  × Used in 3 elements (values will be lost)
  
Impact:
  Low Risk - Parameter not critical to project
  
Backup created: Unused_Param_backup_20260131.json
  
Delete parameter? [Y/N]
```

---

## 🔄 MULTI-MODEL SYNCHRONIZATION

### **param-sync-models** - Synchronize Parameters Across Models

**Syntax:**
```bash
param-sync-models source=<model> targets=<model1,model2,...> parameters=<param1,param2,...> [mode=<bidirectional|unidirectional>] [conflict-resolution=<strategy>] [auto-commit=true]
```

**Description:**  
Synchronizes parameter values across multiple Revit models.

**Parameters:**
- `source` - Source model file path or "current"
- `targets` - Comma-separated list of target models
- `parameters` - Parameters to synchronize
- `mode` - Sync mode (default: bidirectional)
- `conflict-resolution` - Strategy: newest, oldest, manual, merge, source-wins, target-wins
- `auto-commit` - Auto-commit changes (default: true)

**Examples:**
```bash
# Sync 3 models bidirectionally
param-sync-models source="Project_A.rvt" 
                  targets="Link_Struct.rvt,Link_MEP.rvt" 
                  parameters="Level,Phase,Room_Number,Department"
                  mode=bidirectional 
                  conflict-resolution=newest

# One-way sync (source to targets)
param-sync-models source=current 
                  targets="Model_1.rvt,Model_2.rvt,Model_3.rvt"
                  parameters="Project_Name,Project_Number,Client_Name"
                  mode=unidirectional

# Manual conflict resolution
param-sync-models source=current targets="Link.rvt" parameters="all" conflict-resolution=manual
```

**Output:**
```
Multi-Model Parameter Synchronization:

Source: Project_A.rvt
Targets: 2 models
  - Link_Struct.rvt
  - Link_MEP.rvt
  
Parameters: 4
  - Level
  - Phase
  - Room_Number
  - Department
  
Analysis:
  Total elements to sync: 3,847
  
Conflict Detection:
  Conflicts found: 23
  
  Conflict #1:
    Element: Wall id:1234567
    Parameter: Room_Number
    Source value: "205" (2026-01-31 10:15:23)
    Target value: "204" (2026-01-30 14:22:10)
    Resolution: Use source (newer)
    
  ... (22 more conflicts)
  
Resolution Summary:
  - Auto-resolved (newest): 23
  - Manual review required: 0
  
Sync Progress:
  [████████████████████████████████] 100%
  Processed: 3,847 elements
  Updated: 3,824 elements
  Skipped: 23 elements (no changes)
  
Sync Time: 2.3 seconds
Speed: 1,673 elements/second

Status: ✓ Sync completed successfully
```

---

### **param-sync-status** - Check Synchronization Status

**Syntax:**
```bash
param-sync-status [models=<model1,model2,...>] [parameters=<param1,param2,...>]
```

**Description:**  
Shows synchronization status across models.

**Examples:**
```bash
# Check all linked models
param-sync-status

# Check specific models
param-sync-status models="Link_1.rvt,Link_2.rvt"

# Check specific parameters
param-sync-status parameters="Level,Phase,Department"
```

**Output:**
```
Parameter Synchronization Status:

Models: 3
  ✓ Project_A.rvt (source)
  ✓ Link_Struct.rvt (in sync)
  ⚠ Link_MEP.rvt (12 parameters out of sync)
  
Out of Sync Parameters:
  
  Room_Number:
    Project_A: 1,247 elements
    Link_MEP: 1,235 elements (12 missing)
    Last sync: 2026-01-30 15:30:00
    
  Department:
    Project_A: 850 elements
    Link_MEP: 850 elements (3 value mismatches)
    Last sync: 2026-01-30 15:30:00
    
Recommendation: Run param-sync-models to resolve discrepancies
```

---

### **param-link-mapping** - Map Parameters Between Models

**Syntax:**
```bash
param-link-mapping source-model=<model> target-model=<model> mapping=<source_param:target_param,...> [bidirectional=true]
```

**Description:**  
Creates parameter mappings between models with different parameter names.

**Examples:**
```bash
# Map architectural to MEP parameters
param-link-mapping source-model="Arch.rvt" 
                    target-model="MEP.rvt"
                    mapping="Room_Number:Space_Number,Room_Name:Space_Name,Room_Area:Space_Area"
                    bidirectional=true

# One-way mapping
param-link-mapping source-model=current 
                    target-model="Link.rvt"
                    mapping="Level:Story,Phase:Construction_Phase"
                    bidirectional=false
```

**Output:**
```
Parameter Link Mapping Created:

Source Model: Arch.rvt
Target Model: MEP.rvt
Mode: Bidirectional

Mappings:
  1. Room_Number ↔ Space_Number
     Elements: 480 rooms/spaces
     Status: ✓ Active
     
  2. Room_Name ↔ Space_Name
     Elements: 480 rooms/spaces
     Status: ✓ Active
     
  3. Room_Area ↔ Space_Area
     Elements: 480 rooms/spaces
     Status: ✓ Active
     
Auto-Sync: Enabled
Sync Frequency: Real-time

Status: Mapping active, changes will synchronize automatically
```

---

## 🔗 PARAMETER COMBINING & LINKING

### **param-combine** - Combine Multiple Parameters

**Syntax:**
```bash
param-combine output=<name> inputs=<param1,param2,...> template="<template>" [apply-to=<category>] [update-mode=<live|manual>] [separator="<sep>"]
```

**Description:**  
Creates a combined parameter from multiple source parameters using a template.

**Parameters:**
- `output` - Name of combined parameter to create
- `inputs` - Source parameters (comma-separated)
- `template` - Template string with placeholders {param_name}
- `apply-to` - Category to apply to
- `update-mode` - live (auto-update) or manual (default: live)
- `separator` - Default separator for list combines (default: " ")

**Examples:**
```bash
# Combine room information
param-combine output="Full_Room_Name" 
              inputs="Level,Department,Room_Number,Room_Name"
              template="{Level}-{Department}{Room_Number}: {Room_Name}"
              apply-to=Rooms 
              update-mode=live

# Combine address parts
param-combine output="Full_Address"
              inputs="Street,City,State,ZIP"
              template="{Street}, {City}, {State} {ZIP}"
              apply-to=Project_Information

# Concatenate with custom separator
param-combine output="Material_List"
              inputs="Layer_1,Layer_2,Layer_3"
              template="{Layer_1} | {Layer_2} | {Layer_3}"
              separator=" | "
```

**Output:**
```
Parameter Combination Created:

Output Parameter: Full_Room_Name
Source Parameters: 4
  - Level
  - Department
  - Room_Number
  - Room_Name
  
Template: "{Level}-{Department}{Room_Number}: {Room_Name}"

Sample Results:
  "02-ADMIN205: Conference Room"
  "02-ADMIN206: Office"
  "03-ENG301: Design Studio"
  
Applied to: Rooms (480 elements)
Update Mode: Live (auto-updates on source changes)

Processing:
  [████████████████████████████████] 100%
  Updated: 480 rooms
  Time: 0.4 seconds
  
Status: ✓ Combination active and updating
```

---

### **param-link** - Link Parameters Across Categories

**Syntax:**
```bash
param-link source-category=<category> source-param=<param> target-category=<category> target-param=<param> [link-type=<copy|reference|calculate>] [update-trigger=<onchange|manual>]
```

**Description:**  
Creates intelligent links between parameters across different categories.

**Examples:**
```bash
# Link room names to space names
param-link source-category=Rooms source-param="Room_Name"
           target-category=Spaces target-param="Space_Name"
           link-type=copy update-trigger=onchange

# Reference wall fire rating in doors
param-link source-category=Walls source-param="Fire_Rating"
           target-category=Doors target-param="Host_Wall_Fire_Rating"
           link-type=reference

# Calculate door count per room
param-link source-category=Doors source-param="Room"
           target-category=Rooms target-param="Door_Count"
           link-type=calculate update-trigger=onchange
```

---

### **param-propagate** - Propagate Parameter Values

**Syntax:**
```bash
param-propagate source=<param> target=<param> [filter=<condition>] [mode=<overwrite|fill-empty>] [preview=true]
```

**Description:**  
Propagates parameter values based on conditions.

**Examples:**
```bash
# Copy fire ratings
param-propagate source="Wall_Type_Fire_Rating" target="Fire_Rating" mode=fill-empty

# Conditional propagation
param-propagate source="Design_Occupancy" target="Actual_Occupancy" 
                filter="[Actual_Occupancy] = 0" mode=overwrite preview=true

# Fill empty department values
param-propagate source="Level_Default_Department" target="Room_Department"
                filter="[Room_Department] = ''" mode=fill-empty
```

**Output:**
```
Parameter Propagation Preview:

Source: Wall_Type_Fire_Rating
Target: Fire_Rating
Mode: Fill Empty (only update blank values)

Elements to Update: 1,247 walls

Sample Changes:
  Wall id:123456
    Source: "2 Hour"
    Target: "" → "2 Hour" ✓
    
  Wall id:123457
    Source: "1 Hour"
    Target: "2 Hour" → (no change - not empty)
    
  Wall id:123458
    Source: "2 Hour"
    Target: "" → "2 Hour" ✓
    
Summary:
  Will update: 842 elements
  Will skip: 405 elements (already have values)
  
Apply propagation? [Y/N]
```

---

## 📚 PARAMETER GENEALOGY & HISTORY

### **param-history** - View Parameter History

**Syntax:**
```bash
param-history parameter=<name> [show-versions=true] [show-changes=true] [limit=<n>]
```

**Description:**  
Shows complete history of parameter versions and changes.

**Examples:**
```bash
# View all versions
param-history parameter="Room_Area_m2" show-versions=true

# View recent changes
param-history parameter="Fire_Rating" show-changes=true limit=10

# Complete history
param-history parameter="Cost_Estimate_UGX" show-versions=true show-changes=true
```

**Output:**
```
Parameter History: Room_Area_m2

Versions:
  v3.0 (Current) - 2026-01-31 10:45:00 by John Doe
    Formula: [Gross_Area] * 0.92
    Comment: "Updated to account for wall thickness"
    
  v2.1 - 2026-01-15 14:30:00 by Jane Smith
    Formula: [Gross_Area] * 0.90
    Comment: "Increased efficiency factor"
    
  v2.0 - 2025-12-20 09:15:00 by John Doe
    Formula: [Gross_Area] - [Column_Area]
    Comment: "Changed calculation method"
    
  v1.0 - 2025-12-01 11:00:00 by System
    Formula: [Gross_Area]
    Comment: "Initial creation"

Recent Changes:
  2026-01-31 10:45:23 | Modified | John Doe
    Changed formula from "[Gross_Area] * 0.90" to "[Gross_Area] * 0.92"
    Reason: "Better reflects actual usable area"
    
  2026-01-15 14:32:10 | Modified | Jane Smith
    Changed formula from "[Gross_Area] - [Column_Area]" to "[Gross_Area] * 0.90"
    Reason: "Simplified calculation"
    
  2025-12-20 09:17:45 | Modified | John Doe
    Changed formula from "[Gross_Area]" to "[Gross_Area] - [Column_Area]"
    Reason: "Added column area deduction"
    
  2025-12-01 11:02:30 | Created | System
    Initial parameter creation
    
Statistics:
  Total versions: 4
  Total changes: 8
  Contributors: 2 users
  Age: 61 days
```

---

### **param-rollback** - Rollback to Previous Version

**Syntax:**
```bash
param-rollback parameter=<name> to-version=<version> [reason="<reason>"] [affected-elements=<preview|all>] [create-backup=true]
```

**Description:**  
Rolls back a parameter to a previous version.

**Examples:**
```bash
# Rollback with preview
param-rollback parameter="Wall_Cost_UGX" to-version="v1.2" affected-elements=preview

# Rollback with reason
param-rollback parameter="Fire_Rating" to-version="v2.0" reason="v3.0 formula producing incorrect values"

# Rollback without backup
param-rollback parameter="Temp_Calculation" to-version="v1.0" create-backup=false
```

**Output:**
```
Parameter Rollback Preview:

Parameter: Wall_Cost_UGX
Current Version: v2.0
Target Version: v1.2

Changes:
  Formula:
    v2.0: [Area] × [Unit_Rate] × (1 + [Labor_Factor] × [Complexity])
    v1.2: [Area] × [Unit_Rate]
    
  Description:
    v2.0: "Total wall cost including labor complexity"
    v1.2: "Basic wall material cost"
    
Affected Elements: 12,450 walls

Sample Impact:
  Wall id:123456 (200mm Brick Wall)
    Current Cost: 1,250,000 UGX
    After Rollback: 950,000 UGX
    Change: -300,000 UGX (-24%)
    
  Wall id:123457 (Concrete Block Wall)
    Current Cost: 2,100,000 UGX
    After Rollback: 1,800,000 UGX
    Change: -300,000 UGX (-14%)
    
Rollback Summary:
  Elements affected: 12,450
  Average cost change: -22%
  Backup will be created: Yes
  Backup location: Wall_Cost_UGX_v2.0_backup_20260131.json
  
Confirm rollback? [Y/N]
```

---

### **param-compare-versions** - Compare Parameter Versions

**Syntax:**
```bash
param-compare-versions parameter=<name> version1=<v1> version2=<v2> [show-differences=true]
```

**Description:**  
Compares two versions of a parameter side-by-side.

**Examples:**
```bash
# Compare current with previous
param-compare-versions parameter="Room_Area" version1="current" version2="v1.0"

# Compare specific versions
param-compare-versions parameter="Cost_Formula" version1="v2.1" version2="v1.5" show-differences=true
```

**Output:**
```
Parameter Version Comparison:

Parameter: Room_Area
Version 1: v2.0 (2026-01-15)
Version 2: v1.0 (2025-12-01)

┌─────────────────┬───────────────────────────────┬───────────────────────┐
│ Property        │ v2.0                          │ v1.0                  │
├─────────────────┼───────────────────────────────┼───────────────────────┤
│ Formula         │ [Gross_Area] * 0.90           │ [Gross_Area]          │
│                 │ (Modified)                    │                       │
├─────────────────┼───────────────────────────────┼───────────────────────┤
│ Data Type       │ Area                          │ Area                  │
│                 │ (Same)                        │                       │
├─────────────────┼───────────────────────────────┼───────────────────────┤
│ Instance        │ Yes                           │ Yes                   │
│                 │ (Same)                        │                       │
├─────────────────┼───────────────────────────────┼───────────────────────┤
│ Description     │ "Net usable room area"        │ ""                    │
│                 │ (Added)                       │                       │
└─────────────────┴───────────────────────────────┴───────────────────────┘

Differences: 2
  1. Formula changed
  2. Description added
  
Performance Comparison:
  v2.0 calculation time: 0.12ms average
  v1.0 calculation time: 0.08ms average
  Change: +50% slower (additional multiplication)
  
Recommendation: v2.0 provides more accurate results but with slight performance penalty
```

---

## ⚡ BATCH OPERATIONS

### **param-batch-update** - Batch Update Parameters

**Syntax:**
```bash
param-batch-update category=<category> parameter=<name> value=<value> [condition=<filter>] [threads=<n>] [gpu=<true|false>] [progress=true]
```

**Description:**  
Updates parameter values for multiple elements with optional GPU acceleration.

**Parameters:**
- `category` - Element category
- `parameter` - Parameter to update
- `value` - New value (can be formula or literal)
- `condition` - Filter condition (optional)
- `threads` - Number of CPU threads (default: 16)
- `gpu` - Use GPU acceleration (default: auto-detect)
- `progress` - Show progress bar (default: true)

**Examples:**
```bash
# Simple batch update
param-batch-update category=Walls parameter="Fire_Rating" value="2 Hour"

# Conditional update
param-batch-update category=Walls parameter="Fire_Rating" value="2 Hour" 
                   condition="[Wall_Type] contains 'Fire'"

# GPU-accelerated update (100,000+ elements)
param-batch-update category=Rooms parameter="Department" value="ADMIN" 
                   condition="[Level] = '02'"
                   gpu=true threads=32

# Formula-based update
param-batch-update category=Doors parameter="Door_Width_mm" 
                   value="[Opening_Width] - 50"
                   threads=16
```

**Output:**
```
Batch Parameter Update:

Category: Walls
Parameter: Fire_Rating
New Value: "2 Hour"
Condition: [Wall_Type] contains "Fire"
Mode: GPU-Accelerated

Elements Found: 127,450 walls
Elements Matching Condition: 8,245 walls

GPU Configuration:
  Device: NVIDIA RTX 4090
  VRAM: 24GB
  Compute Capability: 8.9
  Threads per Block: 256
  Grid Size: 33 blocks

Progress:
  [████████████████████████████████] 100%
  
  Processing: 8,245 / 8,245 elements
  Speed: 30,345 elements/second
  Time Elapsed: 0.27 seconds
  Time Remaining: 0.00 seconds
  
Results:
  Updated: 8,245 elements
  Skipped: 0 elements
  Errors: 0 elements
  
Total Time: 4.2 seconds (includes GPU transfer)
Average Speed: 1,963 elements/second (overall)

Status: ✓ Batch update completed successfully
```

---

### **param-batch-create** - Batch Create Parameters

**Syntax:**
```bash
param-batch-create definitions-file=<path> [validate=true] [apply-immediately=true]
```

**Description:**  
Creates multiple parameters from a definitions file (CSV, JSON, or Excel).

**File Format (CSV):**
```csv
Name,Type,Category,Instance,Group,Formula,Description
Room_Department,Text,Rooms,Yes,Identity Data,,"Department assignment"
Room_Net_Area_m2,Area,Rooms,Yes,Dimensions,"[Gross_Area] * 0.85","Net usable area"
Fire_Rating_Hours,Number,Walls,No,Fire Protection,,"Fire resistance in hours"
```

**Examples:**
```bash
# Create from CSV
param-batch-create definitions-file="parameters.csv"

# Create from JSON
param-batch-create definitions-file="params.json" validate=true

# Create without immediate application
param-batch-create definitions-file="params.xlsx" apply-immediately=false
```

**Output:**
```
Batch Parameter Creation:

Source File: parameters.csv
Format: CSV
Parameters Found: 125

Validation:
  ✓ All names unique
  ✓ All data types valid
  ✓ All categories exist
  ✓ All formulas valid
  ✗ Warning: 3 parameters reference non-existent parameters
  
Warning Details:
  Parameter "Calculated_Cost" references "Unit_Price" (not found)
  Parameter "Total_Area" references "Panel_Count" (not found)
  Parameter "Efficiency" references "Design_Target" (not found)
  
Continue anyway? [Y/N]: Y

Creating Parameters:
  [████████████████████████████████] 100%
  
  Created: 125 / 125 parameters
  Time: 8.5 seconds
  
Application:
  Applying to categories...
  [████████████████████████████████] 100%
  
  Applied to 12 categories
  Total elements affected: 15,847
  
Status: ✓ Batch creation completed successfully
Warnings: 3 (see above)
```

---

### **param-batch-delete** - Batch Delete Parameters

**Syntax:**
```bash
param-batch-delete filter=<condition> [dry-run=true] [backup=true] [force=false]
```

**Description:**  
Deletes multiple parameters based on filter criteria.

**Filter Conditions:**
- `unused` - Parameters not used anywhere
- `empty` - Parameters with no values
- `orphaned` - Shared parameters not in any families
- `pattern:<regex>` - Parameters matching regex pattern
- `category:<cat>` - Parameters in specific category

**Examples:**
```bash
# Delete all unused parameters (dry run)
param-batch-delete filter=unused dry-run=true

# Delete parameters with specific pattern
param-batch-delete filter="pattern:^TEMP_.*" backup=true

# Delete empty parameters
param-batch-delete filter=empty force=true
```

**Output:**
```
Batch Parameter Deletion (DRY RUN):

Filter: unused
Backup: Enabled

Parameters Found: 345 unused parameters

Usage Analysis:
  Not in formulas: 345
  Not in schedules: 342
  Not in filters: 345
  Not in tags: 345
  Has values: 87
  
Risk Assessment:
  Low Risk: 258 parameters (no values, no dependencies)
  Medium Risk: 87 parameters (has values, but unused)
  High Risk: 0 parameters (has dependencies)
  
Sample Parameters to Delete:
  1. OLD_TEMP_CALC (Number) - Last used: Never
  2. LEGACY_PARAM (Text) - Last used: Never
  3. TEST_FIELD (Length) - Last used: Never
  ... (342 more)
  
Backup Plan:
  Backup file: unused_params_backup_20260131.json
  Recovery command: param-batch-restore backup=unused_params_backup_20260131.json
  
DRY RUN - No changes made.
Run with dry-run=false to execute deletion.
```

---

## 🧙 FORMULA WIZARD

### **formula-generate** - Generate Formula from Description

**Syntax:**
```bash
formula-generate description="<natural language>" [parameter=<name>] [optimize=true] [validate=true]
```

**Description:**  
Uses AI to generate Revit formulas from natural language descriptions.

**Examples:**
```bash
# Generate area calculation
formula-generate description="Calculate total wall area excluding openings"

# Generate cost formula
formula-generate description="Material cost is area times unit price plus 15% waste factor"

# Generate complex thermal formula
formula-generate description="Calculate effective R-value including all layers and air films with thermal bridging correction"
```

**Output:**
```
Formula Generation:

Description: "Calculate total wall area excluding openings"

Generated Formulas (3 options):

Option 1 (Recommended):
  Formula: [Wall_Gross_Area] - sum([Door_Area]) - sum([Window_Area])
  Complexity: Medium
  Performance: O(n) where n = number of openings
  Dependencies:
    - Wall_Gross_Area (Required)
    - Door_Area (Required, multiple)
    - Window_Area (Required, multiple)
  Validation: ✓ Valid syntax
  
Option 2 (Simplified):
  Formula: [Wall_Gross_Area] * (1 - [Opening_Percentage])
  Complexity: Low
  Performance: O(1) constant time
  Dependencies:
    - Wall_Gross_Area (Required)
    - Opening_Percentage (Required)
  Validation: ✓ Valid syntax
  
Option 3 (Detailed):
  Formula: [Wall_Length] × [Wall_Height] - sum(if([Opening_Type] = "Door", [Opening_Area], 0)) - sum(if([Opening_Type] = "Window", [Opening_Area], 0))
  Complexity: High
  Performance: O(n) with conditional logic
  Dependencies:
    - Wall_Length (Required)
    - Wall_Height (Required)
    - Opening_Type (Required, multiple)
    - Opening_Area (Required, multiple)
  Validation: ✓ Valid syntax
  
Recommendation:
  Use Option 1 for best balance of accuracy and performance.
  
Apply formula to parameter? [Y/N]
```

---

### **formula-optimize** - Optimize Formula

**Syntax:**
```bash
formula-optimize parameter=<name> [benchmark=true] [show-alternatives=true]
```

**Description:**  
Analyzes and optimizes parameter formulas for better performance.

**Examples:**
```bash
# Optimize single parameter
formula-optimize parameter="Complex_Calculation"

# Benchmark before/after
formula-optimize parameter="Total_Cost_UGX" benchmark=true

# Show alternative formulas
formula-optimize parameter="Thermal_Resistance" show-alternatives=true
```

**Output:**
```
Formula Optimization:

Parameter: Complex_Calculation
Current Formula: if([Type] = "A", [Value_1] + [Value_2], if([Type] = "B", [Value_3] + [Value_4], [Value_5]))

Performance Analysis:
  Complexity: O(1) - constant time
  Execution time: 0.45ms (average)
  Memory usage: 128 bytes
  Redundancies found: 2
  
Optimization Opportunities:
  1. Nested if statements → lookup table
  2. Repeated evaluations → cache intermediate results
  
Optimized Formula: lookup([Type], "A", [Value_1] + [Value_2], "B", [Value_3] + [Value_4], [Value_5])

Benchmark Results:
  Original formula:
    Avg: 0.45ms
    Min: 0.38ms
    Max: 0.62ms
    
  Optimized formula:
    Avg: 0.18ms (-60%)
    Min: 0.15ms (-61%)
    Max: 0.24ms (-61%)
    
  Speedup: 2.5x faster
  
Alternative Formulas:
  
  Alt 1 (Fastest):
    Formula: [Type_Lookup_Value]
    Speed: 0.08ms (5.6x faster)
    Note: Requires pre-calculated lookup parameter
    
  Alt 2 (Most Readable):
    Formula: 
      if([Type] = "A",
        [Value_1] + [Value_2],
      if([Type] = "B",
        [Value_3] + [Value_4],
        [Value_5]))
    Speed: 0.45ms (same as current)
    Note: Better formatted for maintenance
    
Apply optimized formula? [Y/N]
```

---

### **formula-validate** - Validate Formula

**Syntax:**
```bash
formula-validate formula="<formula>" [parameter=<name>] [check-circular=true] [check-performance=true]
```

**Description:**  
Validates formula syntax and checks for issues.

**Examples:**
```bash
# Validate new formula
formula-validate formula="[Area] * [Unit_Price] * 1.15"

# Check existing parameter
formula-validate parameter="Cost_Estimate"

# Full validation
formula-validate formula="[A] + [B] / ([C] - [D])" check-circular=true check-performance=true
```

**Output:**
```
Formula Validation:

Formula: [Area] * [Unit_Price] * 1.15

Syntax Check:
  ✓ Valid Revit formula syntax
  ✓ All operators valid
  ✓ Parentheses balanced
  ✓ No syntax errors
  
Parameter Check:
  ✓ Area - exists, type: Area
  ✓ Unit_Price - exists, type: Currency
  
Type Compatibility:
  ✓ Area (Area) × Unit_Price (Currency) = Currency ✓
  ✓ Result × 1.15 (Number) = Currency ✓
  
Circular Dependency Check:
  ✓ No circular dependencies detected
  
  Dependency Graph:
    [Cost_Estimate]
      ↳ [Area]
      ↳ [Unit_Price]
      
Performance Analysis:
  Complexity: O(1) - constant time
  Operations: 2 (multiply, multiply)
  Expected execution: <0.1ms
  Rating: Excellent
  
Warnings: None
Errors: None

Status: ✓ Formula is valid and ready to use
```

---

### **formula-dependencies** - Show Formula Dependencies

**Syntax:**
```bash
formula-dependencies parameter=<name> [depth=<n>] [visualize=true]
```

**Description:**  
Shows all dependencies for a parameter's formula.

**Examples:**
```bash
# Show direct dependencies
formula-dependencies parameter="Total_Cost"

# Show nested dependencies
formula-dependencies parameter="Complex_Calc" depth=5

# Visualize dependency graph
formula-dependencies parameter="Final_Result" visualize=true
```

**Output:**
```
Formula Dependencies: Total_Cost

Direct Dependencies (3):
  - Material_Cost (Currency)
  - Labor_Cost (Currency)
  - Equipment_Cost (Currency)
  
Nested Dependencies:
  Material_Cost depends on:
    - Material_Quantity (Number)
    - Material_Unit_Price (Currency)
    
  Labor_Cost depends on:
    - Labor_Hours (Number)
    - Labor_Rate (Currency)
    
  Equipment_Cost depends on:
    - Equipment_Hours (Number)
    - Equipment_Rate (Currency)
    
Total Dependencies: 9 parameters
Maximum Depth: 2 levels

Dependency Graph:
```
[Total_Cost]
  ├─ [Material_Cost]
  │  ├─ [Material_Quantity]
  │  └─ [Material_Unit_Price]
  ├─ [Labor_Cost]
  │  ├─ [Labor_Hours]
  │  └─ [Labor_Rate]
  └─ [Equipment_Cost]
     ├─ [Equipment_Hours]
     └─ [Equipment_Rate]
```

Calculation Order:
  1. Material_Quantity, Material_Unit_Price, Labor_Hours, Labor_Rate, Equipment_Hours, Equipment_Rate
  2. Material_Cost, Labor_Cost, Equipment_Cost
  3. Total_Cost
  
Status: ✓ All dependencies resolved, no circular references
```

---

## 📊 PARAMETER ANALYTICS

### **param-health** - Parameter Health Dashboard

**Syntax:**
```bash
param-health [analyze=true] [generate-report=true] [export=<format>]
```

**Description:**  
Generates comprehensive health analysis of all parameters.

**Examples:**
```bash
# Quick health check
param-health

# Full analysis with report
param-health analyze=true generate-report=true

# Export to Excel
param-health analyze=true export=xlsx
```

**Output:**
```
Parameter Health Dashboard:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OVERVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total Parameters: 1,548
Used Parameters: 1,203 (77.7%) ✓
Unused Parameters: 345 (22.3%) ⚠
Orphaned Shared Parameters: 12 (0.8%) ✗
Empty Value Instances: 2,840 ⚠
Formula Errors: 3 ✗
Performance Issues: 8 slow formulas ⚠

Health Score: 82/100 (Good) ✓

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
USAGE BREAKDOWN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Used in Formulas: 456 parameters
Used in Schedules: 892 parameters
Used in Filters: 234 parameters
Used in Tags: 167 parameters
Has Values: 1,203 parameters

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CRITICAL ISSUES (3)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Formula Error - "Total_Area_Calc"
   Error: Circular dependency detected
   Impact: 1,247 elements affected
   Recommendation: Review formula dependencies
   
2. Formula Error - "Cost_Factor"
   Error: Division by zero in 12 instances
   Impact: 12 elements affected
   Recommendation: Add if condition to check denominator
   
3. Formula Error - "Complex_Ratio"
   Error: Invalid parameter reference "[Non_Existent_Param]"
   Impact: 850 elements affected
   Recommendation: Update formula or create missing parameter

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PERFORMANCE ISSUES (8)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Slow Formulas (>1ms average):

1. "Nested_Calculation" - 12.5ms avg
   Formula: if(if([A] > [B], [C] + [D], [E] - [F]) > 100, [G] * 2, [H] / 3)
   Recommendation: Simplify nested if statements
   Potential speedup: 8x
   
2. "Sum_All_Areas" - 8.2ms avg
   Formula: sum([Panel_Area_1]) + sum([Panel_Area_2]) + sum([Panel_Area_3]) + ...
   Recommendation: Use single sum function with filter
   Potential speedup: 5x
   
... (6 more)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CLEANUP OPPORTUNITIES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Unused Parameters (345):
  Could save: ~2.1MB in file size
  Recommendation: Run param-batch-delete filter=unused
  
Orphaned Shared Parameters (12):
  Risk: High (not in any families)
  Recommendation: Remove from shared parameter file
  
Empty Parameters (258):
  Parameters with no values in any instances
  Recommendation: Review necessity, delete if unused
  
Duplicate Parameters (4 groups):
  "Room_Area" and "Room_Area_m2" - likely duplicates
  "Fire_Rating" and "Fire_Resistance" - possibly redundant
  ... (2 more groups)
  Recommendation: Consolidate duplicate parameters

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECOMMENDATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Priority Actions:

1. HIGH: Fix 3 formula errors
   Command: formula-fix --auto
   
2. MEDIUM: Delete 345 unused parameters
   Command: param-batch-delete filter=unused
   
3. MEDIUM: Optimize 8 slow formulas
   Command: formula-optimize --batch
   
4. LOW: Remove 12 orphaned shared parameters
   Command: param-cleanup-orphaned
   
5. LOW: Consolidate 4 duplicate parameter groups
   Command: param-merge-duplicates

Estimated Improvement:
  Health Score: 82 → 95 (+13 points)
  File Size: -2.1MB
  Performance: +40% faster calculations

Report saved to: Parameter_Health_Report_20260131.pdf
```

---

### **param-usage** - Show Parameter Usage

**Syntax:**
```bash
param-usage parameter=<name> [detailed=true]
```

**Description:**  
Shows where and how a parameter is used throughout the project.

**Examples:**
```bash
# Basic usage
param-usage parameter="Fire_Rating"

# Detailed usage report
param-usage parameter="Room_Department" detailed=true
```

**Output:**
```
Parameter Usage Report: Fire_Rating

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Type: Number
Category: Walls
Instance: No (Type parameter)
Total Elements: 8,245 walls

Value Distribution:
  "1 Hour": 3,450 walls (41.9%)
  "2 Hour": 4,250 walls (51.6%)
  "0.5 Hour": 420 walls (5.1%)
  (empty): 125 walls (1.5%)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
USAGE DETAILS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Used in Formulas (3):
  1. Parameter: "Door_Fire_Rating"
     Formula: [Host_Wall_Fire_Rating]
     Elements: 680 doors
     
  2. Parameter: "Assembly_Fire_Rating"
     Formula: max([Wall_Fire_Rating], [Door_Fire_Rating])
     Elements: 1,450 assemblies
     
  3. Parameter: "Compliance_Check"
     Formula: if([Fire_Rating] >= 1, "✓", "✗")
     Elements: 8,245 walls

Used in Schedules (5):
  1. "Wall Schedule - Fire Rated"
     Filter: Fire_Rating > 0
     Sorting: Fire_Rating (descending)
     
  2. "Fire Protection Summary"
     Grouping: Fire_Rating
     Totals: Count
     
  3. "Code Compliance Report"
     Field: Fire_Rating
     Conditional formatting: Red if < 1 hour
     
  ... (2 more schedules)

Used in Filters (2):
  1. "Fire-Rated Walls"
     Rule: Fire_Rating ≥ 1
     Applied to: 3 views
     
  2. "2-Hour Rated Elements"
     Rule: Fire_Rating = 2
     Applied to: 2 views

Used in Tags (1):
  1. "Wall Fire Rating Tag"
     Field: Fire_Rating
     Format: "{value} Hour Fire Rating"
     Instances: 247 tags

Referenced By (12 parameters):
  - Door_Fire_Rating (reference)
  - Assembly_Fire_Rating (calculation)
  - Code_Compliance_Status (conditional)
  ... (9 more)

Impact Assessment:
  Criticality: HIGH
  Deletion risk: SEVERE
  Modification impact: Would affect 12 dependent parameters, 5 schedules, 2 filters, 1 tag

Status: ✓ Actively used, critical to project
```

---

### **param-find** - Find Parameters

**Syntax:**
```bash
param-find [name="<pattern>"] [type=<type>] [category=<category>] [has-formula=<true|false>] [has-value=<true|false>] [used-in=<schedules|formulas|filters|tags>]
```

**Description:**  
Searches for parameters matching specified criteria.

**Examples:**
```bash
# Find by name pattern
param-find name="*Fire*"

# Find unused parameters
param-find has-value=false used-in=none

# Find all Area parameters
param-find type=Area

# Find parameters with formulas
param-find has-formula=true

# Complex search
param-find name="Room_*" category=Rooms has-value=true
```

**Output:**
```
Parameter Search Results:

Query: name="*Fire*"
Found: 18 parameters

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RESULTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Fire_Rating
   Type: Number
   Category: Walls
   Instance: No
   Has Formula: No
   Has Values: 8,120 / 8,245 elements (98.5%)
   Used In: Formulas (3), Schedules (5), Filters (2), Tags (1)
   
2. Fire_Resistance_Hours
   Type: Number
   Category: Walls
   Instance: No
   Has Formula: Yes
   Formula: if([Fire_Rating] > 0, [Fire_Rating], 0)
   Has Values: 8,245 / 8,245 elements (100%)
   Used In: Schedules (2)
   
3. Fire_Protection_Type
   Type: Text
   Category: Walls
   Instance: Yes
   Has Formula: No
   Has Values: 6,450 / 8,245 elements (78.2%)
   Used In: Schedules (3), Filters (1)
   
4. Firewall_Classification
   Type: Text
   Category: Walls
   Instance: No
   Has Formula: Yes
   Formula: if([Fire_Rating] >= 2, "Firewall", "Fire Barrier")
   Has Values: 8,245 / 8,245 elements (100%)
   Used In: Formulas (1), Schedules (4)
   
... (14 more parameters)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total Found: 18 parameters
With Formulas: 8 (44%)
With Values: 16 (89%)
Used in Schedules: 14 (78%)
Used in Formulas: 6 (33%)
Used in Filters: 4 (22%)
Used in Tags: 2 (11%)
```

---

## 📈 EXCEL INTEGRATION

### **param-export-excel** - Export to Excel

**Syntax:**
```bash
param-export-excel file=<path> [category=<category>] [parameters=<param1,param2,...>] [include-formulas=true] [include-metadata=true]
```

**Description:**  
Exports parameter values to Excel for editing.

**Examples:**
```bash
# Export all room parameters
param-export-excel file="Rooms.xlsx" category=Rooms

# Export specific parameters
param-export-excel file="Walls.xlsx" category=Walls parameters="Fire_Rating,Wall_Type,Cost"

# Export without formulas
param-export-excel file="Simple_Export.xlsx" category=Doors include-formulas=false
```

**Output:**
```
Excel Export:

Source Category: Rooms
Target File: Rooms.xlsx
Parameters: ALL (85 parameters)

Export Configuration:
  Include formulas: Yes
  Include metadata: Yes
  Include formatting: Yes
  
Elements to Export: 480 rooms

Creating Excel File:
  [████████████████████████████████] 100%
  
  Sheet 1: Room Data
    Rows: 481 (1 header + 480 data)
    Columns: 88 (ID, Mark, Name + 85 parameters)
    
  Sheet 2: Formulas
    Formula definitions: 23
    Dependencies: Listed
    
  Sheet 3: Metadata
    Parameter GUIDs: Listed
    Data types: Listed
    Last modified: Listed
    
  Sheet 4: Instructions
    How to edit
    How to import back
    
File Size: 1.2MB
Export Time: 3.5 seconds

Status: ✓ Export completed successfully
File saved: C:\Projects\Rooms.xlsx

Next Steps:
  1. Open Rooms.xlsx in Excel
  2. Edit parameter values
  3. Import back with: param-import-excel file="Rooms.xlsx"
```

---

### **param-import-excel** - Import from Excel

**Syntax:**
```bash
param-import-excel file=<path> [conflict-resolution=<strategy>] [validate=true] [preview=true]
```

**Description:**  
Imports parameter values from Excel file.

**Examples:**
```bash
# Import with preview
param-import-excel file="Rooms.xlsx" preview=true

# Import with conflict resolution
param-import-excel file="Walls.xlsx" conflict-resolution=newest

# Import without validation (faster)
param-import-excel file="Simple_Data.xlsx" validate=false preview=false
```

**Output:**
```
Excel Import:

Source File: Rooms.xlsx
Last Modified: 2026-01-31 14:30:00
File Size: 1.3MB

Reading Excel File:
  [████████████████████████████████] 100%
  
  Sheets detected: 4
  Data sheet: "Room Data"
  Rows: 481 (1 header + 480 data)
  Columns: 88 parameters
  
Validation:
  ✓ All element IDs found in model
  ✓ All parameters exist
  ✓ All data types compatible
  ✓ All formulas valid
  ⚠ 12 conflicts detected

Conflicts:
  
  Room id:123456 - Parameter: "Room_Name"
    Excel value: "Conference Room A" (modified: 2026-01-31 14:30:00)
    Revit value: "Conference Room" (modified: 2026-01-31 10:15:00)
    Resolution: Use Excel (newer)
    
  Room id:123457 - Parameter: "Department"
    Excel value: "ADMIN" (modified: 2026-01-31 14:30:00)
    Revit value: "Administrative" (modified: 2026-01-31 10:15:00)
    Resolution: Use Excel (newer)
    
  ... (10 more conflicts)
  
Import Summary:
  Total rows: 480
  Will update: 480 elements
  Will skip: 0 elements
  Conflicts resolved: 12 (using newest)
  
Apply import? [Y/N]

Importing Changes:
  [████████████████████████████████] 100%
  
  Updated: 480 / 480 elements
  Parameters modified: 2,340
  Time: 1.8 seconds
  
Status: ✓ Import completed successfully
```

---

### **param-sync-excel** - Real-Time Excel Sync

**Syntax:**
```bash
param-sync-excel file=<path> [category=<category>] [interval=<seconds>] [bidirectional=true] [start=true]
```

**Description:**  
Sets up real-time bidirectional sync between Revit and Excel.

**Examples:**
```bash
# Start sync with defaults
param-sync-excel file="Rooms.xlsx" category=Rooms

# Custom sync interval
param-sync-excel file="Walls.xlsx" category=Walls interval=30

# One-way sync (Excel → Revit only)
param-sync-excel file="Data.xlsx" bidirectional=false
```

**Output:**
```
Excel Real-Time Sync:

Configuration:
  Excel File: Rooms.xlsx
  Category: Rooms
  Mode: Bidirectional
  Interval: 30 seconds
  Auto-start: Yes
  
Initialization:
  [████████████████████████████████] 100%
  
  Excel file opened
  FileSystemWatcher configured
  Sync engine started
  
Sync Status: ACTIVE ✓

Monitoring:
  - Watching for Excel file changes
  - Watching for Revit parameter changes
  - Auto-sync every 30 seconds
  
Recent Activity:
  [14:45:30] Revit → Excel: Room_Name updated (3 elements)
  [14:46:15] Excel → Revit: Department updated (5 elements)
  [14:47:00] Auto-sync completed (0 changes)
  [14:47:30] Auto-sync completed (0 changes)
  
Commands:
  - param-sync-pause: Pause sync
  - param-sync-resume: Resume sync
  - param-sync-stop: Stop sync
  - param-sync-status: Check status
  
Status: Monitoring for changes...
```

---

*Continues with 100+ more commands...*

---

## 🎓 USAGE EXAMPLES

### **Complete Workflow Examples**

#### **Example 1: AI-Powered Parameter Creation**

```bash
# Step 1: Suggest parameters for commercial office
param-suggest category=Walls context="commercial office, open plan, acoustic separation" topk=10

# Step 2: Create parameter from AI suggestion
param-create-ai prompt="Calculate acoustic rating based on wall thickness and material density"

# Step 3: Apply to all walls with batch update
param-batch-update category=Walls parameter="Acoustic_Rating_STC" 
                   value="[Wall_Thickness_mm] * 0.08 + 25" gpu=true

# Step 4: Export to Excel for review
param-export-excel file="Wall_Acoustics.xlsx" category=Walls 
                   parameters="Mark,Wall_Type,Acoustic_Rating_STC"

# Step 5: Set up real-time sync
param-sync-excel file="Wall_Acoustics.xlsx" category=Walls interval=30
```

#### **Example 2: Multi-Model Synchronization**

```bash
# Step 1: Sync parameters across architectural, structural, and MEP models
param-sync-models source="Arch.rvt"
                  targets="Struct.rvt,MEP.rvt"
                  parameters="Level,Phase,Room_Number,Room_Name"
                  mode=bidirectional
                  conflict-resolution=newest

# Step 2: Create parameter mapping (different names between models)
param-link-mapping source-model="Arch.rvt"
                    target-model="MEP.rvt"
                    mapping="Room_Number:Space_Number,Room_Name:Space_Name"
                    bidirectional=true

# Step 3: Check sync status
param-sync-status models="Struct.rvt,MEP.rvt"

# Step 4: Set up automatic sync on change
param-sync-auto enable=true models="Struct.rvt,MEP.rvt" trigger=onchange
```

#### **Example 3: Parameter Cleanup and Optimization**

```bash
# Step 1: Run health check
param-health analyze=true generate-report=true

# Step 2: Delete unused parameters
param-batch-delete filter=unused dry-run=true
param-batch-delete filter=unused backup=true

# Step 3: Optimize slow formulas
formula-optimize --batch benchmark=true

# Step 4: Fix formula errors
formula-fix --auto

# Step 5: Final health check
param-health export=pdf
```

---

*StingBIM V2.0 - Revolutionary Parameter Manager*
*Complete Command Reference - 200+ Commands*
