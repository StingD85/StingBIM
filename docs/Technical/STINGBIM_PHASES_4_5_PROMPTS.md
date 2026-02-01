# STINGBIM PROMPT LIBRARY - PHASES 4-5 CONTINUATION
**Advanced AI & User Interface Prompts**

---

## 🤖 PHASE 4: ADVANCED AI SYSTEMS (Week 15-19)

### [P4.1] DWG PARSER (netDXF)

**Copy this entire prompt:**

```
Create comprehensive DWG/DXF file parser using netDXF library:

PROJECT: StingBIM.DWGConverter
NAMESPACE: StingBIM.DWGConverter.Parser
PURPOSE: Parse all DWG versions (R12-2018), extract entities

═══════════════════════════════════════════════════════════════════
REQUIREMENTS
═══════════════════════════════════════════════════════════════════

1. FILE SUPPORT:
   ✓ DWG formats: R12, R13, R14, 2000, 2004, 2007, 2010, 2013, 2018
   ✓ DXF formats: ASCII and Binary
   ✓ Large files (>100MB)
   ✓ Multiple layouts/tabs

2. ENTITY EXTRACTION:
   ✓ Lines, Polylines, Arcs, Circles
   ✓ Blocks (with insertion points)
   ✓ Text, MText
   ✓ Dimensions
   ✓ Hatches
   ✓ Layers (with properties)

3. METADATA:
   ✓ Drawing units
   ✓ Scale detection
   ✓ Layer standards (AIA, BS1192, ISO13567)
   ✓ Block definitions
   ✓ Text styles

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (4,200 LINES)
═══════════════════════════════════════════════════════════════════

1. DWGReader.cs (2,000 lines)
   
   PUBLIC API:
   DWGDocument Read(string filePath)
   Task<DWGDocument> ReadAsync(string filePath, IProgress<int> progress, CancellationToken ct)
   DWGDocument ReadFromStream(Stream stream)
   DWGMetadata GetMetadata(string filePath) // Quick metadata without full parsing
   
   FEATURES:
   - Automatic format detection
   - Error recovery for corrupted files
   - Partial loading (load only specific layers)
   - Memory efficient for large files

2. LayerAnalyzer.cs (1,200 lines)
   
   LAYER ANALYSIS:
   List<LayerInfo> ExtractLayers(DWGDocument doc)
   LayerStandard DetectStandard(List<LayerInfo> layers)
   Dictionary<string, string> MapLayersToDisciplines(List<LayerInfo> layers)
   
   LAYER STANDARDS:
   - AIA (American Institute of Architects)
   - BS1192 (British Standard)
   - ISO13567 (International)
   - Custom/Unknown

3. EntityExtractor.cs (1,000 lines)
   
   ENTITY EXTRACTION:
   List<LineEntity> ExtractLines(DWGDocument doc, string layerName = null)
   List<PolylineEntity> ExtractPolylines(DWGDocument doc)
   List<BlockEntity> ExtractBlocks(DWGDocument doc)
   List<TextEntity> ExtractText(DWGDocument doc)
   List<DimensionEntity> ExtractDimensions(DWGDocument doc)
   
   FILTERING:
   - By layer
   - By color
   - By line type
   - By block name

4. DWGDocument.cs (Data Model) (500 lines)
   
   PROPERTIES:
   string FilePath { get; }
   DWGVersion Version { get; }
   DrawingUnits Units { get; }
   double DetectedScale { get; }
   List<LayerInfo> Layers { get; }
   List<BlockDefinition> Blocks { get; }
   Dictionary<string, List<EntityBase>> EntitiesByLayer { get; }
   BoundingBox Bounds { get; }
   
   METHODS:
   List<T> GetEntities<T>(string layerName = null) where T : EntityBase
   LayerInfo GetLayer(string name)
   BlockDefinition GetBlock(string name)

5. ScaleDetector.cs (500 lines)
   
   SCALE DETECTION:
   double DetectScale(DWGDocument doc) // Analyzes dimensions, text size
   ScaleConfidence GetConfidence() // 0-100%
   List<ScaleCandidate> GetScaleCandidates() // Multiple possible scales
   
   METHODS:
   - Analyze dimension values vs actual distances
   - Check text heights
   - Look for scale bars
   - Parse title blocks

═══════════════════════════════════════════════════════════════════
USAGE EXAMPLES
═══════════════════════════════════════════════════════════════════

EXAMPLE 1: Read DWG file
```csharp
var reader = new DWGReader();
var doc = await reader.ReadAsync("FloorPlan.dwg", progress, ct);

Console.WriteLine($"Version: {doc.Version}");
Console.WriteLine($"Units: {doc.Units}");
Console.WriteLine($"Scale: 1:{doc.DetectedScale}");
Console.WriteLine($"Layers: {doc.Layers.Count}");
Console.WriteLine($"Blocks: {doc.Blocks.Count}");
```

EXAMPLE 2: Extract walls (polylines on A-WALL layer)
```csharp
var extractor = new EntityExtractor();
var walls = extractor.ExtractPolylines(doc)
    .Where(p => p.Layer == "A-WALL")
    .ToList();

Console.WriteLine($"Found {walls.Count} wall polylines");
```

EXAMPLE 3: Detect layer standard
```csharp
var analyzer = new LayerAnalyzer();
var layers = analyzer.ExtractLayers(doc);
var standard = analyzer.DetectStandard(layers);

Console.WriteLine($"Layer standard: {standard}"); // AIA, BS1192, etc.

var disciplines = analyzer.MapLayersToDisciplines(layers);
foreach (var kvp in disciplines)
{
    Console.WriteLine($"{kvp.Key} → {kvp.Value}");
    // A-WALL → Architecture
    // S-BEAM → Structure
    // M-HVAC → Mechanical
}
```

EXAMPLE 4: Extract blocks (doors, windows)
```csharp
var doors = extractor.ExtractBlocks(doc)
    .Where(b => b.Name.Contains("DOOR"))
    .ToList();

foreach (var door in doors)
{
    Console.WriteLine($"Door at {door.InsertionPoint}, Rotation: {door.Rotation}");
}
```

═══════════════════════════════════════════════════════════════════
ERROR HANDLING
═══════════════════════════════════════════════════════════════════

EXCEPTIONS:
- UnsupportedDWGVersionException - DWG version too old/new
- CorruptedFileException - File is damaged
- InvalidScaleException - Cannot determine scale
- LayerNotFoundException - Specified layer doesn't exist

ERROR RECOVERY:
- Skip corrupted entities, continue parsing
- Provide partial results when possible
- Log all errors with entity context
- Suggest fixes for common issues

═══════════════════════════════════════════════════════════════════
PERFORMANCE
═══════════════════════════════════════════════════════════════════

BENCHMARKS:
- Small file (<5MB): <2 seconds
- Medium file (5-50MB): <10 seconds
- Large file (50-100MB): <30 seconds
- Metadata only: <500ms

MEMORY:
- Stream large files (don't load all in memory)
- Use lazy loading for entities
- Maximum 1GB memory usage

═══════════════════════════════════════════════════════════════════
TECH STACK
═══════════════════════════════════════════════════════════════════

NUGET:
- netDxf.netstandard (3.0.0) - DWG/DXF library
- System.IO.Compression - for compressed DWG files

═══════════════════════════════════════════════════════════════════
OUTPUT
═══════════════════════════════════════════════════════════════════

Provide complete C# code for:
1. DWGReader.cs (2,000 lines)
2. LayerAnalyzer.cs (1,200 lines)
3. EntityExtractor.cs (1,000 lines)
4. DWGDocument.cs (500 lines)
5. ScaleDetector.cs (500 lines)
6. Unit tests (800 lines)
7. Sample DWG files for testing

TOTAL: 4,200 lines
```

---

### [P4.2] AI LAYER CLASSIFIER (ML.NET)

**Copy this entire prompt:**

```
Create AI-powered layer classification system:

PROJECT: StingBIM.DWGConverter
NAMESPACE: StingBIM.DWGConverter.Classifier
PURPOSE: 99.2% accuracy on layer classification

═══════════════════════════════════════════════════════════════════
ML MODEL
═══════════════════════════════════════════════════════════════════

CLASSIFICATION:
- Input: Layer name (string)
- Output: Discipline + Category (200+ classes)
- Training: 10,000+ layer names
- Algorithm: Multi-class LightGBM
- Accuracy: 99.2%+

CLASSES (Examples):
- Architecture.Wall
- Architecture.Door
- Architecture.Window
- Structure.Column
- Structure.Beam
- Mechanical.HVAC
- Electrical.Power
- Plumbing.Pipe

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (3,500 LINES)
═══════════════════════════════════════════════════════════════════

1. LayerClassifier.cs (1,500 lines)
   
   METHODS:
   LayerClassification Classify(string layerName)
   List<LayerClassification> ClassifyBatch(List<string> layerNames)
   float GetConfidence(string layerName, LayerClass predictedClass)
   void Train(List<TrainingSample> samples)
   void SaveModel(string path)
   void LoadModel(string path)

2. FeatureExtractor.cs (1,000 lines)
   
   FEATURES:
   - Layer name tokens (split by dash, underscore)
   - Prefix (first token)
   - Suffix (last token)
   - Contains discipline codes (A-, S-, M-, E-, P-)
   - Contains keywords (WALL, DOOR, BEAM, etc.)
   - Character patterns
   - Length

3. ModelTrainer.cs (1,000 lines)
   
   TRAINING PIPELINE:
   - Load training data (10,000+ samples)
   - Feature engineering
   - Model training (LightGBM)
   - Cross-validation (5-fold)
   - Hyperparameter tuning
   - Model evaluation

═══════════════════════════════════════════════════════════════════
TRAINING DATA
═══════════════════════════════════════════════════════════════════

Generate from standards:

AIA LAYERS:
A-WALL → Architecture.Wall
A-DOOR → Architecture.Door
S-COLS → Structure.Column
M-HVAC → Mechanical.HVAC

BS1192 LAYERS:
(-)-A-WALL → Architecture.Wall
(-)-S-BEAM → Structure.Beam

ISO13567 LAYERS:
A_WALL → Architecture.Wall
E_LIGHT → Electrical.Lighting

TOTAL SAMPLES: 10,000+ layer names covering 200+ classes

═══════════════════════════════════════════════════════════════════
USAGE
═══════════════════════════════════════════════════════════════════

```csharp
var classifier = new LayerClassifier();
classifier.LoadModel("layer-classifier.zip");

var result = classifier.Classify("A-WALL");
Console.WriteLine($"Discipline: {result.Discipline}"); // Architecture
Console.WriteLine($"Category: {result.Category}"); // Wall
Console.WriteLine($"Confidence: {result.Confidence:P}"); // 99.8%
```

═══════════════════════════════════════════════════════════════════
ACCURACY REQUIREMENTS
═══════════════════════════════════════════════════════════════════

METRICS:
- Overall Accuracy: >99.2%
- Precision: >98%
- Recall: >98%
- F1 Score: >98%

OUTPUT:
Complete C# code + training script + model file + tests (3,500 lines)
```

---

### [P4.3] DWG-TO-REVIT CONVERTER

**Copy this entire prompt:**

```
Create DWG-to-Revit conversion engine:

PROJECT: StingBIM.DWGConverter
NAMESPACE: StingBIM.DWGConverter.Converter
PURPOSE: 4.0 sec/sheet, 99.2% accuracy

═══════════════════════════════════════════════════════════════════
CONVERSION PIPELINE
═══════════════════════════════════════════════════════════════════

1. Parse DWG → DWGDocument
2. Classify layers → Disciplines
3. Detect scale → 1:50, 1:100, etc.
4. Convert entities:
   - Polylines → Walls
   - Blocks → Doors/Windows (Families)
   - Text → TextNotes
   - Dimensions → Dimensions
5. Validate → Check results
6. Report → Conversion statistics

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (4,500 LINES)
═══════════════════════════════════════════════════════════════════

1. DWGToRevitConverter.cs (2,000 lines)
   
   PUBLIC API:
   ConversionResult Convert(string dwgPath, Document doc, ConversionOptions options = null)
   Task<ConversionResult> ConvertAsync(string dwgPath, Document doc, IProgress<ConversionProgress> progress)
   
   PIPELINE:
   - Parse DWG
   - Classify layers
   - Detect scale
   - Convert walls
   - Convert doors/windows
   - Convert text
   - Validate
   - Report

2. PolylineToWall.cs (1,000 lines)
   
   CONVERSION:
   List<Wall> Convert(List<PolylineEntity> polylines, Document doc, WallType wallType)
   
   FEATURES:
   - Detect wall thickness from double lines
   - Handle curves
   - Join connected polylines
   - Set wall height (from level or default)
   - Apply base offset

3. BlockToFamily.cs (1,200 lines)
   
   FAMILY MAPPING:
   Dictionary<string, FamilySymbol> MapBlocks(List<BlockEntity> blocks, Document doc)
   
   CONVERSION:
   - Doors: Match by size, create instances
   - Windows: Match by size, sill height
   - Generic: Place as generic model families

4. ConversionValidator.cs (800 lines)
   
   VALIDATION:
   - Check element counts match
   - Validate geometry accuracy
   - Check for missing elements
   - Verify scale correctness
   - Report warnings/errors

5. ConversionResult.cs (500 lines)
   
   STATISTICS:
   - Walls created
   - Doors placed
   - Windows placed
   - Text notes
   - Errors
   - Warnings
   - Processing time
   - Accuracy percentage

═══════════════════════════════════════════════════════════════════
USAGE
═══════════════════════════════════════════════════════════════════

```csharp
var converter = new DWGToRevitConverter();

var options = new ConversionOptions
{
    DefaultWallHeight = 9.0, // feet
    CreateLevel = true,
    MergeConnectedWalls = true
};

var result = await converter.ConvertAsync("FloorPlan.dwg", doc, progress);

Console.WriteLine($"Walls: {result.WallsCreated}");
Console.WriteLine($"Doors: {result.DoorsPlaced}");
Console.WriteLine($"Windows: {result.WindowsPlaced}");
Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F1}s");
Console.WriteLine($"Accuracy: {result.Accuracy:P}");
```

═══════════════════════════════════════════════════════════════════
PERFORMANCE REQUIREMENTS
═══════════════════════════════════════════════════════════════════

TARGETS:
- Typical floor plan: <4.0 seconds
- Large plan (1,000+ entities): <10 seconds
- Accuracy: >99.2%

OUTPUT:
Complete C# code (4,500 lines) + tests + sample files
```

---

### [P4.4] IMAGE-TO-BIM VISION SYSTEM

**Copy this entire prompt:**

```
Create computer vision preprocessing for Image-to-BIM:

PROJECT: StingBIM.ImageToBIM
NAMESPACE: StingBIM.ImageToBIM.Vision
PURPOSE: Prepare images for YOLOv9 and SAM

═══════════════════════════════════════════════════════════════════
PREPROCESSING PIPELINE
═══════════════════════════════════════════════════════════════════

1. Load image (JPEG, PNG, TIFF)
2. Resize to 640×640 (YOLOv9 input)
3. Normalize pixels [0-255] → [0-1]
4. Convert to RGB (if grayscale)
5. Apply CLAHE (contrast enhancement)
6. Denoise
7. Sharpen edges
8. Prepare ONNX input tensor

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (2,300 LINES)
═══════════════════════════════════════════════════════════════════

1. ImagePreprocessor.cs (1,500 lines)
   
   PUBLIC API:
   PreprocessedImage Preprocess(string imagePath, PreprocessOptions options = null)
   Task<PreprocessedImage> PreprocessAsync(string imagePath)
   float[] GetONNXInputTensor(PreprocessedImage image)
   
   PROCESSING:
   - Load image (OpenCvSharp)
   - Resize to target size
   - Normalize pixel values
   - Apply CLAHE (Contrast Limited Adaptive Histogram Equalization)
   - Denoise (Non-local Means)
   - Sharpen (Unsharp Mask)
   - Convert to NCHW format for ONNX

2. ModelLoader.cs (800 lines)
   
   ONNX MODEL LOADING:
   InferenceSession LoadYOLOv9(string modelPath)
   InferenceSession LoadSAM(string modelPath)
   InferenceSession LoadLayoutLM(string modelPath)
   
   FEATURES:
   - Automatic GPU detection
   - CPU fallback
   - Model validation
   - Memory management

═══════════════════════════════════════════════════════════════════
USAGE
═══════════════════════════════════════════════════════════════════

```csharp
var preprocessor = new ImagePreprocessor();

var preprocessed = await preprocessor.PreprocessAsync("floorplan.jpg");

// Get tensor for ONNX model
var inputTensor = preprocessor.GetONNXInputTensor(preprocessed);

// Run YOLOv9 detection
var session = ModelLoader.LoadYOLOv9("yolov9-wall-detector.onnx");
var outputs = session.Run(new[] { inputTensor });
```

═══════════════════════════════════════════════════════════════════
TECH STACK
═══════════════════════════════════════════════════════════════════

NUGET:
- OpenCvSharp4 (4.8.1) - Computer vision
- Microsoft.ML.OnnxRuntime (1.16.3) - ONNX inference
- SixLabors.ImageSharp (3.1.2) - Image loading

OUTPUT:
Complete C# code (2,300 lines) + tests
```

---

### [P4.5] YOLOV9 WALL DETECTOR

**Copy this entire prompt:**

```
Create YOLOv9-based wall detection system:

PROJECT: StingBIM.ImageToBIM
NAMESPACE: StingBIM.ImageToBIM.Detection
PURPOSE: 99.2% mAP, <2 sec per image

═══════════════════════════════════════════════════════════════════
YOLOV9 MODEL
═══════════════════════════════════════════════════════════════════

MODEL FILE: yolov9-wall-detector.onnx (200MB)
INPUT: 640×640×3 RGB image
OUTPUT: Bounding boxes for walls

CLASSES:
- Wall (exterior)
- Wall (interior)
- Wall (partition)

PERFORMANCE:
- mAP@0.5: >99.2%
- Inference time: <500ms per image
- GPU accelerated

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (2,500 LINES)
═══════════════════════════════════════════════════════════════════

1. YOLOv9Detector.cs (2,000 lines)
   
   PUBLIC API:
   List<Detection> Detect(PreprocessedImage image)
   Task<List<Detection>> DetectAsync(PreprocessedImage image)
   
   DETECTION:
   - Run ONNX inference
   - Post-process outputs (NMS)
   - Convert to bounding boxes
   - Filter by confidence threshold
   
   POST-PROCESSING:
   - Non-Maximum Suppression (NMS)
   - Confidence filtering (>0.5)
   - Class selection

2. Detection.cs (500 lines)
   
   DETECTION RESULT:
   - BoundingBox (x, y, width, height)
   - Class (Wall type)
   - Confidence (0-1)
   - Coordinates (scaled to original image)

═══════════════════════════════════════════════════════════════════
USAGE
═══════════════════════════════════════════════════════════════════

```csharp
var detector = new YOLOv9Detector("yolov9-wall-detector.onnx");

var detections = await detector.DetectAsync(preprocessedImage);

Console.WriteLine($"Detected {detections.Count} walls");

foreach (var detection in detections)
{
    Console.WriteLine($"Wall at {detection.BoundingBox}, confidence: {detection.Confidence:P}");
}
```

═══════════════════════════════════════════════════════════════════
PERFORMANCE
═══════════════════════════════════════════════════════════════════

BENCHMARKS:
- Inference (GPU): <500ms
- Inference (CPU): <2 seconds
- mAP@0.5: >99.2%

OUTPUT:
Complete C# code (2,500 lines) + ONNX model + tests
```

---

## 💻 PHASE 5: USER INTERFACE & INTEGRATION (Week 20-22)

### [P5.1] COMMAND CONSOLE (WPF)

**Copy this entire prompt:**

```
Create professional command console interface:

PROJECT: StingBIM.Console
NAMESPACE: StingBIM.Console.UI
PURPOSE: 500+ commands, <100ms response

═══════════════════════════════════════════════════════════════════
REQUIREMENTS
═══════════════════════════════════════════════════════════════════

1. WPF INTERFACE:
   ✓ Dockable panel (can dock anywhere in Revit)
   ✓ Command input textbox
   ✓ Output/history panel (scrollable)
   ✓ Syntax highlighting
   ✓ Auto-completion (Tab key)
   ✓ Command history (Up/Down arrows)
   ✓ Clear command (clear/cls)

2. COMMAND SYSTEM:
   ✓ 500+ commands across all StingBIM features
   ✓ Command aliases (shortcuts)
   ✓ Help system (help <command>)
   ✓ Command categories
   ✓ Parameter validation
   ✓ Error messages

3. PERFORMANCE:
   ✓ Command execution: <100ms
   ✓ Auto-completion: <50ms
   ✓ Syntax highlighting: <10ms
   ✓ History search: <20ms

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (3,900 LINES)
═══════════════════════════════════════════════════════════════════

1. ConsoleWindow.xaml (300 lines XAML)
   
   LAYOUT:
   - Title bar with minimize/close
   - Command input (TextBox)
   - Output panel (RichTextBox)
   - Status bar
   - Auto-completion dropdown
   
   STYLING:
   - Dark theme (default)
   - Light theme (option)
   - Syntax highlighting colors
   - Monospace font

2. ConsoleWindow.xaml.cs (1,200 lines)
   
   FEATURES:
   - Command input handling
   - Auto-completion logic
   - History navigation (Up/Down)
   - Output formatting
   - Syntax highlighting
   - Docking management

3. ConsoleViewModel.cs (800 lines)
   
   MVVM PATTERN:
   - Commands (ICommand)
   - ObservableCollections
   - Property change notifications
   - Command binding

4. CommandRegistry.cs (1,000 lines)
   
   COMMAND REGISTRATION:
   Dictionary<string, ICommand> RegisteredCommands
   
   COMMANDS (500+):
   
   PROJECT (50 commands):
   - project.info
   - project.save
   - project.close
   - project.export
   
   PARAMETERS (80 commands):
   - param.create <name> <type>
   - param.set <element> <name> <value>
   - param.get <element> <name>
   - param.delete <element> <name>
   - param.list [element]
   - param.batch.update <filter> <name> <value>
   
   SCHEDULES (60 commands):
   - schedule.create <type>
   - schedule.generate <template>
   - schedule.export <name> [format]
   
   MATERIALS (40 commands):
   - material.apply <element> <material>
   - material.list
   - material.search <query>
   
   FORMULAS (30 commands):
   - formula.run <name>
   - formula.calculate <element> <formula>
   
   GENIUS TAG (70 commands):
   - tag.place <element>
   - tag.batch <selection>
   - tag.quality <tag>
   - tag.learn
   
   CONVERSION (50 commands):
   - dwg.import <file>
   - dwg.convert <file>
   - image.import <file>
   - image.convert <file>
   
   BATCH (40 commands):
   - batch.select <filter>
   - batch.process <operation>
   - batch.undo
   
   SYSTEM (30 commands):
   - help [command]
   - clear / cls
   - history
   - exit
   - settings
   - version
   
   ADVANCED (50 commands):
   - script.run <file>
   - macro.record
   - macro.play <name>

5. CommandParser.cs (600 lines)
   
   PARSING:
   ParsedCommand Parse(string input)
   
   SYNTAX:
   - Command name
   - Parameters (positional and named)
   - Flags (--flag or -f)
   - Quoted strings ("value with spaces")
   - Escape sequences

═══════════════════════════════════════════════════════════════════
USAGE EXAMPLES
═══════════════════════════════════════════════════════════════════

SIMPLE COMMANDS:
```
> project.info
Project: Office Building
File: C:\Projects\Office.rvt
Modified: 2026-01-31

> param.list wall_123
Parameters for Wall id: wall_123:
- Height: 9.0 ft
- Thickness: 8 in
- Fire Rating: 2-Hour
```

BATCH OPERATIONS:
```
> batch.select category:Walls
Selected 1,247 walls

> param.batch.update selection Fire_Rating "1-Hour"
Updated 1,247 elements in 0.8 seconds
```

GENIUS TAG:
```
> tag.batch selection
Tagging 1,247 walls...
Progress: 100%
Tagged 1,247 elements in 8.2 seconds
Average quality: 87.3
```

AUTO-COMPLETION:
```
> par<Tab>
param.create
param.set
param.get
param.delete
param.list
param.batch.update

> param.<Tab>
create
set
get
...
```

═══════════════════════════════════════════════════════════════════
SYNTAX HIGHLIGHTING
═══════════════════════════════════════════════════════════════════

COLORS:
- Command name: Blue
- Parameters: Green
- Strings: Orange
- Numbers: Cyan
- Flags: Purple
- Errors: Red

═══════════════════════════════════════════════════════════════════
TECH STACK
═══════════════════════════════════════════════════════════════════

NUGET:
- MaterialDesignThemes (4.9.0) - UI components
- AvalonEdit (6.3.0) - Syntax highlighting
- ReactiveUI (19.5.31) - MVVM framework

═══════════════════════════════════════════════════════════════════
OUTPUT
═══════════════════════════════════════════════════════════════════

Provide complete C# + XAML code for:
1. ConsoleWindow.xaml (300 lines)
2. ConsoleWindow.xaml.cs (1,200 lines)
3. ConsoleViewModel.cs (800 lines)
4. CommandRegistry.cs (1,000 lines)
5. CommandParser.cs (600 lines)
6. Unit tests (500 lines)

TOTAL: 3,900 lines + 500 commands defined
```

---

### [P5.2] RIBBON INTERFACE

**Copy this entire prompt:**

```
Create Revit ribbon interface for StingBIM:

PROJECT: StingBIM.AddIn
NAMESPACE: StingBIM.AddIn.Ribbon
PURPOSE: Professional ribbon with all commands

═══════════════════════════════════════════════════════════════════
RIBBON LAYOUT
═══════════════════════════════════════════════════════════════════

TAB: "StingBIM"

PANEL 1: Quick Access
- Command Console (large button)
- GENIUS TAG (large button)
- Help (button)

PANEL 2: Parameters
- Load Parameters (button)
- Parameter Manager (split button)
  → Apply to Selection
  → Batch Update
  → Validate

PANEL 3: Automation
- Generate Schedules (button)
- Apply Materials (button)
- Run Formulas (button)
- Validate Standards (button)

PANEL 4: Conversion
- Import DWG (split button)
  → Convert to Revit
  → Preview Only
- Import Image (split button)
  → Convert to BIM
  → Extract Data

PANEL 5: Tools
- Sheet Manager (button)
- Analytics (button)
- Settings (button)

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (1,500 LINES)
═══════════════════════════════════════════════════════════════════

1. RibbonBuilder.cs (1,000 lines)
   
   METHODS:
   void CreateRibbon(UIControlledApplication app)
   void AddTab(UIControlledApplication app, string tabName)
   void AddPanels(RibbonPanel[] panels)
   void AddButtons(RibbonPanel panel, ButtonData[] buttons)

2. ExternalCommands.cs (500 lines)
   
   COMMANDS:
   - OpenConsoleCommand
   - GeniusTagCommand
   - LoadParametersCommand
   - ParameterManagerCommand
   - GenerateSchedulesCommand
   - etc. (15-20 commands)

═══════════════════════════════════════════════════════════════════
OUTPUT
═══════════════════════════════════════════════════════════════════

Complete C# code (1,500 lines) + icons (PNG) + manifest file
```

---

## ✅ FINAL DELIVERABLE SUMMARY

**Total Prompts:** 50+  
**Total Lines:** 126,500  
**Phases Covered:** All 5 phases  
**Timeline:** 22 weeks  

**Usage:** Copy each prompt → Paste into Claude Code → Get instant production code

**Quality:** Production-ready, tested, documented

---

All prompts are ready to copy-paste into Claude Code for instant code generation! 🚀