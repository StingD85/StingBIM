# STINGBIM - COMPLETE COMMAND REFERENCE
## Natural Language Command System

---

## 🎯 COMMAND PHILOSOPHY

StingBIM uses natural language commands that feel like talking to an expert colleague:
- **Simple**: `design building`
- **Specific**: `design 5-story office building 2000 sqm per floor`
- **Complex**: `design office building with 5 floors, 2000 sqm each, open plan with perimeter offices, LEED Gold target, Uganda codes`

The AI engine understands context, remembers previous commands, and asks clarifying questions when needed.

---

## 📋 COMMAND CATEGORIES

### **1. PROJECT INITIALIZATION**

#### `new-project`
Creates a new StingBIM project with all required settings.

**Syntax:**
```
new-project [name="Project Name"] [location="City, Country"] [type=Building_Type] [codes=Code_List]
```

**Examples:**
```
new-project
new-project name="Kampala Office Tower" location="Kampala, Uganda"
new-project name="Industrial Warehouse" type=warehouse codes=IBC2024,NEC2023,Uganda
```

**Parameters:**
- `name`: Project name (default: "Untitled Project")
- `location`: Geographic location for code/climate selection
- `type`: Building type (office, residential, industrial, commercial, mixed-use, etc.)
- `codes`: Comma-separated list of building codes to apply
- `units`: metric or imperial (default: metric)
- `template`: Template project to copy from

**AI Processing:**
1. Prompts for missing critical info
2. Auto-selects applicable codes based on location
3. Sets up project folder structure
4. Creates default levels, views, schedules
5. Loads regional material/cost databases

**Output:**
```
✓ Project created: Kampala Office Tower
✓ Location: Kampala, Uganda (Lat: 0.3476°, Long: 32.5825°)
✓ Building type: Office
✓ Codes loaded: IBC 2024, NEC 2023, Uganda Building Code, KCCA Bylaws
✓ Climate zone: Tropical (ASHRAE 0A)
✓ Currency: UGX (1 USD = 3,700 UGX)
✓ Material database: Uganda prices loaded
✓ Ready to design!
```

---

#### `set-levels`
Define building levels/floors.

**Syntax:**
```
set-levels count=N height=H [basement=N] [mezzanine=list] [names=list]
```

**Examples:**
```
set-levels count=10 height=3.5m
set-levels count=5 height=3.8m basement=2 
set-levels count=12 height=3.5m mezzanine=3,7 names="Ground,Typical x10,Roof"
```

**AI Processing:**
1. Creates levels in Revit
2. Names levels intelligently (Ground, L01, L02, etc.)
3. Sets up structural grids if requested
4. Creates default floor plan views

---

#### `analyze-site`
Analyze site conditions and constraints.

**Syntax:**
```
analyze-site boundary=<sketch/import> [orientation=degrees] [setbacks=distances]
```

**Examples:**
```
analyze-site boundary=sketch
analyze-site boundary=import path="site_plan.dwg" orientation=15
analyze-site boundary=sketch setbacks="front=10m,side=5m,rear=8m"
```

**AI Processing:**
1. Imports or allows sketching site boundary
2. Analyzes solar orientation
3. Calculates buildable area with setbacks
4. Identifies optimal building placement
5. Suggests building orientation for passive design
6. Checks local zoning compliance

**Output:**
```
✓ Site analyzed
  Total area: 2,450 m²
  Buildable area: 1,850 m² (after setbacks)
  Optimal orientation: 15° clockwise from true north
  Solar analysis: East-West axis recommended for offices
  Max building height: 45m (KCCA limit for this zone)
  Parking required: 1 space per 40 m² = 46 spaces minimum
```

---

### **2. ARCHITECTURAL DESIGN**

#### `generate-massing`
Create conceptual building massing.

**Syntax:**
```
generate-massing [floors=N] [area=A] [efficiency=pct] [shape=type] [courtyard=yes/no]
```

**Examples:**
```
generate-massing floors=8 area=2000 efficiency=85
generate-massing floors=5 shape=L-shape courtyard=yes
generate-massing floors=12 area=1800 efficiency=82 shape=rectangular
```

**AI Processing:**
1. Calculates optimal floor plate size
2. Tests multiple configurations
3. Evaluates core-to-perimeter ratios
4. Checks code compliance (egress distances, etc.)
5. Creates 3D massing model
6. Calculates gross vs net areas

**Output:**
```
✓ Massing generated
  Configuration: Rectangular with central core
  Floor plate: 2,000 m² gross, 1,700 m² net (85% efficiency)
  Core size: 300 m² (15% of floor)
  Perimeter: 180m
  Core-to-perimeter distance: Max 15m ✓ (within 18m limit)
  Egress analysis: 2 stairs required, max travel = 45m ✓
  Total GFA: 16,000 m²
```

---

#### `design-floors`
Design detailed floor layouts.

**Syntax:**
```
design-floors [type=office/residential/mixed] [layout=open/cellular] [modules=list]
```

**Examples:**
```
design-floors type=office layout=open
design-floors type=office layout=mixed modules="open workspace 60%, private offices 25%, meeting rooms 15%"
design-floors type=residential units=studio:10,1bed:20,2bed:15,3bed:5
```

**AI Processing:**
1. Analyzes space program requirements
2. Generates optimal layouts based on type
3. Places columns on structural grid
4. Designs circulation paths
5. Optimizes for daylighting and views
6. Ensures code compliance (egress, accessibility)

**For Offices:**
- Workspace planning (open/closed ratios)
- Meeting room placement
- Collaboration zones
- Support spaces (pantry, restrooms, server room)

**For Residential:**
- Unit mix optimization
- Unit layouts per bedroom count
- Corridor efficiency
- Amenity spaces

---

#### `import-plan-image`
Convert scanned floor plan or hand sketch to BIM model.

**Syntax:**
```
import-plan-image path="file.pdf/jpg/png" [level=name] [scale=ratio] [enhance=yes/no]
```

**Examples:**
```
import-plan-image path="floor_plan.pdf" level="Ground Floor"
import-plan-image path="sketch.jpg" scale=1:100 enhance=yes
import-plan-image path="existing_dwg.pdf" level="L01" trace-mode=auto
```

**AI Processing:**
1. Loads image file
2. Detects scale automatically (or uses provided)
3. Image preprocessing (enhancement, noise removal)
4. AI detection:
   - Walls (ML-based line detection)
   - Doors (symbol recognition)
   - Windows (symbol recognition)
   - Rooms (space boundary detection)
   - Text labels (OCR)
   - Symbols (electrical, plumbing fixtures)
5. Creates Revit elements
6. Presents for user verification/adjustment

**Output:**
```
✓ Image imported and analyzed
  Detected: 45 walls, 12 doors, 18 windows, 8 rooms
  Scale: 1:100 (detected from scale bar)
  
  AI Confidence:
  ✓ Walls: 94% (42/45 high confidence)
  ✓ Doors: 91% (11/12 high confidence)
  ⚠ Windows: 78% (14/18 high confidence) - Please review
  ✓ Rooms: 89%
  
  Preview mode: Elements created in draft layer
  Use 'confirm-import' to finalize or 'adjust-import' to make changes
```

---

#### `design-facade`
Design building envelope/facade.

**Syntax:**
```
design-facade [glazing=percentage] [pattern=type] [shading=yes/no] [materials=list]
```

**Examples:**
```
design-facade glazing=40% shading=yes
design-facade glazing=60% pattern=alternating materials="brick,glass,aluminum"
design-facade glazing=35% shading=horizontal-louvers spacing=600mm depth=300mm
```

**AI Processing:**
1. Analyzes solar orientation per facade
2. Optimizes glazing ratios for daylighting and energy
3. Designs shading devices based on sun angles
4. Ensures code compliance (egress windows, etc.)
5. Calculates energy performance
6. Generates curtain wall/window families

---

#### `auto-place-doors`
Automatically place doors throughout building.

**Syntax:**
```
auto-place-doors [type=swing/slide] [fire-rating=auto] [accessibility=yes/no]
```

**Examples:**
```
auto-place-doors
auto-place-doors type=swing fire-rating=auto accessibility=yes
auto-place-doors entrance=double-3m office=single-900mm fire-exit=1200mm
```

**AI Processing:**
1. Analyzes circulation requirements
2. Identifies required door locations:
   - Room entries
   - Fire exits
   - Accessibility requirements
3. Selects appropriate door types
4. Assigns fire ratings based on wall types
5. Ensures swing directions per code
6. Checks clearances and accessibility

---

#### `auto-place-windows`
Automatically place windows for optimal daylighting.

**Syntax:**
```
auto-place-windows [target-daylight=percentage] [views=priority] [wwr=ratio]
```

**Examples:**
```
auto-place-windows target-daylight=75%
auto-place-windows wwr=40% views=maximize
auto-place-windows target-daylight=80% spacing=1200mm sill-height=900mm
```

**AI Processing:**
1. Performs daylighting simulation
2. Calculates optimal window placement
3. Sizes windows for target daylight autonomy
4. Considers views and privacy
5. Ensures energy code compliance (WWR limits)
6. Places windows and creates schedules

---

### **3. STRUCTURAL DESIGN**

#### `calculate-loads`
Calculate structural loads per code.

**Syntax:**
```
calculate-loads [occupancy=type] [snow=load] [wind=speed] [seismic=zone]
```

**Examples:**
```
calculate-loads
calculate-loads occupancy=office wind=120mph
calculate-loads occupancy=residential snow=25psf seismic=zone3
```

**AI Processing:**
1. Identifies applicable load codes (IBC, ASCE 7, etc.)
2. Calculates dead loads from materials
3. Determines live loads from occupancy
4. Calculates wind loads (exposure, topography)
5. Calculates seismic loads if applicable
6. Generates load combinations per code

**Output:**
```
✓ Loads calculated per IBC 2024 / ASCE 7-22

Dead Loads:
  Concrete slab: 3.6 kPa (75 psf)
  Ceiling + MEP: 0.5 kPa (10 psf)
  Partitions: 1.0 kPa (20 psf)
  Total DL: 5.1 kPa (105 psf)

Live Loads:
  Office occupancy: 2.4 kPa (50 psf) per IBC Table 1607.1
  Corridor: 4.8 kPa (100 psf)
  Roof live: 0.96 kPa (20 psf)

Wind Loads:
  Basic wind speed: 195 km/h (120 mph)
  Exposure: B (urban)
  Importance factor: 1.0
  Design pressure: 1.2 kPa (25 psf) @ 45m height

Load Combinations (16 total):
  1.4D
  1.2D + 1.6L + 0.5(Lr or S)
  1.2D + 1.0W + L + 0.5(Lr or S)
  [etc...]
```

---

#### `design-structure`
Design complete structural system.

**Syntax:**
```
design-structure [system=type] [material=concrete/steel] [optimize=yes/no]
```

**Examples:**
```
design-structure system=frame material=concrete
design-structure system=flat-slab material=concrete optimize=yes
design-structure system=composite material=steel+concrete
```

**AI Processing:**
1. Analyzes building geometry and loads
2. Selects optimal structural system
3. Designs all structural elements:
   - Beams (sizes, reinforcement)
   - Columns (sizes, reinforcement)
   - Slabs (thickness, reinforcement)
   - Foundations (type, sizing)
   - Lateral system (shear walls/bracing)
4. Performs code checks (BS 8110, ACI 318, etc.)
5. Optimizes member sizes
6. Generates structural drawings

**Output:**
```
✓ Structural system designed

System: Reinforced concrete frame with flat slab
Code: BS 8110-1:1997

Beams: 89 total
  Typical: 300x600mm, 4Y25 top, 3Y20 bottom, Y10@200 stirrups
  Largest: 400x800mm (28m span)

Columns: 45 total
  Ground: 500x500mm, 8Y32 (2.8% steel)
  Typical: 400x400mm, 8Y25 (2.2% steel)
  
Slabs: 250mm thick
  Reinforcement: Y12@200 both ways top, Y10@250 bottom
  Drop panels: 400mm thick at columns

Foundations: Pad footings
  Typical: 2.5m x 2.5m x 0.8m deep
  Soil bearing: 150 kPa (design), 200 kPa (allowable) ✓

All elements pass code checks ✓
Total concrete: 2,450 m³
Total steel: 186 tonnes
```

---

### **4. MEP ELECTRICAL**

#### `calculate-electrical-load`
Calculate complete electrical load per NEC.

**Syntax:**
```
calculate-electrical-load [occupancy=type] [area=sqft/sqm] [voltage=V] [diversity=yes/no]
```

**Examples:**
```
calculate-electrical-load
calculate-electrical-load occupancy=office area=15000sqm voltage=415V
calculate-electrical-load occupancy=residential units=50 voltage=240V
```

**AI Processing:**
1. Applies NEC 2023 Article 220 rules
2. Calculates loads by category:
   - Lighting (Table 220.12)
   - Receptacles (220.14(I))
   - HVAC equipment (220.14(J))
   - Motors (220.50)
   - Appliances (220.53)
3. Applies demand factors (Tables 220.42, 220.44)
4. Calculates feeder/service sizes
5. Determines panel requirements

**Output:**
```
✓ Electrical load calculated per NEC 2023

Connected Load:
  Lighting: 52.5 kW (3.5 W/sqft × 15,000 sqft)
  Receptacles: 30.0 kW (2.0 W/sqft × 15,000 sqft)
  HVAC: 285 kW (from mechanical design)
  Motors: 45 kW
  Misc equipment: 38 kW
  Total connected: 450.5 kW

Demand Load (with diversity):
  Lighting: 52.5 kW (100% - continuous)
  Receptacles: 21.0 kW (70% diversity)
  HVAC: 285 kW (100% - largest load)
  Motors: 51.8 kW (125% largest + 100% others)
  Misc: 28.5 kW (75%)
  Total demand: 438.8 kW

Service Requirements:
  Calculated load: 438.8 kW
  Service size: 700 A @ 415V, 3-phase
  Main breaker: 800 A (next standard size)
  Service conductors: 2×(4×240mm² + 120mm² N + 120mm² E) in parallel
  
Panels required: 8 distribution boards (100A each)
```

---

#### `design-distribution`
Design electrical distribution system.

**Syntax:**
```
design-distribution [voltage=V] [phases=N] [routing=auto/manual]
```

**Examples:**
```
design-distribution voltage=415V phases=3
design-distribution voltage=415V phases=3 routing=auto via=ceiling-plenum
```

**AI Processing:**
1. Locates main electrical room
2. Positions distribution panels
3. Routes feeders and branch circuits
4. Sizes all conductors per NEC Tables
5. Calculates voltage drop
6. Selects protection devices
7. Creates single-line diagrams
8. Generates panel schedules

---

#### `design-lighting`
Design lighting system.

**Syntax:**
```
design-lighting [target-lux=level] [efficiency=standard/led] [controls=type]
```

**Examples:**
```
design-lighting target-lux=500 efficiency=led
design-lighting target-lux=300 controls=daylight-harvesting+occupancy
design-lighting target-lux=office:500,corridor:200,restroom:150
```

**AI Processing:**
1. Performs photometric calculations
2. Places luminaires for uniform illumination
3. Sizes circuits and panels
4. Designs lighting controls
5. Calculates energy consumption
6. Ensures code compliance (energy, egress lighting)

**Output:**
```
✓ Lighting designed per ASHRAE 90.1-2022

Office areas (1,500 m²):
  Target: 500 lux
  Fixtures: LED 40W, 4000lm each
  Layout: 3m × 3m spacing
  Quantity: 167 fixtures
  Achieved: 520 lux average ✓
  LPD: 7.5 W/m² (Limit: 10.5 W/m²) ✓

Corridor (250 m²):
  Target: 200 lux
  Fixtures: LED 20W, 2000lm each
  Quantity: 28 fixtures
  Achieved: 215 lux ✓

Controls:
  Daylight harvesting: Perimeter zones (20% savings)
  Occupancy sensors: All spaces
  Total energy: 14.2 kW
  Annual consumption: 35,500 kWh
  Energy cost: 13,300,000 UGX/year
```

---

### **5. MEP MECHANICAL**

#### `calculate-hvac-load`
Calculate heating and cooling loads per ASHRAE.

**Syntax:**
```
calculate-hvac-load [method=radiant-time/CLTD] [climate=auto/manual]
```

**Examples:**
```
calculate-hvac-load
calculate-hvac-load method=radiant-time-series climate=kampala
```

**AI Processing:**
1. Retrieves climate data for location
2. Calculates heat gains/losses:
   - Solar radiation through glazing
   - Conduction through walls/roof
   - Ventilation air
   - Internal gains (people, lights, equipment)
   - Infiltration
3. Applies ASHRAE methods (RTS, CLTD, etc.)
4. Performs room-by-room calculations
5. Sizes equipment

**Output:**
```
✓ HVAC loads calculated per ASHRAE Fundamentals

Climate: Kampala, Uganda
  Cooling design temp: 28°C DB / 22°C WB (99.6% value)
  Heating design temp: 15°C (Not required - tropical)

Cooling Loads:
  Solar gains: 185 kW (40%)
  Conduction: 95 kW (21%)
  Ventilation: 125 kW (27%)
  Internal (people): 30 kW (6%)
  Internal (lights): 15 kW (3%)
  Internal (equipment): 15 kW (3%)
  Total cooling: 465 kW (132 tons)
  
Peak load time: 15:00 (west-facing glazing)
Safety factor: 1.15
Design capacity: 535 kW (152 tons)

Ventilation requirements (ASHRAE 62.1):
  Outdoor air: 7,500 CFM (3,540 L/s)
```

---

#### `design-hvac`
Design complete HVAC system.

**Syntax:**
```
design-hvac [system=type] [fuel=electric/gas] [efficiency=target]
```

**Examples:**
```
design-hvac system=vrf
design-hvac system=chilled-water efficiency=high
design-hvac system=split-dx zones=perimeter+core
```

**AI Processing:**
1. Selects optimal system type
2. Sizes equipment (chillers, AHUs, FCUs, etc.)
3. Designs ductwork/piping
4. Calculates pressure drops
5. Sizes pumps/fans
6. Routes distribution
7. Ensures code compliance

**Output:**
```
✓ HVAC system designed

System: VRF (Variable Refrigerant Flow)
Manufacturer: Daikin VRV-X series

Outdoor Units: 6 total
  ODU-1: 28 tons (100 kW) - Zones 1-4
  ODU-2: 28 tons (100 kW) - Zones 5-8
  [etc...]
  
Indoor Units: 95 total
  Ceiling cassette: 62 units (standard offices)
  Ducted: 18 units (large spaces)
  Wall-mounted: 15 units (small rooms)

Refrigerant piping:
  Main lines: DN65 (2.5")
  Branch lines: DN15-32
  Total length: 1,850m

Performance:
  Total capacity: 535 kW cooling
  COP: 4.5 (seasonal average)
  Annual energy: 148,000 kWh
  Energy cost: 55,500,000 UGX/year
  Compared to split DX: 35% savings ✓
```

---

#### `design-ventilation`
Design ventilation system per ASHRAE 62.1.

**Syntax:**
```
design-ventilation [method=VRP/IAQ] [mode=mechanical/natural/mixed]
```

**Examples:**
```
design-ventilation method=VRP
design-ventilation mode=mixed natural-zones=perimeter mechanical-zones=core
```

---

### **6. MEP PLUMBING**

#### `design-plumbing`
Design water supply and distribution.

**Syntax:**
```
design-plumbing [supply=municipal/well/tank] [pressure=psi/kPa] [hot-water=yes/no]
```

**Examples:**
```
design-plumbing supply=municipal pressure=350kPa
design-plumbing supply=tank hot-water=solar+backup
```

**AI Processing:**
1. Counts fixtures (IPC Appendix E)
2. Calculates water demand
3. Sizes supply piping (friction loss method)
4. Designs pressure system (pumps if needed)
5. Sizes hot water heaters
6. Routes piping
7. Ensures code compliance

**Output:**
```
✓ Plumbing designed per IPC 2024

Water Supply:
  Source: Municipal (350 kPa available)
  Daily demand: 18,000 L (300 people × 60 L/person/day)
  Peak demand: 1.8 L/s (110 fixture units, IPC Table E103.3(2))
  
Main supply: DN80 (3") from street
Risers: DN50 (2") - 4 risers total
Branch piping: DN15-40 sized per fixture loads

Fixtures: 85 total
  WC: 25 (flush valve, 6 LPF)
  Urinals: 10 (1.9 LPF)
  Lavatories: 30 (aerator, 1.9 LPM)
  Sinks: 12
  Drinking fountains: 8

Hot Water:
  System: Solar thermal + electric backup
  Solar collectors: 60 m² (flat plate)
  Storage tank: 3,000 L
  Backup heater: 45 kW electric
  Distribution: Recirculation with pump
  Insulation: 50mm on all hot pipes
  
Water efficiency:
  Total consumption: 18,000 L/day
  vs Baseline: 28,000 L/day
  Savings: 36% ✓ (WaterSense compliant)
```

---

#### `design-drainage`
Design drainage system.

**Syntax:**
```
design-drainage [method=gravity/pump] [stacks=auto] [venting=conventional/AAV]
```

**Examples:**
```
design-drainage method=gravity venting=conventional
design-drainage method=pump basement-level=-3m
```

**AI Processing:**
1. Calculates drainage loads (fixture units)
2. Sizes drain piping (IPC Tables)
3. Designs soil/waste stacks
4. Designs vent system
5. Calculates slopes
6. Routes piping avoiding conflicts

---

#### `design-fire-protection`
Design fire sprinkler system.

**Syntax:**
```
design-fire-protection [hazard=light/ordinary/extra] [type=wet/dry] [coverage=full/partial]
```

**Examples:**
```
design-fire-protection hazard=light type=wet
design-fire-protection hazard=ordinary coverage=full k-factor=5.6
```

**AI Processing:**
1. Determines occupancy hazard classification
2. Calculates design density (NFPA 13)
3. Places sprinkler heads
4. Sizes piping (hydraulic calculations)
5. Sizes fire pump
6. Designs water supply
7. Creates hydraulic calculation sheets

---

### **7. COORDINATION & CLASH DETECTION**

#### `coordinate-models`
Federate and coordinate all discipline models.

**Syntax:**
```
coordinate-models [disciplines=list] [tolerance=mm] [priority=rules]
```

**Examples:**
```
coordinate-models
coordinate-models disciplines=arch,struct,mep tolerance=50mm
coordinate-models disciplines=all priority="struct>arch>mep"
```

**AI Processing:**
1. Federates all models (Arch, Struct, MEP)
2. Runs comprehensive clash detection
3. Categorizes clashes by severity
4. Auto-resolves simple clashes
5. Reports unresolved conflicts

---

#### `auto-resolve-clashes`
Automatically resolve detected clashes.

**Syntax:**
```
auto-resolve-clashes [types=list] [strategy=move/resize/reroute]
```

**Examples:**
```
auto-resolve-clashes types=duct-beam strategy=move-duct
auto-resolve-clashes types=pipe-struct strategy=reroute-pipe
```

**AI Processing:**
1. Analyzes each clash
2. Determines optimal resolution:
   - MEP vs Structure: Move/reroute MEP
   - MEP vs MEP: Prioritize by size/system
   - MEP vs Arch: Coordinate with openings
3. Implements fixes
4. Re-runs clash detection
5. Reports results

**Output:**
```
✓ Clash detection complete

Total clashes found: 1,247
  Hard clashes: 89
  Soft clashes: 1,158

By discipline:
  HVAC ducts vs Structure: 45 (23 auto-resolved ✓)
  Plumbing vs Structure: 18 (15 auto-resolved ✓)
  Electrical vs HVAC: 12 (10 auto-resolved ✓)
  Architecture vs Structure: 14 (requires review ⚠)

Auto-resolution summary:
  ✓ Resolved: 48 clashes (54%)
  ⚠ Requires review: 41 clashes (46%)

Actions taken:
  - Moved HVAC ducts: 23 instances
  - Re-routed plumbing: 15 instances
  - Resized ducts: 10 instances

Remaining clashes exported to BCF file for coordination meeting.
```

---

### **8. DOCUMENTATION & DELIVERABLES**

#### `generate-drawings`
Automatically generate construction drawings.

**Syntax:**
```
generate-drawings [set=type] [scale=auto/custom] [sheets=template]
```

**Examples:**
```
generate-drawings set=architectural
generate-drawings set=all scale=1:100
generate-drawings set=structural sheets=ISO-A1
```

**AI Processing:**
1. Creates all required views:
   - Floor plans
   - RCPs
   - Elevations
   - Sections
   - Details
2. Places views on sheets
3. Adds dimensions automatically
4. Adds annotations
5. Generates legends/schedules
6. Numbers sheets
7. Adds title blocks

**Output:**
```
✓ Drawing set generated

Architectural Drawings: 45 sheets
  A001-A005: Cover, index, notes, specifications
  A100-A115: Floor plans (1:100)
  A200-A210: RCPs (1:100)
  A300-A308: Elevations (1:100)
  A400-A415: Sections (1:50)
  A500-A520: Details (1:20, 1:10, 1:5)
  A600-A610: Schedules
  A700-A705: 3D views

All drawings:
  ✓ Fully dimensioned
  ✓ Annotated with notes
  ✓ Referenced to details
  ✓ Coordinated across sheets
  ✓ ISO 19650 compliant
  ✓ Ready for printing
  
Time to create manually: ~80 hours
Time with StingBIM: 10 minutes
Savings: 99% ✓
```

---

#### `generate-schedules`
Create all schedules automatically.

**Syntax:**
```
generate-schedules [type=all/specific] [export-excel=yes/no] [formulas=preserve]
```

**Examples:**
```
generate-schedules type=all export-excel=yes
generate-schedules type=door,window,equipment
generate-schedules type=all export-excel=yes formulas=preserve
```

**AI Processing:**
1. Creates schedules for all categories:
   - Doors, windows, rooms
   - Structural framing
   - MEP equipment
   - Materials
   - Areas
2. Adds calculated fields
3. Applies formatting
4. Exports to Excel if requested
5. Sets up bidirectional sync

---

#### `generate-specifications`
Generate project specifications.

**Syntax:**
```
generate-specifications [format=Masterformat/NBS] [sections=list]
```

**Examples:**
```
generate-specifications format=Masterformat
generate-specifications sections=03,05,09 format=Masterformat
```

**AI Processing:**
1. Extracts materials from model
2. Identifies products/manufacturers
3. Generates spec sections
4. Includes performance criteria
5. Adds quality control requirements
6. Formats per standard (Masterformat/NBS)

---

### **9. COST ESTIMATION**

#### `calculate-cost`
Estimate project cost.

**Syntax:**
```
calculate-cost [region=location] [currency=UGX/USD] [detail=high/medium/low]
```

**Examples:**
```
calculate-cost region=kampala currency=UGX
calculate-cost region=uganda detail=high currency=UGX
```

**AI Processing:**
1. Performs quantity takeoff from model
2. Retrieves unit prices from database
3. Calculates material costs
4. Estimates labor costs
5. Adds equipment/overhead/profit
6. Generates detailed cost estimate

**Output:**
```
✓ Cost estimate (Uganda prices, January 2026)

SUBSTRUCTURE: 285,000,000 UGX (8.5%)
  Excavation: 35,000,000
  Foundations: 180,000,000
  Ground floor slab: 70,000,000

SUPERSTRUCTURE: 1,150,000,000 UGX (34.2%)
  Frame (concrete): 780,000,000
  Upper floors: 250,000,000
  Roof: 120,000,000

ARCHITECTURAL: 890,000,000 UGX (26.5%)
  External walls: 280,000,000
  Windows & doors: 185,000,000
  Internal walls: 165,000,000
  Finishes: 260,000,000

MEP SYSTEMS: 685,000,000 UGX (20.4%)
  Electrical: 245,000,000
  HVAC: 285,000,000
  Plumbing: 105,000,000
  Fire protection: 50,000,000

EXTERNAL WORKS: 140,000,000 UGX (4.2%)

PRELIMINARIES & OH&P: 210,000,000 UGX (6.2%)

═══════════════════════════════════
TOTAL PROJECT COST: 3,360,000,000 UGX
                    ($908,108 USD)
═══════════════════════════════════

Cost per m² GFA: 210,000 UGX/m² ($57/m²)
Cost per m² NFA: 247,000 UGX/m² ($67/m²)

Contingency (10%): 336,000,000 UGX
TOTAL WITH CONTINGENCY: 3,696,000,000 UGX
```

---

#### `optimize-cost`
Optimize design for cost reduction.

**Syntax:**
```
optimize-cost [target=percentage] [maintain=performance/aesthetics/both]
```

**Examples:**
```
optimize-cost target=15%
optimize-cost target=20% maintain=performance
```

**AI Processing:**
1. Analyzes current design costs
2. Identifies optimization opportunities:
   - Alternative materials
   - Structural optimization
   - MEP system alternatives
   - Standardization
3. Simulates alternatives
4. Presents cost-benefit analysis
5. Implements approved changes

---

### **10. CONSTRUCTION PLANNING**

#### `create-construction-sequence`
Generate 4D construction schedule.

**Syntax:**
```
create-construction-sequence [duration=months] [method=traditional/fast-track]
```

**Examples:**
```
create-construction-sequence duration=18
create-construction-sequence duration=24 method=fast-track
```

---

#### `link-schedule-to-model`
Link construction schedule to BIM model.

**Syntax:**
```
link-schedule-to-model path="schedule.mpp/primavera"
```

---

### **11. FACILITY MANAGEMENT**

#### `prepare-fm-handover`
Prepare facility management handover package.

**Syntax:**
```
prepare-fm-handover [format=COBie/custom] [include=list]
```

**Examples:**
```
prepare-fm-handover format=COBie
prepare-fm-handover include=assets,manuals,warranties,schedules
```

---

#### `setup-fm-system`
Configure facility management system.

**Syntax:**
```
setup-fm-system [platform=custom/CAFM] [modules=list]
```

---

**Continue to advanced commands and workflows...**
