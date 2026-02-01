# STINGBIM - COMMAND REFERENCE PART 2
## Documentation, FM, Excel Sync & Advanced Commands

---

### **DOCUMENTATION COMMANDS**

#### `generate-drawings`
Automated drawing production

**Syntax:**
```
generate-drawings type=<all|arch|struct|mep> [scale=<1:50|1:100|1:200>]
                  [level=<specific|all>] [detail-level=<low|medium|high>]
```

**Examples:**
```
generate-drawings type=all
generate-drawings type=arch scale=1:100
generate-drawings type=mep level=L02 detail-level=high
```

**What It Does:**
1. Creates all required drawing sheets
2. Places plan views on sheets
3. Adds elevations and sections
4. Places detail views
5. Auto-annotates dimensions
6. Adds room tags and labels
7. Adds keynotes
8. Applies view templates
9. Adds title blocks
10. Populates sheet parameters
11. Numbers all sheets
12. Creates drawing index

**Drawing Generation Output:**
```
✓ Automated drawing production complete

Sheets Created: 127 total

Architectural (45 sheets):
  ✓ A-001: Site Plan (1:500)
  ✓ A-101 to A-112: Floor Plans (1:100)
  ✓ A-201 to A-204: Elevations (1:100)
  ✓ A-301 to A-308: Building Sections (1:50)
  ✓ A-401 to A-420: Details (1:10, 1:20)

Structural (28 sheets):
  ✓ S-101 to S-112: Foundation Plans (1:100)
  ✓ S-201 to S-212: Framing Plans (1:100)
  ✓ S-401 to S-404: Details (1:20)

Electrical (22 sheets):
  ✓ E-001: Single Line Diagram
  ✓ E-101 to E-112: Power Plans (1:100)
  ✓ E-201 to E-208: Lighting Plans (1:100)

Mechanical (18 sheets):
  ✓ M-001: System Diagram
  ✓ M-101 to M-112: HVAC Plans (1:100)
  ✓ M-201 to M-204: Sections (1:50)

Plumbing (14 sheets):
  ✓ P-001: Riser Diagrams
  ✓ P-101 to P-112: Plumbing Plans (1:100)

Annotations Added:
  → Dimensions: 5,680 automatic dimensions
  → Room tags: 480 rooms tagged
  → Door tags: 285 doors
  → Window tags: 185 windows
  → Equipment tags: 890 items
  → Keynotes: 1,250 notes
  → Grid lines: All plans
  → North arrows: All plans

Quality Checks:
  ✓ All views placed correctly
  ✓ No overlapping annotations
  ✓ All dimensions readable
  ✓ Title blocks complete
  ✓ Sheet numbers sequential
  ✓ Drawing index updated

Ready for: PDF export, printing, client review
```

**Time Saved:** 80 hours → 10 minutes (480x faster)

---

#### `generate-schedules`
Auto-create all project schedules

**Syntax:**
```
generate-schedules type=<all|specific> [export-excel=<yes|no>]
                   [formulas=<calculate|preserve>]
```

**Examples:**
```
generate-schedules type=all export-excel=yes
generate-schedules type=doors formulas=calculate
```

**What It Does:**
1. Creates all standard schedules (127 schedules)
2. Adds required fields
3. Applies filters
4. Adds formulas
5. Formats headers/text
6. Sorts data logically
7. Groups similar items
8. Calculates totals
9. Exports to Excel (if requested)
10. Sets up bidirectional sync

**Schedule Generation:**
```
✓ Schedule generation complete

Schedules Created: 127

Architectural (45):
  ✓ Door Schedule (285 doors)
  ✓ Window Schedule (185 windows)
  ✓ Room Schedule (480 rooms)
  ✓ Wall Schedule (12 types)
  ✓ Finish Schedule (480 rooms)
  ✓ Ceiling Schedule (480 rooms)
  ✓ And 39 more...

Structural (18):
  ✓ Column Schedule (248 columns)
  ✓ Beam Schedule (856 beams)
  ✓ Foundation Schedule (62 footings)
  ✓ Slab Schedule (12 floors)
  ✓ And 14 more...

MEP (64):
  ✓ Electrical Panel Schedule (45 panels)
  ✓ Lighting Fixture Schedule (1,280 fixtures)
  ✓ Receptacle Schedule (840 outlets)
  ✓ Equipment Schedule (285 items)
  ✓ Duct Schedule (560 ducts)
  ✓ Pipe Schedule (780 pipes)
  ✓ And 58 more...

Formulas Active:
  → Cost calculations: 45 schedules
  → Area calculations: 28 schedules
  → Load calculations: 32 schedules
  → Performance metrics: 22 schedules

Excel Export:
  ✓ Exported to: /Project/Schedules/
  ✓ Bidirectional sync enabled
  ✓ Formulas preserved
  ✓ Formatting retained

Total Quantity Takeoff Ready:
  → Materials: 5,680 items quantified
  → Labour: 2,340 activities calculated
  → Equipment: 890 items scheduled
  → Estimated total cost: UGX 25,450,000,000
```

---

#### `generate-specifications`
Automated specification writing

**Syntax:**
```
generate-specifications format=<masterformat|uniformat> [sections=<all|specific>]
```

**Examples:**
```
generate-specifications format=masterformat
generate-specifications format=uniformat sections=03,04,05
```

**What It Does:**
1. Analyzes all project materials
2. Analyzes all equipment
3. Generates spec sections
4. Organizes by Masterformat/Uniformat
5. Includes manufacturer data
6. Adds performance requirements
7. References applicable standards
8. Includes installation requirements
9. Adds quality assurance requirements
10. Creates table of contents
11. Formats as Word document

**Specifications Output:**
```
✓ Project specifications generated

Format: CSI MasterFormat 2020
Total Sections: 45
Total Pages: 385

Division 00 - Procurement and Contracting:
  ✓ 00 01 10 - Project Information
  ✓ 00 21 13 - Instructions to Bidders
  ✓ 00 52 00 - Agreement Form

Division 01 - General Requirements:
  ✓ 01 11 00 - Summary of Work
  ✓ 01 33 00 - Submittal Procedures
  ✓ 01 45 00 - Quality Control

Division 03 - Concrete:
  ✓ 03 20 00 - Concrete Reinforcing
    → Material: High tensile steel, Grade 460
    → Standards: BS 4449, BS 8666
    → Lap lengths: 40 × bar diameter
    → Cover: 50mm (external), 25mm (internal)
    
  ✓ 03 30 00 - Cast-in-Place Concrete
    → Strength: C25/30 (slabs), C30/37 (columns)
    → Standards: BS 8110, BS EN 206
    → Slump: 75-100mm
    → Curing: Minimum 7 days moist curing

Division 23 - HVAC:
  ✓ 23 05 00 - Common Work Results for HVAC
  ✓ 23 34 00 - Fans
  ✓ 23 64 00 - Water-Source Heat Pumps
  ✓ 23 74 00 - Packaged Water Chillers
    → Manufacturer: Carrier, Trane, or approved equal
    → Type: Water-cooled, centrifugal
    → Capacity: 170 tons (each of 2)
    → Efficiency: Minimum 6.2 EER
    → Refrigerant: R-134a
    → Controls: Building management system compatible
    → Standards: ASHRAE 90.1, AHRI 550/590

Division 26 - Electrical:
  ✓ 26 05 00 - Common Work Results for Electrical
  ✓ 26 24 00 - Switchboards and Panelboards
  ✓ 26 27 00 - Low-Voltage Distribution Equipment
  ✓ 26 50 00 - Lighting
    → Type: LED throughout
    → Efficacy: Minimum 100 lm/W
    → Color temperature: 4000K (offices), 3000K (amenities)
    → CRI: Minimum 80
    → Standards: NEC 2023, Energy Star

Standards Referenced: 185
Manufacturers Listed: 340

Document exported: Project_Specifications.docx
```

**Time Saved:** 60 hours → 8 minutes (450x faster)

---

### **COSTING COMMANDS**

#### `calculate-cost`
Comprehensive cost estimation

**Syntax:**
```
calculate-cost currency=<UGX|USD> [breakdown=<elemental|trade>] 
               [contingency=<pct>]
```

**Examples:**
```
calculate-cost currency=UGX
calculate-cost currency=USD breakdown=elemental contingency=10
```

**What It Does:**
1. Extracts all quantities from model
2. Matches to cost database
3. Applies regional pricing (Uganda)
4. Calculates material costs
5. Calculates labour costs
6. Calculates equipment costs
7. Applies wastage factors
8. Adds preliminaries
9. Adds contingency
10. Generates cost report

**Cost Estimate (Uganda Pricing):**
```
✓ Cost estimation complete (Kampala, Uganda rates)

PROJECT COST SUMMARY
====================

1. SUBSTRUCTURE                           UGX        USD
   Excavation                          125,000,000   33,784
   Blinding & DPC                       45,000,000   12,162
   Foundations                         680,000,000  183,784
   Ground floor slab                   420,000,000  113,514
   -------------------------------  --------------  -------
   Subtotal Substructure             1,270,000,000  343,243

2. SUPERSTRUCTURE
   Structural frame                  6,150,000,000  1,662,162
   Upper floors                      2,340,000,000    632,432
   Roof structure                      580,000,000    156,757
   Stairs & ramps                      285,000,000     77,027
   External walls                    1,450,000,000    391,892
   Internal walls & partitions         890,000,000    240,541
   -------------------------------  --------------  -------
   Subtotal Superstructure           11,695,000,000  3,160,811

3. INTERNAL FINISHES
   Floor finishes                      960,000,000    259,459
   Wall finishes                       680,000,000    183,784
   Ceiling finishes                    540,000,000    145,946
   -------------------------------  --------------  -------
   Subtotal Finishes                 2,180,000,000    589,189

4. SERVICES - ELECTRICAL
   Main switchboard & distribution   1,595,000,000    431,081
   Power installation                2,340,000,000    632,432
   Lighting                          1,680,000,000    454,054
   Small power                         890,000,000    240,541
   Fire alarm & detection              340,000,000     91,892
   Security systems                    225,000,000     60,811
   IT/Data infrastructure              450,000,000    121,622
   -------------------------------  --------------  -------
   Subtotal Electrical               7,520,000,000  2,032,432

5. SERVICES - MECHANICAL
   HVAC equipment                    3,850,000,000  1,040,541
   Ductwork & distribution           1,280,000,000    345,946
   Controls & BMS                      580,000,000    156,757
   Ventilation                         450,000,000    121,622
   -------------------------------  --------------  -------
   Subtotal Mechanical               6,160,000,000  1,664,865

6. SERVICES - PLUMBING
   Cold water system                   680,000,000    183,784
   Hot water system                    340,000,000     91,892
   Sanitary drainage                   580,000,000    156,757
   Storm water drainage                285,000,000     77,027
   Fire fighting                       890,000,000    240,541
   -------------------------------  --------------  -------
   Subtotal Plumbing                 2,775,000,000    750,000

7. EXTERNAL WORKS
   Site preparation                    340,000,000     91,892
   Roads & parking                   1,450,000,000    391,892
   Drainage                            580,000,000    156,757
   Landscaping                         285,000,000     77,027
   External services                   450,000,000    121,622
   -------------------------------  --------------  -------
   Subtotal External Works           3,105,000,000    839,189

8. PRELIMINARIES & GENERAL
   Site establishment                  450,000,000    121,622
   Temporary works                     580,000,000    156,757
   Site management                     890,000,000    240,541
   Insurance & bonds                   340,000,000     91,892
   -------------------------------  --------------  -------
   Subtotal Preliminaries            2,260,000,000    610,811

   ===============================  ==============  =======
   SUBTOTAL                         36,965,000,000  9,990,541

   Contingency (5%)                  1,848,250,000    499,527
   ===============================  ==============  =======
   TOTAL PROJECT COST               38,813,250,000 10,490,068

COST ANALYSIS
=============
Cost per m²:                      UGX 3,234,438 / USD 874/m²
Cost per person (800 occupants):  UGX 48,516,563 / USD 13,113

BREAKDOWN BY TRADE
==================
Civil works:                          8.2%
Structural works:                    31.6%
Architectural finishes:               5.6%
Electrical services:                 19.4%
Mechanical services:                 15.9%
Plumbing services:                    7.1%
External works:                       8.0%
Preliminaries:                        4.2%

REGIONAL COMPARISONS
====================
Kampala average (offices): UGX 3,200,000/m² → Project: +1.1%
Nairobi equivalent:        UGX 3,850,000/m² → Savings: -16%
Lagos equivalent:          UGX 4,100,000/m² → Savings: -21%

COST OPTIMIZATION OPPORTUNITIES
================================
1. VRF system instead of chilled water: -8% on HVAC
2. Optimize structural grid: -3% on structure
3. Local materials preference: -5% on finishes
4. Value engineering potential: UGX 1,940,663,000 (5%)

Export: Cost_Estimate_Detailed.xlsx (with full breakdown)
```

**Time Saved:** 20 hours → 2 minutes (600x faster)

---

#### `optimize-cost`
AI-powered cost optimization

**Syntax:**
```
optimize-cost target-reduction=<pct> [constraints=<quality|time|both>]
              [preserve=<critical-systems>]
```

**Examples:**
```
optimize-cost target-reduction=10
optimize-cost target-reduction=15 constraints=quality preserve=mep
```

**What It Does:**
1. Analyzes all cost components
2. Identifies optimization opportunities
3. Suggests alternative materials
4. Suggests alternative systems
5. Optimizes specifications
6. Maintains code compliance
7. Preserves quality (if constrained)
8. Re-calculates costs
9. Generates comparison report
10. Shows impact on schedule

**Cost Optimization Report:**
```
✓ Cost optimization analysis complete

TARGET: 10% reduction (UGX 3,881,325,000)

OPTIMIZATION RECOMMENDATIONS
=============================

1. STRUCTURAL OPTIMIZATION
   Current: Steel frame + composite slab
   Proposed: Flat slab concrete frame (post-tensioned)
   
   Impact:
   → Cost: -UGX 1,240,000,000 (-20% on structure)
   → Schedule: +2 weeks (formwork intensive)
   → Quality: Equivalent performance
   → Risk: Low (proven system in Uganda)
   
   Acceptance: RECOMMENDED ✓

2. FACADE SYSTEM
   Current: Curtain wall (40% glazing)
   Proposed: Block wall with punched windows (35% glazing)
   
   Impact:
   → Cost: -UGX 580,000,000 (-40% on facade)
   → Energy: +12% cooling load
   → Aesthetics: Less modern appearance
   → Risk: Medium (affects design intent)
   
   Acceptance: REVIEW REQUIRED ⚠

3. HVAC SYSTEM
   Current: Chilled water central plant
   Proposed: VRF multi-split system
   
   Impact:
   → Cost: -UGX 920,000,000 (-15% on HVAC)
   → Energy: -8% annual consumption
   → Maintenance: Simpler maintenance
   → Flexibility: Better zone control
   → Risk: Low (reliable technology)
   
   Acceptance: STRONGLY RECOMMENDED ✓✓

4. FINISHES
   Current: Imported tiles, premium fixtures
   Proposed: Local tiles, standard fixtures
   
   Impact:
   → Cost: -UGX 340,000,000 (-16% on finishes)
   → Quality: Acceptable (local products improving)
   → Lead time: -4 weeks (local supply)
   → Risk: Low
   
   Acceptance: RECOMMENDED ✓

5. ELECTRICAL DISTRIBUTION
   Current: Individual floor panels
   Proposed: Optimized riser layout
   
   Impact:
   → Cost: -UGX 285,000,000 (-4% on electrical)
   → Performance: Equivalent
   → Risk: Very low (design optimization)
   
   Acceptance: RECOMMENDED ✓

OPTIMIZATION SUMMARY
====================
Recommendations accepted:          4 of 5
Total savings achieved:            UGX 3,785,000,000
Target savings:                    UGX 3,881,325,000
Achievement:                       97.5% of target

REVISED PROJECT COST
====================
Original estimate:                 UGX 38,813,250,000
Less optimizations:                UGX  3,785,000,000
Revised total:                     UGX 35,028,250,000

Cost per m²:                       UGX 2,919,021/m² (-9.8%)

SCHEDULE IMPACT
===============
Flat slab construction:            +2 weeks
Local material sourcing:           -4 weeks
Net schedule impact:               -2 weeks (FASTER!)

RISK ASSESSMENT
===============
Technical risk:                    LOW
Commercial risk:                   LOW
Programme risk:                    LOW
Overall risk:                      LOW - PROCEED ✓

Next step: Review facade recommendation with client
           Approve other optimizations to proceed
```

**Time Saved:** 16 hours → 5 minutes (192x faster)

---

### **FACILITY MANAGEMENT COMMANDS**

#### `prepare-fm-handover`
Complete FM data preparation

**Syntax:**
```
prepare-fm-handover format=<cobie|proprietary> [include-om=<yes|no>]
```

**Examples:**
```
prepare-fm-handover format=cobie
prepare-fm-handover format=cobie include-om=yes
```

**What It Does:**
1. Extracts all asset data
2. Validates completeness
3. Assigns asset IDs
4. Generates O&M manuals
5. Creates warranty register
6. Exports COBie file
7. Creates asset register
8. Generates space data
9. Creates system diagrams
10. Packages all deliverables

**FM Handover Package:**
```
✓ FM handover package prepared

ASSET INVENTORY
===============
Total assets tracked: 2,840

By Category:
  → HVAC equipment:           285 items
  → Electrical equipment:     890 items
  → Plumbing fixtures:        680 items
  → Fire protection:          420 items
  → Elevators:                  3 items
  → Doors:                    285 items
  → Windows:                  185 items
  → Lighting fixtures:      1,280 items
  → Finishes:                 480 rooms

DATA COMPLETENESS
=================
  ✓ Equipment names:          100%
  ✓ Manufacturers:             98%
  ✓ Model numbers:             97%
  ✓ Installation dates:        100%
  ✓ Warranty info:             95%
  ✓ O&M manuals:               92%
  ✓ Asset locations:           100%
  ✓ Serial numbers:            89%

⚠ Missing Data:
  → 8 items missing warranty info
  → 15 items missing serial numbers
  → 25 items missing O&M manuals

DELIVERABLES CREATED
====================
1. COBie Spreadsheet
   ✓ File: Project_COBie.xlsx
   ✓ Format: COBie 2.4
   ✓ Validation: 100% compliant
   ✓ Sheets: 18 worksheets
   ✓ Records: 2,840 assets

2. Asset Register
   ✓ File: Asset_Register.xlsx
   ✓ Format: Custom template
   ✓ QR codes: Generated for all assets
   ✓ Photos: 2,150 equipment photos

3. O&M Manuals
   ✓ Folder: /FM_Handover/OM_Manuals/
   ✓ HVAC: 285 PDFs
   ✓ Electrical: 890 PDFs
   ✓ Plumbing: 680 PDFs
   ✓ Other: 420 PDFs
   ✓ Total size: 8.5 GB

4. Warranty Register
   ✓ File: Warranty_Register.xlsx
   ✓ Active warranties: 2,745
   ✓ Warranty value: UGX 1,850,000,000
   ✓ Expiry tracking: Alert system configured

5. Maintenance Schedules
   ✓ File: Maintenance_Schedules.xlsx
   ✓ Tasks: 1,680 scheduled tasks
   ✓ Frequency: Daily to annual
   ✓ Estimated annual cost: UGX 450,000,000

6. Space Data
   ✓ File: Space_Data.xlsx
   ✓ Rooms: 480 spaces
   ✓ Areas: Gross & net calculated
   ✓ Occupancy: Design loads included

7. System Diagrams
   ✓ Folder: /FM_Handover/Diagrams/
   ✓ HVAC schematics: 12 diagrams
   ✓ Electrical SLDs: 18 diagrams
   ✓ Plumbing risers: 8 diagrams
   ✓ Format: PDF + Revit views

8. As-Built Drawings
   ✓ Folder: /FM_Handover/Drawings/
   ✓ Sheets: 127 drawings
   ✓ Format: PDF (stamped "AS-BUILT")

HANDOVER PACKAGE
================
Location: /FM_Handover_Package/
Total size: 12.4 GB
Format: ZIP archive + DVD image

Ready for: Facility management team
Next step: setup-fm-system (configure CAFM system)
```

---

#### `setup-fm-system`
Configure facility management system

**Syntax:**
```
setup-fm-system [cmms=<integrated|standalone>] [mobile=<yes|no>]
```

**What It Does:**
1. Imports asset data
2. Configures maintenance schedules
3. Sets up work order system
4. Configures energy monitoring
5. Sets up space management
6. Creates user accounts
7. Configures alerts
8. Sets up reporting
9. Configures mobile access
10. Trains system

---

### **EXCEL INTEGRATION COMMANDS**

#### `excel-export`
Export schedules to Excel

**Syntax:**
```
excel-export schedules=<all|specific> [format=<standard|custom>] 
             [sync=<enable|disable>]
```

**Examples:**
```
excel-export schedules=all sync=enable
excel-export schedules="Door Schedule,Window Schedule" format=custom
```

**What It Does:**
1. Exports selected schedules
2. Preserves formulas
3. Preserves formatting
4. Adds data validation
5. Embeds metadata for sync
6. Sets up bidirectional sync
7. Configures conflict resolution
8. Creates Excel template

**Excel Export:**
```
✓ Excel export complete

Schedules Exported: 127

Files Created:
  → /Excel_Sync/Architectural/
    - Doors.xlsx (285 doors)
    - Windows.xlsx (185 windows)
    - Rooms.xlsx (480 rooms)
    - Walls.xlsx (47 types)
    - Finishes.xlsx (480 rooms)
    ... (40 more files)

  → /Excel_Sync/Structural/
    - Columns.xlsx (248 columns)
    - Beams.xlsx (856 beams)
    - Foundations.xlsx (62 footings)
    ... (15 more files)

  → /Excel_Sync/MEP_Electrical/
    - Panels.xlsx (45 panels)
    - Lighting.xlsx (1,280 fixtures)
    - Power.xlsx (840 outlets)
    ... (19 more files)

  → /Excel_Sync/MEP_Mechanical/
    - Equipment.xlsx (285 items)
    - Ducts.xlsx (560 ducts)
    ... (18 more files)

  → /Excel_Sync/MEP_Plumbing/
    - Fixtures.xlsx (680 fixtures)
    - Pipes.xlsx (780 pipes)
    ... (12 more files)

Features Enabled:
  ✓ Formulas preserved (850 formulas)
  ✓ Data validation (1,250 fields)
  ✓ Conditional formatting
  ✓ Dropdown lists
  ✓ Comments preserved
  ✓ Metadata embedded
  ✓ Bidirectional sync active
  ✓ Auto-sync interval: 30 seconds
  ✓ Conflict resolution: Prompt user

Sync Configuration:
  → Monitor folder: /Excel_Sync/
  → Sync log: Excel_Sync_Log.txt
  → Backup folder: /Excel_Sync/Backups/
  → Backup frequency: Every sync

Instructions:
  1. Edit Excel files as needed
  2. Save changes (auto-sync will trigger)
  3. Or use: excel-import to manually sync
  4. Check sync log for any conflicts
```

---

#### `excel-import`
Import Excel changes to Revit

**Syntax:**
```
excel-import file=<path> [preview=<yes|no>] [conflicts=<prompt|excel-wins|revit-wins>]
```

**Examples:**
```
excel-import file="Doors.xlsx" preview=yes
excel-import file="All" conflicts=excel-wins
```

**What It Does:**
1. Reads Excel file
2. Compares with Revit data
3. Identifies changes
4. Highlights conflicts
5. Shows preview (if requested)
6. Updates Revit parameters
7. Logs all changes
8. Creates backup
9. Generates change report

**Excel Import:**
```
✓ Excel import analysis complete

File: Doors.xlsx
Last modified: 2026-01-31 14:35:20

CHANGES DETECTED: 47

Added:
  → 3 new doors (rows 286-288)
    - D-286: Office entrance (900mm)
    - D-287: Storage (800mm)
    - D-288: Emergency exit (1200mm)

Modified:
  → 42 doors updated
    Changes by column:
    - Fire Rating: 18 changes
    - Hardware: 12 changes
    - Unit Cost: 8 changes
    - Notes: 4 changes

Deleted:
  → 2 doors removed (D-145, D-201)
    ⚠ Warning: These elements still exist in Revit
    Action: Archive in Revit or restore in Excel?

CONFLICTS: 3

1. Door D-045
   Excel:    Fire Rating = "60min"
   Revit:    Fire Rating = "90min"
   Modified: Excel (2026-01-31 14:35), Revit (2026-01-31 14:40)
   Action:   ? (Prompt user)

2. Door D-128
   Excel:    Width = 1000mm
   Revit:    Width = 900mm
   Modified: Excel (yesterday), Revit (today)
   Action:   ? (Prompt user)

3. Door D-234
   Excel:    Hardware = "Panic bar"
   Revit:    Hardware = "Standard lever"
   Modified: Both today
   Action:   ? (Prompt user)

VALIDATION ISSUES: 2

⚠ D-286: Fire rating "120min" not in validation list
   Valid options: 30min, 60min, 90min
   Suggestion: Change to 90min?

⚠ D-287: Width 750mm below minimum (800mm per code)
   Action: Correct in Excel or override?

PREVIEW MODE: Enabled
No changes applied yet.

Options:
  1. Apply all changes (excel-wins)
  2. Skip conflicts (keep Revit values)
  3. Resolve conflicts one by one
  4. Cancel import

Command: ? _
```

---

### **ANALYSIS COMMANDS**

#### `analyze-energy`
Building energy analysis

**Syntax:**
```
analyze-energy [standard=<ASHRAE90.1|LEED|local>] [baseline=<yes|no>]
```

**Examples:**
```
analyze-energy standard=ASHRAE90.1
analyze-energy standard=LEED baseline=yes
```

**What It Does:**
1. Runs energy simulation
2. Calculates annual consumption
3. Breaks down by end use
4. Compares to baseline/code
5. Identifies improvement opportunities
6. Calculates carbon emissions
7. Estimates operating costs
8. Generates energy model
9. Creates compliance report

**Energy Analysis:**
```
✓ Energy analysis complete (ASHRAE 90.1-2019 Appendix G)

BUILDING CHARACTERISTICS
========================
Location: Kampala, Uganda (Climate Zone 1A - Hot Humid)
Area: 12,000 m² conditioned space
Occupancy: 800 people
Hours: 60 hours/week

ANNUAL ENERGY CONSUMPTION
=========================
Total: 1,450,000 kWh/year
EUI: 121 kWh/m²/year

By End Use:
  → HVAC:           650,000 kWh (45%)
  → Lighting:       385,000 kWh (27%)
  → Equipment:      290,000 kWh (20%)
  → Pumps/fans:      85,000 kWh (6%)
  → Misc:            40,000 kWh (2%)

Monthly Peak Demand: 580 kW (March - hottest month)

CODE COMPLIANCE
===============
Baseline Building (ASHRAE 90.1-2019): 1,680,000 kWh/year
Proposed Building:                      1,450,000 kWh/year
Improvement:                            -14% (COMPLIANT ✓)

Energy Cost Index: 12.1% below minimum requirement

CARBON EMISSIONS
================
Annual CO₂e: 1,015 tonnes
Grid intensity: 0.70 kg CO₂e/kWh (Uganda grid mix)

By source:
  → Fossil fuels:    710 tonnes (70%)
  → Hydro:          305 tonnes (30%)

OPERATING COSTS (Uganda Rates)
===============================
Electricity: 1,450,000 kWh × UGX 800/kWh = UGX 1,160,000,000/year
Monthly average: UGX 96,666,667

IMPROVEMENT OPPORTUNITIES
=========================
1. Solar PV System (500 kWp rooftop)
   → Annual generation: 780,000 kWh
   → Self-consumption: 650,000 kWh (83%)
   → Grid export: 130,000 kWh
   → Savings: -UGX 520,000,000/year (-45%)
   → Payback: 6.2 years
   → CO₂ reduction: -455 tonnes/year

2. LED Lighting Upgrade (already included)
   → Status: IMPLEMENTED ✓

3. VRF System Efficiency
   → Current EER: 3.2
   → High-efficiency option: EER 3.8
   → Savings: -85,000 kWh/year (-6% HVAC)
   → Cost premium: UGX 120,000,000
   → Payback: 1.8 years

4. Natural Ventilation (mixed-mode)
   → Applicable hours: 2,840 hours/year (32%)
   → HVAC savings: -95,000 kWh/year
   → Design modification required
   → Cost: UGX 45,000,000
   → Payback: 0.6 years

5. Energy Recovery Ventilation
   → Heat recovery efficiency: 75%
   → Savings: -120,000 kWh/year (-18% ventilation)
   → Cost: UGX 180,000,000
   → Payback: 1.9 years

RECOMMENDED PACKAGE
===================
Implement: Solar PV + VRF efficiency + ERV
Total savings: -850,000 kWh/year (-59%)
Total cost: UGX 800,000,000
Simple payback: 1.7 years
20-year NPV: UGX 12,500,000,000

CERTIFICATION POTENTIAL
=======================
  ✓ ASHRAE 90.1: Compliant (-14%)
  ✓ Uganda Energy Code: Exceeds requirements
  ✓ LEED v4 Energy prerequisite: Met
  ✓ LEED Energy points: 12 points (optimized case)
  ✓ Green Star: 5 stars potential
```

---

**Continue with final sections...**
