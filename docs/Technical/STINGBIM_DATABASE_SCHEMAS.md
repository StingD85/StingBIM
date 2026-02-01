# STINGBIM - DATABASE SCHEMAS & EXCEL TEMPLATES
## Enhanced Data Structures for Maximum Flexibility

---

## 📊 ENHANCED EXCEL FILE STRUCTURES

### **1. GLOBAL_STANDARDS.xlsx**

**Sheet 1: Code_Registry**
```
Column A: Code_ID (Primary Key)
Column B: Code_Name
Column C: Code_Version
Column D: Jurisdiction
Column E: Effective_Date
Column F: Category (Electrical/Mechanical/Plumbing/Structural/Architectural)
Column G: Status (Active/Deprecated/Superseded)
Column H: Superseded_By
Column I: File_Location (for embedded rules)
Column J: Total_Rules
Column K: Last_Updated
Column L: Update_Frequency

Example Rows:
NEC-2023 | National Electrical Code | 2023 | USA | 2023-01-01 | Electrical | Active | | Embedded | 15000 | 2023-01-01 | 3-years
ASHRAE-62.1-2022 | Ventilation Standard | 2022 | International | 2022-01-01 | Mechanical | Active | | Embedded | 8000 | 2022-01-01 | Annual
IBC-2024 | International Building Code | 2024 | International | 2024-01-01 | Building | Active | IBC-2021 | Embedded | 12000 | 2024-01-01 | 3-years
```

**Sheet 2: Rule_Definitions**
```
Column A: Rule_ID (Primary Key)
Column B: Code_ID (Foreign Key)
Column C: Section_Reference
Column D: Rule_Text
Column E: Condition_Logic
Column F: Action_Logic
Column G: Exception_Conditions
Column H: Priority
Column I: Category
Column J: Searchable_Keywords
Column K: Example
Column L: Diagram_Reference
Column M: Calculation_Formula
Column N: Unit_System

Example Rows:
NEC-220.14A-001 | NEC-2023 | Table 220.12 | General lighting load dwelling | OccupancyType==Dwelling AND Area>0 | LightingLoad_VA = Area_sqft * 3.0 | None | 1 | Load Calculation | lighting, dwelling, load | 2000 sqft house = 6000 VA | | Area_sqft * 3.0 | Imperial
ASHRAE-62.1-001 | ASHRAE-62.1-2022 | Table 6.2.2.1 | Office ventilation | SpaceType==Office | OA_CFM = (5*Occupancy)+(0.06*Area_sqft) | None | 1 | Ventilation | office, outdoor air, ventilation | 20 person 1000sf = 100+60=160 CFM | | (Ra*Pz)+(Rp*Az) | Imperial
```

**Sheet 3: Compliance_Matrix**
```
Column A: Project_Type
Column B: Required_Codes (comma-separated Code_IDs)
Column C: Optional_Codes
Column D: Jurisdiction_Specific
Column E: Special_Requirements
Column F: Typical_Variances
Column G: Approval_Authorities

Example Rows:
Office Building - Uganda | IBC-2024,NEC-2023,ASHRAE-62.1,Uganda-BC | LEED-v4.1,WELL-v2 | KCCA,NEMA,NWSC,UMEME | Accessibility,Energy,Fire | None | KCCA Building Control
Residential - USA | IBC-2024,NEC-2023,IRC-2024 | Energy Star,LEED Homes | Local AHJ | Energy code compliance | State amendments | Local Building Department
```

---

### **2. FM_PARAMETERS_ENHANCED.xlsx**

**Sheet 1: Asset_Parameters**
```
Column A: Parameter_Name
Column B: Parameter_GUID
Column C: Data_Type
Column D: Group
Column E: Binding_Type
Column F: Asset_Categories (which equipment types)
Column G: COBie_Field_Mapping
Column H: Maintenance_Relevant (Yes/No)
Column I: Energy_Tracking (Yes/No)
Column J: Required_For_Handover (Yes/No)
Column K: Default_Value
Column L: Validation_Rule
Column M: Unit
Column N: Description

Example Rows:
ASS_INST_DATE_TXT | 0d021db7-c85a-5df7-82e3-6a2fd48eb619 | TEXT | ASS_MNG | Type | All Equipment | Type.InstallationDate | Yes | No | Yes | | Date format: YYYY-MM-DD | | Installation date per ISO 19650-3:2020
ASS_WARRANTY_EXP_DATE_TXT | bb4c8fcd-1997-5f0c-9670-f5c245517a8f | TEXT | ASS_MNG | Type | All Equipment | Type.WarrantyExpiration | Yes | No | Yes | | Date format: YYYY-MM-DD | | Warranty expiration date
ASS_EXPECTED_LIFE_YEARS_YRS | 3bc7b880-b296-532f-9faf-8c41d69df5c3 | NUMBER | ASS_MNG | Type | All Equipment | Type.ExpectedLife | Yes | No | Yes | 10 | >0 | years | Expected lifespan in years
ASS_ENERGY_RATING_TXT | NEW-GUID-001 | TEXT | ASS_MNG | Type | HVAC,Electrical | Type.EnergyRating | No | Yes | No | | Energy Star,A+,etc | | Energy efficiency rating
```

**Sheet 2: Maintenance_Schedules**
```
Column A: Equipment_Category
Column B: Manufacturer
Column C: Model_Type
Column D: PM_Task
Column E: Frequency
Column F: Frequency_Unit (Days/Weeks/Months/Years/Hours)
Column G: Task_Duration_Minutes
Column H: Required_Skills
Column I: Required_Tools
Column J: Required_Parts
Column K: Task_Description
Column L: Safety_Requirements
Column M: Estimated_Cost
Column N: Criticality (Low/Medium/High/Critical)

Example Rows:
Chiller | Carrier | 30XA | Filter Replacement | 3 | Months | 60 | HVAC Tech Level 2 | Filter wrench, Vacuum | Filters (24x24) | Replace air filters, inspect coils | Lockout/Tagout, PPE | 150 | High
AHU | Trane | TAM | Belt Inspection | 1 | Months | 30 | HVAC Tech Level 1 | Tension gauge | None | Check belt tension and wear | None | 50 | Medium
Fire Pump | Grundfos | CR95 | Weekly Test Run | 1 | Weeks | 45 | Facility Tech | None | None | Run pump for 30 min, check pressure | Safety glasses | 25 | Critical
```

**Sheet 3: Energy_Metrics**
```
Column A: Metric_Name
Column B: Parameter_GUID
Column C: Data_Type
Column D: Calculation_Formula
Column E: Input_Parameters
Column F: Benchmark_Value
Column G: Target_Value
Column H: Alert_Threshold
Column I: Unit
Column J: Reporting_Frequency
Column K: Dashboard_Display

Example Rows:
Energy Use Intensity | NEW-GUID-002 | NUMBER | TotalEnergyUse_kWh / BuildingArea_sqm | TotalEnergyUse_kWh, BuildingArea_sqm | 200 | 150 | 250 | kWh/m²/year | Monthly | Yes
Carbon Emissions | NEW-GUID-003 | NUMBER | TotalEnergy_kWh * GridCarbonIntensity | TotalEnergy_kWh, GridCarbonIntensity | | | | kg CO2e | Monthly | Yes
Water Use Intensity | NEW-GUID-004 | NUMBER | TotalWaterUse_m3 / BuildingArea_sqm | TotalWaterUse_m3, BuildingArea_sqm | 0.8 | 0.6 | 1.2 | m³/m²/year | Monthly | Yes
```

---

### **3. COST_DATABASE_UGANDA_DETAILED.xlsx**

**Sheet 1: Material_Costs**
```
Column A: Material_ID
Column B: Material_Category
Column C: Material_Name
Column D: Specification
Column E: Unit
Column F: Unit_Price_UGX
Column G: Unit_Price_USD
Column H: Supplier_1
Column I: Supplier_2
Column J: Supplier_3
Column K: Lead_Time_Days
Column L: Minimum_Order
Column M: Transport_Cost_UGX_Per_Unit
Column N: Wastage_Factor
Column O: Price_Date
Column P: Price_Trend (Up/Down/Stable)
Column Q: Alternative_Materials
Column R: Quality_Grade

Example Rows:
MAT-001 | Concrete | Ready Mix Concrete C25/30 | 25MPa, 20mm aggregate | m³ | 380000 | 103 | Simba Cement | Hima Cement | Tororo Cement | 2 | 2 m³ | 15000 | 1.05 | 2026-01-31 | Up | C20/25 (cheaper) | Standard
MAT-002 | Steel | Reinforcement Y12 | High tensile steel | kg | 4200 | 1.14 | Roofings Group | Steel & Tube | Entebbe Steel | 3 | 100 kg | 200 | 1.08 | 2026-01-31 | Stable | Y10 (smaller) | Grade 460
MAT-003 | Block | Cement Block 6" | 150mm solid | unit | 1800 | 0.49 | Blockmaster | Uganda Blocks | Local supplier | 1 | 500 | 100 | 1.03 | 2026-01-31 | Stable | 4" block (thinner) | Standard
MAT-004 | Roofing | Gauge 28 Iron Sheets | 3m length, corrugated | sheet | 35000 | 9.46 | Roofings | Steel & Tube | Hardware stores | 1 | 10 | 500 | 1.15 | 2026-01-31 | Up | Gauge 30 (thinner) | Premium
```

**Sheet 2: Labor_Rates**
```
Column A: Trade
Column B: Skill_Level
Column C: Rate_UGX_Per_Hour
Column D: Rate_UGX_Per_Day
Column E: Productivity_Factor
Column F: Typical_Crew_Size
Column G: Supervision_Required
Column H: Equipment_Required
Column I: Region
Column J: Urban_Premium_Pct
Column K: Availability (High/Medium/Low)

Example Rows:
Mason | Skilled | 8000 | 64000 | 1.0 | 1 mason + 2 laborers | Foreman (1:5 ratio) | Trowel, level, string line | Kampala | 0 | High
Carpenter | Skilled | 9000 | 72000 | 1.0 | 1 carpenter + 1 helper | Foreman (1:4 ratio) | Hand tools, saw | Kampala | 0 | High
Electrician | Licensed | 12000 | 96000 | 1.0 | 1 electrician + 1 helper | Electrical supervisor | Multimeter, tools | Kampala | 0 | Medium
Plumber | Licensed | 11000 | 88000 | 1.0 | 1 plumber + 1 helper | None | Pipe wrench, threading | Kampala | 0 | Medium
General Laborer | Unskilled | 4000 | 32000 | 0.8 | Multiple | None | Basic tools | Kampala | 0 | High
```

**Sheet 3: Equipment_Hire**
```
Column A: Equipment_Type
Column B: Model/Specification
Column C: Daily_Rate_UGX
Column D: Weekly_Rate_UGX
Column E: Monthly_Rate_UGX
Column F: Fuel_Included
Column G: Operator_Included
Column H: Transport_Cost_UGX
Column I: Supplier
Column J: Availability
Column K: Lead_Time_Days

Example Rows:
Concrete Mixer | 350L diesel | 80000 | 450000 | 1500000 | No | No | 50000 | Equipment Hire Ltd | High | 1
Excavator | 20-ton tracked | 600000 | 3500000 | 12000000 | No | Yes | 200000 | CAT Rental | Medium | 3
Tower Crane | 50m height | 2000000 | 10000000 | 35000000 | No | Yes | 500000 | Crane Services UG | Low | 14
Concrete Pump | Truck-mounted | 1200000 | N/A | N/A | Yes | Yes | 0 | Simba Cement | Medium | 2
Scaffolding | Steel frame per m² | 3000 | 15000 | 45000 | N/A | No | 100000 (setup) | Scaff-Pro | High | 1
```

**Sheet 4: Price_Escalation**
```
Column A: Year
Column B: Month
Column C: Construction_Index
Column D: Material_Index
Column E: Labor_Index
Column F: Equipment_Index
Column G: UGX_USD_Rate
Column H: Inflation_Rate_Annual
Column I: Notes

Example Rows:
2026 | January | 156.3 | 158.2 | 154.1 | 156.8 | 3700 | 6.5% | Post-election stability
2026 | February | 157.1 | 159.5 | 154.3 | 157.2 | 3710 | 6.5% | 
2026 | March | 158.0 | 160.8 | 154.6 | 157.6 | 3720 | 6.4% | Steel prices rising
```

---

### **4. EQUIPMENT_LIBRARY_10000.xlsx**

**Sheet 1: HVAC_Equipment**
```
Column A: Equipment_ID
Column B: Category
Column C: Type
Column D: Manufacturer
Column E: Model_Number
Column F: Capacity
Column G: Capacity_Unit
Column H: Efficiency_Rating
Column I: Power_kW
Column J: Voltage
Column K: Phases
Column L: Weight_kg
Column M: Dimensions_mm
Column N: Price_UGX
Column O: Price_USD
Column P: Lead_Time_Days
Column Q: Warranty_Years
Column R: Datasheet_Link
Column S: BIM_Family_Link
Column T: Operating_Temperature_Range
Column U: Sound_Level_dB
Column V: Refrigerant_Type
Column W: Application

Example Rows:
HVAC-001 | Chiller | Water-Cooled | Carrier | 30XA-080 | 80 | Tons | 6.2 EER | 110 | 415V | 3 | 2800 | 2500x1200x1800 | 185000000 | 50000 | 90 | 2 | carrier.com/30XA | Carrier_30XA.rfa | 15-45°C | 78 | R-134a | Commercial cooling
HVAC-002 | VRF Outdoor | Multi-Split | Daikin | VRV-X | 28 | Tons | 4.5 COP | 75 | 415V | 3 | 580 | 1700x850x1850 | 95000000 | 25675 | 60 | 3 | daikin.com/vrv | Daikin_VRV.rfa | -5-43°C | 65 | R-32 | Office buildings
HVAC-003 | AHU | Packaged | Trane | TAM-150 | 15000 | CFM | | 18 | 415V | 3 | 850 | 3000x1200x1400 | 28000000 | 7568 | 45 | 2 | trane.com/tam | Trane_AHU.rfa | 5-40°C | 72 | N/A | Commercial ventilation
```

**Sheet 2: Electrical_Equipment**
```
Column A: Equipment_ID
Column B: Category
Column C: Type
Column D: Manufacturer
Column E: Model_Number
Column F: Rating_A
Column G: Voltage
Column H: Phases
Column I: Fault_Level_kA
Column J: Ways/Poles
Column K: Frame_Size
Column L: Price_UGX
Column M: Price_USD
Column N: Lead_Time_Days
Column O: Standards_Compliance
Column P: Datasheet_Link
Column Q: BIM_Family_Link
Column R: IP_Rating
Column S: Arc_Flash_Rating

Example Rows:
ELEC-001 | Switchboard | Main Distribution | ABB | MNS | 1600 | 415V | 3 | 50 | Form 4 | 2000x800x600 | 45000000 | 12162 | 60 | IEC 61439 | abb.com/mns | ABB_MNS.rfa | IP43 | Arc-resistant
ELEC-002 | Transformer | Dry-Type | Schneider | Trihal | 1000 | 415/230V | 3 | | Cast resin | 1800x1200x1500 | 38000000 | 10270 | 75 | IEC 60076 | se.com/trihal | Schneider_Trihal.rfa | IP23 | 
ELEC-003 | Panel | Distribution Board | Hager | JK236A | 250 | 415V | 3 | 10 | 36-way | 800x600x200 | 3500000 | 946 | 14 | IEC 61439 | hager.com | Hager_DB.rfa | IP54 | 
```

**Sheet 3: Plumbing_Fixtures**
```
Column A: Equipment_ID
Column B: Category
Column C: Type
Column D: Manufacturer
Column E: Model_Number
Column F: Flow_Rate
Column G: Flow_Unit
Column H: Flush_Volume_L
Column I: Connection_Size
Column J: Material
Column K: Finish
Column L: Price_UGX
Column M: Price_USD
Column N: Lead_Time_Days
Column O: Water_Efficiency_Rating
Column P: Datasheet_Link
Column Q: BIM_Family_Link
Column R: ADA_Compliant

Example Rows:
PLUMB-001 | Toilet | Wall-Hung | Duravit | Starck 3 | | | 4.5/3 | DN100 | Ceramic | White | 1800000 | 486 | 30 | WaterSense | duravit.com | Duravit_WC.rfa | Yes
PLUMB-002 | Sink | Vanity | Kohler | Verticyl | 2.2 | GPM | | 1.25" | Vitreous China | White | 850000 | 230 | 21 | WaterSense | kohler.com | Kohler_Sink.rfa | Yes
PLUMB-003 | Faucet | Sensor | Sloan | ETF610 | 0.5 | GPM | | 0.5" | Chrome-plated brass | Chrome | 650000 | 176 | 14 | WaterSense | sloan.com | Sloan_Faucet.rfa | Yes
```

**Sheet 4: Fire_Protection**
```
Column A: Equipment_ID
Column B: Category
Column C: Type
Column D: Manufacturer
Column E: Model_Number
Column F: Coverage_sqft
Column G: K_Factor
Column H: Temperature_Rating
Column I: Response_Type
Column J: Finish
Column K: Price_UGX
Column L: Price_USD
Column M: Standards_Compliance
Column N: Datasheet_Link
Column O: BIM_Family_Link

Example Rows:
FIRE-001 | Sprinkler | Pendent | Viking | VK302 | 130 | 5.6 | 165°F | Quick | Chrome | 45000 | 12 | UL Listed, FM Approved | viking.com | Viking_Sprinkler.rfa
FIRE-002 | Fire Pump | Electric | Grundfos | CR95-2 | | | | | Red | 18500000 | 5000 | NFPA 20, UL Listed | grundfos.com | Grundfos_Pump.rfa
FIRE-003 | Fire Alarm Panel | Addressable | Siemens | FC2040 | | | | | Red | 12000000 | 3243 | UL 864, NFPA 72 | siemens.com | Siemens_Panel.rfa
```

---

### **5. FORMULA_LIBRARY_EXPANDED_200.xlsx**

**Sheet 1: Structural_Formulas**
```
Column A: Formula_ID
Column B: Discipline
Column C: Parameter_Name
Column D: Data_Type
Column E: Formula
Column F: Description
Column G: Input_Parameters
Column H: Output_Unit
Column I: Code_Reference
Column J: Validation_Range
Column K: Example_Calculation

Example Rows:
STR-001 | Structural | BEAM_MOMENT_KNM | NUMBER | (W_kN * L_m^2) / 8 | Simply supported beam max moment | W_kN (load), L_m (span) | kN·m | | M > 0 | 10kN load, 6m span = 45 kN·m
STR-002 | Structural | BEAM_DEFLECTION_MM | LENGTH | (5 * W_kN * L_m^4 * 1000000) / (384 * E_GPa * I_mm4) | Max deflection simply supported | W_kN, L_m, E_GPa, I_mm4 | mm | | δ < L/360 | Steel beam: 15mm
STR-003 | Structural | COLUMN_SLENDERNESS | NUMBER | (K * L_mm) / (r_mm) | Column slenderness ratio | K (effective length factor), L_mm, r_mm (radius of gyration) | | BS 5950 | λ < 180 | 4m column: λ = 85
STR-004 | Structural | CONCRETE_STEEL_AREA_MM2 | AREA | (M_kNm * 10^6) / (0.87 * fy_MPa * 0.9 * d_mm) | Required steel area for moment | M_kNm, fy_MPa, d_mm | mm² | BS 8110 | As,min < As < As,max | 150 kN·m: As = 1250 mm²
```

**Sheet 2: Energy_Formulas**
```
Column A: Formula_ID
Column B: Discipline
Column C: Parameter_Name
Column D: Data_Type
Column E: Formula
Column F: Description
Column G: Input_Parameters
Column H: Output_Unit
Column I: Code_Reference
Column J: Climate_Zone_Specific

Example Rows:
ENERGY-001 | Energy | BUILDING_ENERGY_INDEX | NUMBER | TotalEnergy_kWh / (Area_m2 * 365) | Annual energy use intensity | TotalEnergy_kWh, Area_m2 | kWh/m²/year | ASHRAE 90.1 | No
ENERGY-002 | Energy | ENVELOPE_UA_W_K | NUMBER | SUM(Area_m2 * U_value_W_m2K) | Total building envelope heat loss | Area_m2[], U_value_W_m2K[] | W/K | ASHRAE 90.1 | Yes
ENERGY-003 | Energy | SOLAR_HEAT_GAIN_W | NUMBER | Area_m2 * SHGC * SOLAR_IRRADIANCE_W_m2 | Solar heat gain through glazing | Area_m2, SHGC, SOLAR_IRRADIANCE | W | ASHRAE Fundamentals | Yes
ENERGY-004 | Energy | DAYLIGHTING_SAVINGS_PCT | NUMBER | (DA_pct / 100) * 0.3 * LIGHTING_FRACTION | Energy savings from daylighting | DA_pct (daylight autonomy), LIGHTING_FRACTION | % | LEED v4 | No
```

**Sheet 3: Hydraulic_Formulas**
```
Column A: Formula_ID
Column B: Discipline
Column C: Parameter_Name
Column D: Data_Type
Column E: Formula
Column F: Description
Column G: Input_Parameters
Column H: Output_Unit
Column I: Code_Reference

Example Rows:
HYD-001 | Plumbing | PIPE_VELOCITY_MPS | NUMBER | (Q_Lps / 1000) / (PI * (D_mm / 2000)^2) | Flow velocity in pipe | Q_Lps, D_mm | m/s | | 
HYD-002 | Plumbing | FRICTION_LOSS_KPA_M | NUMBER | (10.67 * Q_Lps^1.85 * C_hw^-1.85 * D_mm^-4.87) | Hazen-Williams friction loss | Q_Lps, C_hw, D_mm | kPa/m | IPC |
HYD-003 | Plumbing | PUMP_POWER_KW | ELECTRICAL_POWER | (Q_m3h * H_m * 9.81) / (3600 * EFF) | Required pump power | Q_m3h, H_m, EFF | kW | |
HYD-004 | Plumbing | DRAIN_CAPACITY_DFU | NUMBER | IF(SLOPE_pct=2, 21*D_in^2, 27*D_in^2) | Drainage fixture units capacity | SLOPE_pct, D_in | DFU | IPC Table 704.1 |
```

**Sheet 4: Cost_Formulas**
```
Column A: Formula_ID
Column B: Discipline
Column C: Parameter_Name
Column D: Data_Type
Column E: Formula
Column F: Description
Column G: Input_Parameters
Column H: Output_Unit

Example Rows:
COST-001 | Costing | TOTAL_PROJECT_COST | CURRENCY | SUM(Substructure + Superstructure + Arch + MEP + External) | Complete project cost | All cost components | UGX
COST-002 | Costing | COST_PER_SQM | CURRENCY | TOTAL_PROJECT_COST / GFA_m2 | Cost per square meter | TOTAL_PROJECT_COST, GFA_m2 | UGX/m²
COST-003 | Costing | COST_WITH_ESCALATION | CURRENCY | BASE_COST * (1 + ESCALATION_PCT/100)^YEARS | Future cost with inflation | BASE_COST, ESCALATION_PCT, YEARS | UGX
COST-004 | Costing | ROI_YEARS | NUMBER | INITIAL_INVESTMENT / ANNUAL_SAVINGS | Return on investment period | INITIAL_INVESTMENT, ANNUAL_SAVINGS | years
COST-005 | Costing | NPV | CURRENCY | SUM((CASH_FLOW_n / (1+DISCOUNT_RATE)^n)) - INITIAL_INVESTMENT | Net present value | CASH_FLOW[], DISCOUNT_RATE, INITIAL_INVESTMENT | UGX
```

---

### **6. WORKFLOW_TEMPLATES.xlsx**

**Sheet 1: Command_Sequences**
```
Column A: Workflow_Name
Column B: Building_Type
Column C: Project_Phase
Column D: Command_Sequence
Column E: Parameters_Required
Column F: Estimated_Time_Savings_Pct
Column G: Description
Column H: Prerequisites

Example Rows:
Quick Office Design | Office | Schematic Design | new-project → analyze-site → generate-massing → design-floors → design-facade → auto-place-doors → auto-place-windows → generate-drawings | site area, floors, target efficiency | 95% | Complete office building design from scratch | Site boundary defined
MEP Auto-Design | Any | MEP Design | calculate-electrical-load → design-distribution → design-lighting → calculate-hvac-load → design-hvac → design-ventilation → design-plumbing → design-drainage → design-fire-protection → coordinate-models | occupancy, area, usage type | 97% | Complete MEP design automation | Architectural model complete
FM Handover | Any | Handover | prepare-fm-handover → setup-fm-system → generate-om-manuals → export-cobie → create-asset-register → setup-maintenance-schedules → configure-energy-monitoring | All project data | 90% | Complete facility management setup | Construction complete
```

**Sheet 2: Best_Practices**
```
Column A: Practice_ID
Column B: Category
Column C: Title
Column D: Description
Column E: When_To_Apply
Column F: Benefits
Column G: Common_Mistakes
Column H: Example_Commands

Example Rows:
BP-001 | Modeling | Start with Levels | Always create all levels before modeling | Beginning of project | Ensures consistent floor heights, easier coordination | Creating levels as you go | new-project → set-levels count=12 height=3.5m
BP-002 | Coordination | Daily Clash Checks | Run clash detection daily during coordination | Coordination phase | Catches issues early, reduces rework | Only checking at milestones | coordinate-models → auto-resolve-clashes → review-remaining
BP-003 | Documentation | Use Schedules Early | Create schedules from the start | Design development | Easier to track quantities, spot errors | Creating schedules at end | generate-schedules all → excel-export=yes
```

---

## 🗄️ DATABASE SCHEMA FOR CODE STORAGE

### **SQL Schema for Standards Database**

```sql
-- Standards Registry
CREATE TABLE Code_Registry (
    Code_ID VARCHAR(50) PRIMARY KEY,
    Code_Name VARCHAR(200),
    Code_Version VARCHAR(50),
    Jurisdiction VARCHAR(100),
    Effective_Date DATE,
    Category VARCHAR(50),
    Status VARCHAR(20),
    Superseded_By VARCHAR(50),
    Total_Rules INT,
    Last_Updated DATE,
    FOREIGN KEY (Superseded_By) REFERENCES Code_Registry(Code_ID)
);

-- Rule Definitions (80,000+ rows)
CREATE TABLE Rule_Definitions (
    Rule_ID VARCHAR(100) PRIMARY KEY,
    Code_ID VARCHAR(50),
    Section_Reference VARCHAR(100),
    Rule_Text TEXT,
    Condition_Logic TEXT,  -- JSON or XML
    Action_Logic TEXT,     -- JSON or XML
    Exception_Conditions TEXT,
    Priority INT,
    Category VARCHAR(100),
    Searchable_Keywords TEXT,
    Example TEXT,
    Diagram_Reference VARCHAR(255),
    Calculation_Formula TEXT,
    Unit_System VARCHAR(20),
    FOREIGN KEY (Code_ID) REFERENCES Code_Registry(Code_ID)
);

-- Lookup Tables (embedded for offline use)
CREATE TABLE NEC_Conductor_Ampacities (
    AWG_Size VARCHAR(20),
    Material VARCHAR(20),
    Insulation_Type VARCHAR(20),
    Temperature_Rating INT,
    Ampacity_60C INT,
    Ampacity_75C INT,
    Ampacity_90C INT
);

CREATE TABLE ASHRAE_Ventilation_Rates (
    Space_Type VARCHAR(100),
    People_Component_CFM DECIMAL(5,2),
    Area_Component_CFM DECIMAL(5,2),
    Default_Occupancy DECIMAL(5,2),
    Air_Class VARCHAR(10)
);

CREATE TABLE IPC_Drainage_Capacities (
    Pipe_Diameter_IN DECIMAL(4,2),
    Slope_Percent DECIMAL(3,1),
    Capacity_DFU INT,
    Max_Units_Horizontal INT,
    Max_Units_Vertical INT
);

-- Material Database
CREATE TABLE Materials_Database (
    Material_ID VARCHAR(50) PRIMARY KEY,
    Material_Category VARCHAR(100),
    Material_Name VARCHAR(200),
    Specification TEXT,
    Unit VARCHAR(20),
    Unit_Price_UGX DECIMAL(12,2),
    Unit_Price_USD DECIMAL(10,2),
    Supplier_1 VARCHAR(100),
    Supplier_2 VARCHAR(100),
    Lead_Time_Days INT,
    Wastage_Factor DECIMAL(4,3),
    Price_Date DATE,
    Alternative_Materials TEXT,  -- JSON array
    Quality_Grade VARCHAR(50),
    Location VARCHAR(100)
);

-- Equipment Library (10,000+ products)
CREATE TABLE Equipment_Library (
    Equipment_ID VARCHAR(50) PRIMARY KEY,
    Category VARCHAR(50),
    Type VARCHAR(50),
    Manufacturer VARCHAR(100),
    Model_Number VARCHAR(100),
    Capacity DECIMAL(10,2),
    Capacity_Unit VARCHAR(20),
    Efficiency_Rating DECIMAL(5,2),
    Power_kW DECIMAL(8,2),
    Voltage INT,
    Phases INT,
    Price_UGX DECIMAL(15,2),
    Price_USD DECIMAL(10,2),
    Lead_Time_Days INT,
    Warranty_Years INT,
    Datasheet_Link VARCHAR(255),
    BIM_Family_Link VARCHAR(255),
    Standards_Compliance TEXT,  -- JSON array
    Specifications_JSON TEXT    -- Full specs as JSON
);
```

---

## 🔄 EXCEL SYNC MAPPING CONFIGURATION

```json
{
  "SyncMappings": [
    {
      "RevitSchedule": "Door Schedule",
      "ExcelWorkbook": "Doors_Export.xlsx",
      "Worksheet": "Sheet1",
      "MappingRules": [
        {
          "ExcelColumn": "A",
          "ExcelHeader": "Mark",
          "RevitParameter": "Mark",
          "Sync": "Bidirectional",
          "DataType": "Text",
          "Required": true
        },
        {
          "ExcelColumn": "B",
          "ExcelHeader": "Width",
          "RevitParameter": "Width",
          "Sync": "Bidirectional",
          "DataType": "Length",
          "Unit": "mm"
        },
        {
          "ExcelColumn": "C",
          "ExcelHeader": "Height",
          "RevitParameter": "Height",
          "Sync": "Bidirectional",
          "DataType": "Length",
          "Unit": "mm"
        },
        {
          "ExcelColumn": "D",
          "ExcelHeader": "Fire Rating",
          "RevitParameter": "Fire Rating",
          "Sync": "Bidirectional",
          "DataType": "Text",
          "ValidationList": ["30min", "60min", "90min", "120min"]
        },
        {
          "ExcelColumn": "E",
          "ExcelHeader": "Unit Cost (UGX)",
          "RevitParameter": "COST_UNIT_PRICE_UGX",
          "Sync": "ExcelToRevit",
          "DataType": "Currency",
          "CreateIfMissing": true
        },
        {
          "ExcelColumn": "F",
          "ExcelHeader": "Total Cost",
          "Formula": "=E{row}*1",
          "RevitParameter": "COST_TOTAL_UGX",
          "Sync": "ExcelToRevit",
          "DataType": "Currency",
          "CreateIfMissing": true
        }
      ],
      "ConflictResolution": "PromptUser",
      "AutoSync": true,
      "SyncInterval": 30
    }
  ]
}
```

---

**Continue to Part 2: Command Reference & API Documentation...**
