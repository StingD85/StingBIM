# STINGBIM - COMMAND REFERENCE & API DOCUMENTATION
## Complete Command System for Maximum Productivity

---

## 🎯 COMMAND PHILOSOPHY

**StingBIM uses natural, English-like commands that are:**
- **Intuitive**: Easy to remember and understand
- **Powerful**: One command can trigger hundreds of automated tasks
- **Flexible**: Optional parameters for customization
- **Forgiving**: Smart error handling and suggestions
- **Fast**: Average command execution < 5 seconds

**Command Syntax:**
```
command-name [required-param] [optional-param=value] [--flag]
```

---

## 📋 COMPLETE COMMAND CATALOG (150+ COMMANDS)

### **PROJECT MANAGEMENT COMMANDS**

#### `new-project`
Create a new BIM project with full setup

**Syntax:**
```
new-project name="Project Name" type=<office|residential|industrial|mixed-use> 
            location="City, Country" area=<sqm> floors=<count>
            [template=<template-name>] [standards=<code-list>]
```

**Parameters:**
- `name` (required): Project name
- `type` (required): Building type (affects default standards)
- `location` (required): Physical location (affects climate, codes)
- `area` (required): Gross floor area in square meters
- `floors` (required): Number of floors
- `template` (optional): Project template to use
- `standards` (optional): Comma-separated list of standards (auto-selected if omitted)

**Examples:**
```
new-project name="Kampala Office Tower" type=office location="Kampala, Uganda" 
            area=12000 floors=10

new-project name="Residential Block A" type=residential location="Nairobi, Kenya" 
            area=5000 floors=5 standards=IBC-2024,NEC-2023,Kenya-BC

new-project name="Factory Complex" type=industrial location="Dar es Salaam, Tanzania" 
            area=25000 floors=2 template="Industrial-Template-01"
```

**What It Does:**
1. Creates Revit project file with proper settings
2. Sets up levels based on floor count (default 3.5m floor-to-floor)
3. Loads applicable building codes (80,000+ rules)
4. Creates default schedules (100+ schedules)
5. Loads all parameters (1,500+ parameters)
6. Sets up worksets for collaboration
7. Configures view templates
8. Creates default sheets
9. Sets up FM structure
10. Loads material/equipment libraries
11. Configures Excel sync folders
12. Creates project dashboard

**Output:**
```
✓ Project created: Kampala_Office_Tower.rvt
✓ Loaded standards: IBC-2024, NEC-2023, ASHRAE-62.1, Uganda-BC
✓ Created 10 levels (GL to Roof)
✓ Loaded 1,548 parameters
✓ Created 127 schedules
✓ Loaded 5,000+ materials
✓ Loaded 10,000+ equipment items
✓ Project ready for design!

Next steps:
  → analyze-site (import site boundaries)
  → generate-massing (create building mass)
  → design-floors (design floor plans)
```

**Time Saved:** 4 hours → 30 seconds (480x faster)

---

#### `set-levels`
Configure building levels

**Syntax:**
```
set-levels count=<number> height=<meters> [basement=<count>] [roof=<type>]
```

**Examples:**
```
set-levels count=12 height=3.5
set-levels count=8 height=4.0 basement=2
set-levels count=15 height=3.2 basement=1 roof=mechanical
```

**What It Does:**
1. Creates levels with proper naming (GL, L01, L02, etc.)
2. Sets floor-to-floor heights
3. Creates basement levels if specified (B01, B02, etc.)
4. Adds roof/mechanical levels
5. Creates corresponding plan views
6. Creates section views
7. Sets up elevation views

---

### **SITE & MASSING COMMANDS**

#### `analyze-site`
Import and analyze site conditions

**Syntax:**
```
analyze-site file=<path> [format=<dwg|pdf|shapefile>] [scale=<ratio>]
```

**Examples:**
```
analyze-site file="SitePlan.dwg"
analyze-site file="Survey.pdf" scale=1:500
analyze-site file="TopoMap.shp" format=shapefile
```

**What It Does:**
1. Imports site boundary
2. Imports topography (if available)
3. Identifies setback requirements from local codes
4. Analyzes solar orientation
5. Identifies utilities (if shown)
6. Calculates site area
7. Determines allowable coverage
8. Suggests building orientation
9. Creates site plan view

**AI Analysis Output:**
```
✓ Site imported: 2,450 m² total area
✓ Setbacks detected: Front 5m, Sides 3m, Rear 3m
✓ Maximum coverage: 60% (1,470 m²)
✓ Building height limit: 35m (Uganda-BC)
✓ Solar orientation: Optimal east-west orientation for daylighting
✓ Slope analysis: Relatively flat (0.5% average grade)
⚠ Notice: Site within 100m of wetland - NEMA approval required
✓ Prevailing wind: Southeast (consider for natural ventilation)

Recommendations:
  → Orient building east-west for solar control
  → Main entrance on north side (street access)
  → Natural ventilation possible
```

---

#### `generate-massing`
AI-generated building massing

**Syntax:**
```
generate-massing target-area=<sqm> efficiency=<0.7-0.9> 
                 [orientation=<N|S|E|W>] [setbacks=<auto|custom>]
                 [cores=<count>] [core-location=<center|edge>]
```

**Examples:**
```
generate-massing target-area=12000 efficiency=0.85
generate-massing target-area=8000 efficiency=0.80 cores=2 core-location=edge
generate-massing target-area=15000 efficiency=0.85 orientation=E setbacks=custom
```

**What It Does:**
1. Calculates required footprint from area + efficiency
2. Respects site setbacks (auto-detected or custom)
3. Places cores (stairs, elevators, services) optimally
4. Creates floor plate layouts
5. Analyzes aspect ratio for daylighting
6. Checks code compliance (area, height, exits)
7. Optimizes for energy performance
8. Creates conceptual 3D mass model
9. Calculates gross/net areas

**AI Analysis:**
```
✓ Massing generated for 12,000 m² GFA
✓ Footprint: 1,200 m² per floor × 10 floors
✓ Core: Central location (optimal for office)
✓ Efficiency: 85% (target achieved)
✓ Aspect ratio: 1:2.5 (good for daylighting)
✓ Perimeter zone depth: 6m (80% daylit area)
✓ Travel distance to exits: <45m (compliant)
✓ Building orientation: East-West (15% energy savings)

Code Compliance:
  ✓ Uganda BC: Area compliant
  ✓ IBC 2024: Occupancy load within limits
  ✓ Fire exits: 2 required, 2 provided
  ✓ Accessibility: Elevator access on all floors
```

**Time Saved:** 8 hours → 2 minutes (240x faster)

---

### **ARCHITECTURAL DESIGN COMMANDS**

#### `design-floors`
Auto-generate floor layouts

**Syntax:**
```
design-floors layout=<open|cellular|mixed> module=<meters> 
              [circulation=<single|double|corridor>]
              [toilets=<auto|custom>] [service-rooms=<yes|no>]
```

**Examples:**
```
design-floors layout=open module=1.2
design-floors layout=cellular module=3.0 circulation=corridor
design-floors layout=mixed module=1.5 toilets=auto service-rooms=yes
```

**What It Does:**
1. Generates space layouts based on building type
2. Places columns on structural grid
3. Creates core walls (shafts, stairs, elevators)
4. Designs perimeter walls
5. Places partition walls (if cellular layout)
6. Sizes and places toilets per occupancy
7. Places service rooms (electrical, telecom, cleaners)
8. Creates door openings
9. Places windows based on daylighting
10. Labels all rooms
11. Calculates areas
12. Checks code compliance

**AI Design Output:**
```
✓ Floor layout generated (Typical Floor)
✓ Structural grid: 7.2m × 7.2m (optimal for office)
✓ Core: 12m × 8m (stairs, 2 elevators, 1 service lift, toilets)
✓ Open office area: 850 m²
✓ Meeting rooms: 4 rooms (100 m² total)
✓ Toilets: M=3 WC + 2 urinals, F=5 WC (IPC compliant)
✓ Electrical room: 15 m² (NEC requirement met)
✓ Telecom room: 8 m² (TIA-569 compliant)
✓ Doors: 28 placed (all code-compliant widths)
✓ Windows: 45% glazing ratio (optimal for daylighting)

Occupancy Calculation:
  → Net office area: 850 m²
  → Occupancy @ 10 m²/person: 85 people
  → With meeting rooms: 110 people total
  → Exit capacity: 120 people (adequate)
  → Toilet fixtures: IPC compliant for 110 occupants
```

**Time Saved:** 40 hours → 5 minutes (480x faster)

---

#### `import-plan-image`
Image-to-BIM conversion (AI-powered)

**Syntax:**
```
import-plan-image file=<path> level=<level-name> [scale=<ratio>] 
                  [quality=<draft|standard|precise>]
```

**Examples:**
```
import-plan-image file="FloorPlan.pdf" level=L01 scale=1:100
import-plan-image file="HandSketch.jpg" level=L02 quality=draft
import-plan-image file="OldDrawing.dwg" level=GL quality=precise
```

**What It Does:**
1. Loads image (PDF, JPEG, PNG, DWG)
2. AI detects scale (or uses provided)
3. AI recognizes walls (external, internal, load-bearing)
4. AI detects doors (swing direction, width)
5. AI detects windows (size, sill height)
6. OCR reads room labels and dimensions
7. AI detects symbols (electrical, plumbing, furniture)
8. Creates Revit elements
9. Assigns materials
10. Generates schedule entries
11. Provides confidence scores
12. Allows manual verification/correction

**AI Recognition Output:**
```
✓ Image loaded: FloorPlan.pdf
✓ Scale detected: 1:100 (20 pixels/meter)
✓ AI Analysis complete:

Detected Elements:
  → Walls: 47 detected (confidence: 95%)
    - External: 12 walls (200mm thick)
    - Internal: 35 walls (100mm thick)
  → Doors: 18 detected (confidence: 92%)
    - Single: 15 doors
    - Double: 3 doors
  → Windows: 23 detected (confidence: 88%)
  → Rooms: 12 labeled (OCR confidence: 94%)
  → Furniture: 45 items (confidence: 85%)
  → Electrical outlets: 32 (confidence: 78%)

⚠ Review Required:
  → 3 doors need swing direction verification
  → 2 walls unclear - manual check needed
  → Room "Stor" - full name unclear

Ready to create elements? (Y/N)
```

**Time Saved:** 20 hours → 10 minutes (120x faster)

---

#### `auto-place-doors`
Intelligent door placement

**Syntax:**
```
auto-place-doors [type=<single|double|sliding>] [width=<mm>] [fire-rated=<yes|no>]
```

**Examples:**
```
auto-place-doors
auto-place-doors type=single width=900
auto-place-doors fire-rated=yes
```

**What It Does:**
1. Analyzes room adjacencies
2. Determines required door locations
3. Checks egress requirements (IBC/Uganda-BC)
4. Sizes doors based on occupancy
5. Sets swing direction for safety
6. Places fire doors where required
7. Ensures accessibility (clear width, hardware)
8. Checks travel distances
9. Tags all doors
10. Generates door schedule

**AI Placement Logic:**
```
✓ Door analysis complete

Egress Analysis:
  → Building occupancy: 800 people
  → Required exit capacity: 400 inches (800 × 0.5")
  → Provided exit width: 432 inches (adequate)
  → Max travel distance: 42m (limit: 45m) ✓

Doors Placed:
  → Main entrance: 2 × 1200mm double doors (fire-rated 90min)
  → Stair doors: 8 × 900mm (fire-rated 60min, self-closing)
  → Office entries: 18 × 900mm single doors
  → Toilet doors: 12 × 800mm (accessible compliant)
  → Service rooms: 6 × 800mm

Code Compliance:
  ✓ All doors meet minimum width (IBC 1010.1.1)
  ✓ Landing sizes adequate (IBC 1010.1.6)
  ✓ Door hardware: ADA compliant handles
  ✓ Fire doors properly located (IBC 716)
  ✓ Panic hardware on egress doors (IBC 1010.1.10)
```

---

#### `auto-place-windows`
AI-powered window placement

**Syntax:**
```
auto-place-windows target-glazing=<pct> [min-daylight=<pct>] 
                   [views=<yes|no>] [solar-control=<yes|no>]
```

**Examples:**
```
auto-place-windows target-glazing=40
auto-place-windows target-glazing=35 min-daylight=75
auto-place-windows target-glazing=50 views=yes solar-control=yes
```

**What It Does:**
1. Analyzes perimeter walls
2. Calculates optimal window sizes
3. Considers solar orientation
4. Analyzes daylighting requirements
5. Checks views (if requested)
6. Places windows at standard heights
7. Ensures structural constraints met
8. Calculates U-values, SHGC
9. Checks energy code compliance
10. Generates window schedule

**AI Window Design:**
```
✓ Window placement optimized

Daylighting Analysis:
  → Target glazing ratio: 40%
  → Achieved: 42% (1,450 m² glazing)
  → Daylit area (>300 lux): 78%
  → View windows: 95% of occupant positions

Solar Optimization:
  → South facade: 35% glazing (solar control glass, SHGC=0.25)
  → North facade: 55% glazing (clear glass, SHGC=0.70)
  → East/West facades: 40% glazing (mid-range SHGC=0.40)
  → External shading: South & west (15% energy savings)

Windows Placed:
  → Standard: 1.5m (W) × 1.8m (H), sill @ 750mm
  → Total windows: 85 units
  → Average U-value: 1.6 W/m²K (energy code compliant)

Energy Impact:
  → Annual cooling load: +125 MWh (solar gains)
  → Annual heating savings: +180 MWh (passive solar)
  → Daylighting savings: -95 MWh (reduced artificial lighting)
  → Net impact: -65 MWh/year (improvement)
```

**Time Saved:** 6 hours → 3 minutes (120x faster)

---

### **STRUCTURAL DESIGN COMMANDS**

#### `calculate-loads`
Comprehensive load calculation

**Syntax:**
```
calculate-loads [live-load=<kPa>] [snow-load=<auto|custom>] 
                [wind-speed=<auto|custom>] [seismic=<auto|yes|no>]
```

**Examples:**
```
calculate-loads
calculate-loads live-load=4.0 wind-speed=auto
calculate-loads seismic=yes
```

**What It Does:**
1. Determines dead loads (self-weight)
2. Applies live loads per code (IBC/Uganda-BC)
3. Calculates wind loads (ASCE 7)
4. Calculates seismic loads (if applicable)
5. Applies load combinations
6. Distributes loads to structural elements
7. Calculates tributary areas
8. Generates load diagrams
9. Creates load tables

**Load Calculation Output:**
```
✓ Load analysis complete per IBC 2024 & ASCE 7-22

Dead Loads:
  → Slab: 4.5 kPa (150mm concrete + finishes)
  → Partitions: 1.0 kPa (allowance)
  → Ceiling/MEP: 0.5 kPa
  → Total DL: 6.0 kPa

Live Loads:
  → Office areas: 2.4 kPa (IBC Table 1607.1)
  → Corridors: 4.8 kPa
  → Assembly: 4.8 kPa
  → Roof: 1.0 kPa (non-snow region)

Wind Loads (ASCE 7-22):
  → Basic wind speed: 35 m/s (Kampala, Uganda)
  → Exposure category: B (urban terrain)
  → Risk category: II (standard occupancy)
  → Design wind pressure: 1.2 kPa (windward @ roof)
  → Lateral load: 450 kN total

Seismic Loads:
  → Not applicable (Kampala - low seismic zone)

Load Combinations (7 combinations per ASCE 7):
  1.4D
  1.2D + 1.6L + 0.5Lr
  1.2D + 1.0W + L + 0.5Lr
  ... (4 more combinations)

Critical Load Case:
  → Governing: 1.2D + 1.6L
  → Column C3: 2,450 kN (maximum axial load)
  → Beam B12: 285 kN·m (maximum moment)
```

---

#### `design-structure`
Automated structural design

**Syntax:**
```
design-structure material=<steel|concrete|timber> [code=<BS5950|EC3|ACI318>]
                 [optimize=<cost|carbon|speed>]
```

**Examples:**
```
design-structure material=steel code=BS5950
design-structure material=concrete code=ACI318 optimize=cost
design-structure material=timber code=EC5
```

**What It Does:**
1. Designs columns for axial + moment
2. Designs beams for moment + shear
3. Designs slabs for flexure
4. Designs foundations
5. Checks deflections
6. Designs connections
7. Optimizes member sizes
8. Checks code compliance
9. Generates calculations
10. Creates structural drawings
11. Generates material takeoff

**Structural Design Output:**
```
✓ Structural design complete per BS 5950-1:2000

Material: Structural Steel Grade S275

Columns (48 total):
  → Ground floor: 254×254×107 UC (2,450 kN capacity)
  → Typical floors: 203×203×60 UC (850 kN capacity)
  → Top floors: 152×152×30 UC (320 kN capacity)
  → Utilization: 65-85% (economical)

Beams (156 total):
  → Primary: 457×191×74 UB (7.2m span)
  → Secondary: 305×165×40 UB (3.6m span)
  → Edge beams: 457×152×60 UB
  → Max deflection: L/420 (limit: L/360) ✓

Slab:
  → Composite metal deck: 150mm total depth
  → Concrete: C30/37 grade
  → Mesh: A252 top, A193 bottom
  → Span: 3.6m between secondary beams

Connections:
  → Column splices: Bolted flanges (M24 Grade 8.8)
  → Beam-column: Fin plates (M20 Grade 8.8)
  → Beam-beam: Web cleats

Foundations:
  → Pad footings: 2.5m × 2.5m × 0.8m deep
  → Soil bearing capacity: 200 kPa (assumed)
  → Reinforcement: H16 @ 150mm c/c both ways

Material Quantities:
  → Structural steel: 285 tonnes
  → Concrete (slabs): 1,800 m³
  → Concrete (foundations): 450 m³
  → Reinforcement: 95 tonnes
  → Bolts: 2,840 M20, 560 M24

Estimated Cost (Uganda):
  → Steel: UGX 4,275,000,000
  → Concrete: UGX 1,026,000,000
  → Labour: UGX 850,000,000
  → Total structure: UGX 6,151,000,000
```

**Time Saved:** 80 hours → 8 minutes (600x faster)

---

### **MEP DESIGN COMMANDS**

#### `calculate-electrical-load`
NEC 2023 compliant load calculation

**Syntax:**
```
calculate-electrical-load [voltage=<415|230>] [phases=<3|1>]
```

**Examples:**
```
calculate-electrical-load
calculate-electrical-load voltage=415 phases=3
```

**What It Does:**
1. Calculates lighting loads (NEC 220.12)
2. Calculates receptacle loads (NEC 220.14)
3. Calculates HVAC loads
4. Calculates motor loads
5. Applies demand factors (NEC 220.42-220.56)
6. Calculates feeder sizes
7. Checks voltage drop
8. Sizes main switchboard
9. Generates single-line diagram
10. Creates load schedule

**Load Calculation (NEC 2023):**
```
✓ Electrical load calculation complete per NEC 2023

General Lighting Load:
  → Office area: 12,000 m² × 37.6 VA/m² = 451 kVA
  → Demand factor (NEC 220.42): 35% above first 3 kVA
  → Demand load: 160 kVA

Receptacle Load:
  → Office: 180 VA/m² × 12,000 m² = 2,160 kVA
  → First 10 kVA @ 100% = 10 kVA
  → Remainder @ 50% = 1,075 kVA
  → Demand load: 1,085 kVA

HVAC Load:
  → Chillers: 220 kW
  → AHUs: 135 kW
  → Pumps: 45 kW
  → Total HVAC: 400 kW (no demand factor)

Motor Load:
  → Elevators (3 × 18.5 kW): 55.5 kW
  → Largest motor @ 125% (NEC 430.24)
  → Demand load: 60 kW

Total Connected Load: 3,071 kVA
Total Demand Load: 1,705 kVA
Diversity: 55.5%

Electrical Service:
  → Voltage: 415V, 3-phase
  → Design current: 2,370 A
  → Main switchboard: 2,500 A
  → Incoming cable: 3 × 400 mm² per phase + neutral
  → Backup generator: 1,800 kVA (covers essential loads)

Distribution:
  → Main distribution board: 2,500A
  → Floor distribution boards (10×): 250A each
  → Final circuits: 1,280 circuits total
  → Cable sizing: Per NEC Table 310.16 with derating

Estimated Costs (Uganda):
  → Main switchboard: UGX 450,000,000
  → Cables/conduits: UGX 680,000,000
  → Distribution boards: UGX 125,000,000
  → Installation: UGX 340,000,000
  → Total electrical: UGX 1,595,000,000
```

---

#### `design-distribution`
Electrical distribution system design

**Syntax:**
```
design-distribution [backup-power=<yes|no>] [solar-pv=<yes|no>]
```

**Examples:**
```
design-distribution
design-distribution backup-power=yes
design-distribution backup-power=yes solar-pv=yes
```

**What It Does:**
1. Designs main switchboard layout
2. Calculates distribution board locations
3. Sizes all cables (with derating)
4. Designs cable routing
5. Calculates voltage drop
6. Designs earthing system
7. Places panels optimally
8. Creates single-line diagram
9. Generates cable schedule
10. Generates panel schedules

---

#### `calculate-hvac-load`
ASHRAE compliant cooling/heating loads

**Syntax:**
```
calculate-hvac-load [method=<RTS|CLTD|detailed>]
```

**Examples:**
```
calculate-hvac-load
calculate-hvac-load method=RTS
```

**What It Does:**
1. Calculates solar heat gains
2. Calculates transmission loads
3. Calculates occupancy loads
4. Calculates equipment/lighting loads
5. Calculates infiltration/ventilation
6. Applies diversity factors
7. Calculates peak loads by zone
8. Calculates system loads
9. Sizes equipment
10. Generates load summary

**HVAC Load Calculation (ASHRAE):**
```
✓ Cooling load calculation per ASHRAE Fundamentals 2021

Building Data:
  → Location: Kampala, Uganda (0.3°N)
  → Outdoor design: 30°C DB / 24°C WB
  → Indoor design: 24°C / 50% RH

Heat Gains:

Envelope (Transmission):
  → Walls: 145 kW (U=0.5 W/m²K, A=3,200 m²)
  → Roof: 95 kW (U=0.35 W/m²K, A=1,200 m²)
  → Windows: 285 kW (U=1.6 W/m²K, SHGC=0.30, A=1,450 m²)
  → Subtotal: 525 kW

Internal Gains:
  → Occupants: 110 people × 120 W = 13.2 kW
  → Lighting: 12,000 m² × 12 W/m² = 144 kW
  → Equipment: 12,000 m² × 15 W/m² = 180 kW
  → Subtotal: 337 kW

Ventilation (ASHRAE 62.1):
  → Outdoor air: 12,000 CFM (5,664 L/s)
  → OA cooling load: 105 kW
  → OA latent load: 65 kW

Total Cooling Load:
  → Sensible: 967 kW
  → Latent: 95 kW
  → Total: 1,062 kW (302 tons)
  → Safety factor (10%): 1,168 kW (332 tons)

Equipment Sizing:
  → Chillers: 2 × 170 tons (1 duty + 1 standby)
  → Cooling towers: 2 × 200 tons
  → Chilled water pumps: 3 × 75 m³/h (2 duty + 1 standby)
  → AHUs: 8 units, total 120,000 CFM
  → FCUs: 85 units for perimeter zones

Energy Consumption Estimate:
  → Annual cooling: 650,000 kWh
  → Annual cost @ 800 UGX/kWh: UGX 520,000,000
  → With energy recovery: 485,000 kWh (-25%)
```

---

#### `design-hvac`
Complete HVAC system design

**Syntax:**
```
design-hvac system=<vrf|chilled-water|dx> [ventilation=<dedicated|combined>]
```

**Examples:**
```
design-hvac system=chilled-water
design-hvac system=vrf ventilation=dedicated
```

**What It Does:**
1. Designs central plant (if applicable)
2. Zones the building
3. Sizes equipment for each zone
4. Designs duct system
5. Sizes ductwork
6. Designs piping system
7. Sizes pipes
8. Places diffusers
9. Checks velocities/noise
10. Generates equipment schedules
11. Creates HVAC drawings

---

### **COORDINATION COMMANDS**

#### `coordinate-models`
Multi-discipline coordination

**Syntax:**
```
coordinate-models disciplines=<arch,struct,mep> [clash-tolerance=<mm>]
```

**Examples:**
```
coordinate-models disciplines=arch,struct,mep
coordinate-models disciplines=all clash-tolerance=50
```

**What It Does:**
1. Federates all models
2. Runs clash detection (hard clashes)
3. Checks clearances (soft clashes)
4. Analyzes critical clashes
5. Groups similar clashes
6. Prioritizes by severity
7. Generates clash report
8. Creates coordination views
9. Exports BCF issues

**Clash Detection Results:**
```
✓ Clash detection complete

Models Analyzed:
  → Architecture: 12,450 elements
  → Structure: 8,920 elements
  → MEP Electrical: 5,680 elements
  → MEP Mechanical: 4,230 elements
  → MEP Plumbing: 2,150 elements

Hard Clashes Found: 247
  → Critical (immediate fix): 45
  → High priority: 102
  → Medium priority: 85
  → Low priority: 15

Clash Categories:
  → Duct vs Structure: 85 clashes
  → Pipe vs Structure: 42 clashes
  → Conduit vs Structure: 38 clashes
  → Duct vs Pipe: 28 clashes
  → Equipment vs Architecture: 35 clashes
  → Other: 19 clashes

Top 5 Critical Clashes:
  1. Main chilled water pipe through beam (Grid C-3)
  2. Supply duct through structural column (Grid D-5)
  3. Electrical panel inside structural wall
  4. Fire sprinkler main through floor slab
  5. AHU conflicts with suspended ceiling height

Auto-Resolution Available: 128 clashes (52%)
Manual Resolution Required: 119 clashes (48%)

Next step: auto-resolve-clashes or review-clashes
```

---

#### `auto-resolve-clashes`
AI-powered clash resolution

**Syntax:**
```
auto-resolve-clashes [category=<all|specific>] [method=<reroute|resize|relocate>]
```

**What It Does:**
1. Analyzes each clash
2. Determines best resolution
3. Reroutes MEP systems
4. Resizes ducts/pipes if possible
5. Relocates equipment
6. Maintains code clearances
7. Preserves design intent
8. Updates all models
9. Re-runs clash detection
10. Reports changes

**Auto-Resolution Results:**
```
✓ Auto-resolution complete

Resolved: 128 clashes (52%)

Resolution Methods:
  → Rerouted pipes: 45 instances
  → Rerouted ducts: 38 instances
  → Resized ducts (smaller): 22 instances
  → Relocated equipment: 15 instances
  → Raised/lowered elements: 8 instances

Code Compliance Maintained:
  ✓ Minimum clearances: OK
  ✓ Access requirements: OK
  ✓ Fire separations: OK
  ✓ Headroom: OK

Remaining Clashes: 119 (require manual review)
  → 18 require structural coordination
  → 32 require architectural coordination
  → 69 require MEP coordination

BCF file exported: Coordination_Issues.bcf
Next step: Coordinate with teams on remaining issues
```

**Time Saved:** 40 hours → 15 minutes (160x faster)

---

**CONTINUE TO PART 2 FOR MORE COMMANDS...**
