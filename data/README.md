# Offline AI Plugin - Comprehensive Data Files

## Overview
This package contains comprehensive, well-organized CSV files for building an offline AI plugin for architectural design and building information modeling. The data is structured to support natural language processing, design knowledge, element creation, and MEP (Mechanical, Electrical, Plumbing) systems.

## Directory Structure

```
data/
├── design_knowledge/      # Building design rules and spatial relationships
├── elements/             # Building element templates and specifications
├── families/             # Family catalogs and parameters
├── materials/            # Material specifications for building elements and MEP
└── training/             # NLP training data for intent recognition
```

## File Descriptions

### 1. Design Knowledge Base (`/design_knowledge/`)

#### **ROOM_DEFINITIONS.csv**
- **Purpose**: Defines 31+ room types with their spatial requirements
- **Key Fields**: RoomType, MinArea, MaxArea, MinHeight, RequiresWindow, RequiresVent, RequiresPlumbing, DefaultFunction, DefaultFurniture
- **Use Case**: Creating rooms with proper sizing and requirements
- **Examples**: Bedroom (9-25 m²), Kitchen (8-20 m²), Bathroom (4-12 m²)

#### **SPATIAL_ADJACENCY.csv**
- **Purpose**: Defines spatial relationships between room types
- **Key Fields**: RoomType1, RoomType2, Relationship, Priority, RequiredConnection, MinDistance, MaxDistance
- **Use Case**: Intelligent room placement and layout optimization
- **Examples**: Kitchen adjacent to Dining (High priority), Bathroom separate from Kitchen (High priority)

#### **DESIGN_RULES.csv**
- **Purpose**: 50+ building code and design standard requirements
- **Key Fields**: RuleID, Category, Rule, Severity, Standard, ValidationFormula, MinValue, MaxValue
- **Use Case**: Automated design validation and code compliance checking
- **Standards**: IBC, ADA, ASHRAE, NEC, UPC
- **Examples**: DR001 (Bedroom window min 0.5m²), DR004 (Doors min 900mm)

#### **ROOM_REQUIREMENTS.csv**
- **Purpose**: Detailed requirements for each room type
- **Key Fields**: RoomType, MinArea, MinWidth, MinHeight, RequiredVentilation, RequiredLighting, RequiredOutlets, RequiredFixtures
- **Use Case**: Comprehensive room specification and validation
- **Examples**: Kitchen requires 15 ACH ventilation, 300 lux lighting

#### **FURNITURE_REQUIREMENTS.csv**
- **Purpose**: Furniture specifications and placement rules for each room
- **Key Fields**: RoomType, FurnitureItem, Quantity, MinClearance, Placement, Priority, Dimensions
- **Use Case**: Automated furniture placement and room furnishing
- **Examples**: Bedroom requires bed, nightstands, wardrobe with specific clearances

#### **CODE_REQUIREMENTS.csv**
- **Purpose**: Comprehensive building code requirements from multiple standards
- **Key Fields**: Standard, Category, Requirement, MinValue, MaxValue, Unit, ApplicableElements, Severity
- **Use Case**: Multi-standard compliance validation
- **Standards Covered**: IBC, ADA, ASHRAE, NEC, UPC, IECC, NFPA, ANSI, BS, ISO, Local codes
- **Examples**: IBC egress door min 810mm, ADA ramp max 8.33% slope

### 2. Element Creation Layer (`/elements/`)

#### **WALL_TYPES.csv**
- **Purpose**: 34 comprehensive wall type definitions
- **Key Fields**: WallType, Thickness, Material, FireRating, Acoustic_STC, ThermalR_Value, UseCase, LoadBearing
- **Use Case**: Automated wall creation with proper specifications
- **Types Include**: Interior Standard, Exterior Brick, Party Wall, Fire Wall, Curtain Wall, Foundation Wall
- **Examples**: Exterior_Brick (300mm, Fire Rating 60min, STC 45, R-2.5)

### 3. Family/Element Library (`/families/`)

#### **FAMILY_CATALOG.csv**
- **Purpose**: 100+ family definitions for all building elements
- **Key Fields**: FamilyName, Category, DefaultWidth, DefaultHeight, DefaultDepth, PlacementType, RequiresHost, ParameterSet
- **Categories**: Doors, Windows, Stairs, Columns, Beams, Floors, Roofs, Plumbing Fixtures, Mechanical Equipment, Electrical Fixtures, Furniture
- **Use Case**: Element selection and placement
- **Examples**: SingleDoor_Swing (900x2100), CasementWindow_Double (1800x1200), Bed_Queen (1530x2030)

#### **FAMILY_PARAMETERS.csv**
- **Purpose**: Parameter definitions for each family category
- **Key Fields**: ParameterSet, ParameterName, DataType, DefaultValue, Unit, IsInstanceParameter, Formula
- **Use Case**: Configurable element properties and calculations
- **Parameter Sets**: Door_Standard, Window_Fixed, Stair_Standard, Column_Structural, Plumbing fixtures, MEP equipment
- **Examples**: Door width/height/thickness, Window glazing type, Stair tread/riser dimensions

#### **FAMILY_PLACEMENT_RULES.csv**
- **Purpose**: Placement logic and constraints for all family types
- **Key Fields**: FamilyCategory, PlacementRule, RequiredHost, PreferredLocation, MinimumClearance, ValidationRule
- **Use Case**: Intelligent element placement with constraint checking
- **Rules Cover**: Wall-hosted elements, floor-based elements, route-based systems, accessibility requirements
- **Examples**: Doors require walls with adequate width, Toilets need 400mm clearance and adjacent wall

#### **FAMILY_RELATIONSHIPS.csv**
- **Purpose**: Dependencies and relationships between family types
- **Key Fields**: PrimaryFamily, RelatedFamily, RelationshipType, RequirementLevel, ProximityRule, MinDistance, MaxDistance
- **Use Case**: Automated component relationships and system validation
- **Relationships**: Requires, Suggests, Supports, Connects_To, Controls, Feeds
- **Examples**: Sink requires faucet, AC_Split_Indoor requires AC_Split_Outdoor, Duct connects to diffuser

### 4. Materials Library (`/materials/`)

#### **BLE_MATERIALS.csv** (Building Elements Materials)
- **Purpose**: 80+ material specifications for building construction
- **Key Fields**: Category, MaterialName, Manufacturer, ThermalConductivity, Density, Cost_Per_Unit, Thickness, FireRating, AcousticRating, Application
- **Categories**: Wall, Ceiling, Floor, Roof, Door, Window, Finish, Insulation, Waterproofing
- **Use Case**: Material selection with thermal, acoustic, and cost analysis
- **Examples**: Concrete_C30 (1.4 W/mK, 120min fire rating), Brick_Common (0.8 W/mK, 60min), Gypsum_Board (0.25 W/mK, 30min)

#### **MEP_MATERIALS.csv** (MEP Systems Materials)
- **Purpose**: 90+ specifications for MEP system components
- **Key Fields**: Category, MaterialName, Specification, Size_Range, Material_Type, Pressure_Rating, Temperature_Rating, Cost_Per_Unit, Application, Standard
- **Categories**: Electrical Cable, Conduit, Cable Tray, Plumbing Pipe, Drainage Pipe, HVAC Duct, Gas Pipe, Valves, Fittings, Devices
- **Standards**: BS, EN, ASTM, DIN, SMACNA, UL
- **Use Case**: MEP system design and specification
- **Examples**: Copper_15mm (PN 16, 110°C, BS EN 1057), PVC_110mm_Soil (BS EN 1329), Galv_Duct (SMACNA)

### 5. NLP Training Data (`/training/`)

#### **ENTITY_DICTIONARY.csv**
- **Purpose**: Comprehensive entity recognition for natural language processing
- **Key Fields**: Entity, Synonyms, Category, Examples, Intent_Association
- **Categories**: Element, RoomType, Intent, Direction, BuildingType, Size, Dimension, Property, Location, Unit, ElementType, WallType, Material, Qualifier, Layout, Relationship, BuildingElement, Furniture, Fixture
- **Use Case**: Natural language command parsing and intent recognition
- **Intents Supported**: CREATE_BUILDING, PLACE_ELEMENT, DELETE_ELEMENT, MODIFY_DIMENSION, MOVE_ELEMENT, QUERY_PROPERTY
- **Examples**: 
  - "Create a 3-bedroom house" → Intent: CREATE_BUILDING, Entities: {rooms:3, type:bedroom}
  - "Add a door to the north wall" → Intent: PLACE_ELEMENT, Entities: {element:door, target:wall, direction:north}
  - "Make the wall 4 meters long" → Intent: MODIFY_DIMENSION, Entities: {element:wall, dimension:length, value:4, unit:meters}

## Usage Guidelines

### For Design Knowledge Base
1. Use ROOM_DEFINITIONS for initial room creation with default parameters
2. Apply SPATIAL_ADJACENCY rules for intelligent room arrangement
3. Validate designs against DESIGN_RULES and CODE_REQUIREMENTS
4. Populate rooms using FURNITURE_REQUIREMENTS

### For Element Creation
1. Select appropriate wall type from WALL_TYPES based on use case
2. Choose families from FAMILY_CATALOG based on category
3. Apply parameters from FAMILY_PARAMETERS
4. Validate placement using FAMILY_PLACEMENT_RULES
5. Check relationships using FAMILY_RELATIONSHIPS

### For Material Selection
1. Query BLE_MATERIALS for building envelope and structure
2. Query MEP_MATERIALS for services systems
3. Filter by performance requirements (thermal, acoustic, fire rating)
4. Consider cost and sustainability factors

### For NLP Processing
1. Use ENTITY_DICTIONARY for tokenization and entity extraction
2. Map user inputs to intents and entities
3. Extract parameters (quantities, dimensions, materials)
4. Resolve references (wall, room, door)
5. Build structured commands for execution

## Data Validation

All CSV files include:
- ✓ Consistent formatting and structure
- ✓ Comprehensive field coverage
- ✓ Realistic default values
- ✓ Industry-standard units
- ✓ Reference to applicable standards
- ✓ Cross-referenced relationships

## Integration Points

### Workflow Example:
1. **User Input**: "Create a 3-bedroom house"
   - Parse with ENTITY_DICTIONARY
   - Extract: Building type, room count, room types

2. **Room Creation**:
   - Query ROOM_DEFINITIONS for bedroom specifications
   - Apply ROOM_REQUIREMENTS for detailed specs
   - Use SPATIAL_ADJACENCY for layout

3. **Element Placement**:
   - Select families from FAMILY_CATALOG
   - Apply WALL_TYPES for partitions
   - Use FAMILY_PLACEMENT_RULES for positioning

4. **Validation**:
   - Check DESIGN_RULES compliance
   - Verify CODE_REQUIREMENTS
   - Validate FAMILY_RELATIONSHIPS

5. **Material Assignment**:
   - Select from BLE_MATERIALS and MEP_MATERIALS
   - Apply based on element type and location

## Technical Specifications

- **File Format**: CSV (Comma-Separated Values)
- **Encoding**: UTF-8
- **Line Endings**: Unix (LF)
- **Delimiter**: Comma (,)
- **Text Qualifier**: None (fields with commas use semicolon as internal separator)
- **Numeric Format**: Decimal point notation
- **Units**: Metric (mm, m, m², kPa, kW, etc.)

## Standards Referenced

- **IBC**: International Building Code
- **ADA**: Americans with Disabilities Act
- **ASHRAE**: American Society of Heating, Refrigerating and Air-Conditioning Engineers
- **NEC**: National Electrical Code
- **UPC**: Uniform Plumbing Code
- **IECC**: International Energy Conservation Code
- **NFPA**: National Fire Protection Association
- **BS/EN**: British/European Standards
- **ISO**: International Organization for Standardization

## Version Information

- **Version**: 1.0
- **Date**: February 2026
- **Coverage**: Residential and light commercial buildings
- **Region**: International (with UK/US standards emphasis)

## Support and Extension

### Adding New Elements:
1. Add entry to appropriate catalog (FAMILY_CATALOG, WALL_TYPES, etc.)
2. Define parameters in FAMILY_PARAMETERS
3. Add placement rules to FAMILY_PLACEMENT_RULES
4. Update ENTITY_DICTIONARY with synonyms
5. Add material specifications if needed

### Custom Room Types:
1. Define in ROOM_DEFINITIONS with requirements
2. Add relationships in SPATIAL_ADJACENCY
3. Specify furniture in FURNITURE_REQUIREMENTS
4. Update validation rules in DESIGN_RULES if needed

### New Materials:
1. Add to BLE_MATERIALS or MEP_MATERIALS
2. Include all performance characteristics
3. Reference applicable standards
4. Update cost database

## Notes

- All dimensions in millimeters unless specified
- Areas in square meters (m²)
- Volumes in cubic meters (m³)
- Pressures in kilopascals (kPa) or bar
- Temperatures in Celsius (°C)
- Costs in local currency per unit

## Credits

Compiled from:
- International building codes and standards
- Manufacturer specifications
- Industry best practices
- Revit parameter schemas
- BIM standards (ISO 19650)
