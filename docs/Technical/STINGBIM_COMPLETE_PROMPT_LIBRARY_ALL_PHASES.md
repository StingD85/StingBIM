# STINGBIM - COMPLETE CLAUDE CODE PROMPT LIBRARY
**All 50+ Production-Ready Prompts for 22-Week Build**

**Date:** January 31, 2026  
**Coverage:** All 126,500 lines across 5 phases  
**Purpose:** Copy-paste these prompts into Claude Code for instant code generation

---

## 📚 COMPLETE TABLE OF CONTENTS

### PHASE 1: FOUNDATION (Week 1-3) - 12,400 lines
- [P1.1] Visual Studio Solution Generator (15 projects, 5 min)
- [P1.2] Core Configuration System (1,500 lines)
- [P1.3] Logging System with NLog (2,000 lines)
- [P1.4] Revit Transaction Manager (3,600 lines)
- [P1.5] Helper Classes & Extensions (2,500 lines)
- [P1.6] Parameter Loader - 818 Parameters (3,500 lines)
- [P1.7] Schedule Loader - 146 Schedules (3,500 lines)
- [P1.8] Material Loader - 2,450+ Materials (3,500 lines)
- [P1.9] Formula Loader - 52 Formulas (3,500 lines)
- [P1.10] Standards Integration - NEC/ASHRAE/IPC (3,500 lines)

### PHASE 2: AUTOMATION (Week 4-9) - 28,200 lines
- [P2.1] Parameter Engine Core (5,200 lines)
- [P2.2] GPU Batch Processor - ILGPU (2,700 lines)
- [P2.3] ML.NET Parameter Classifier (3,700 lines)
- [P2.4] Multi-Model Sync Engine (3,600 lines)
- [P2.5] Parameter Manager WPF UI (2,600 lines)
- [P2.6] Schedule Generator Engine (4,200 lines)
- [P2.7] Material Auto-Assignment (3,800 lines)
- [P2.8] Formula Calculator Engine (5,200 lines)

### PHASE 3: GENIUS TAG (Week 10-14) - 19,800 lines
- [P3.1] Core Tagging Engine (7,200 lines)
- [P3.2] Learning System (4,800 lines)
- [P3.3] Advisory System (3,600 lines)
- [P3.4] Auto-Correction Engine (4,200 lines)

### PHASE 4: ADVANCED AI (Week 15-19) - 22,300 lines
- [P4.1] DWG Parser - netDXF (4,200 lines)
- [P4.2] AI Layer Classifier (3,500 lines)
- [P4.3] DWG-to-Revit Converter (4,500 lines)
- [P4.4] Image Vision System (2,300 lines)
- [P4.5] YOLOv9 Wall Detector (2,500 lines)
- [P4.6] SAM Segmentation (3,100 lines)
- [P4.7] OCR & Layout Analysis (4,100 lines)
- [P4.8] Floor Plan Reconstruction (4,900 lines)

### PHASE 5: UI & INTEGRATION (Week 20-22) - 43,800 lines
- [P5.1] Command Console (3,900 lines)
- [P5.2] Command System (500+ commands)
- [P5.3] Ribbon Interface (1,500 lines)
- [P5.4] Sheet Manager (2,200 lines)
- [P5.5] Analytics Dashboard (1,800 lines)

---

## 🔧 PHASE 2: AUTOMATION ENGINES (Continued)

### [P2.1] PARAMETER ENGINE CORE

**CRITICAL: This is the heart of parameter automation - copy entire prompt:**

```
Create the complete Parameter Engine for StingBIM with GPU acceleration and ML inference:

PROJECT: StingBIM.ParameterManager
NAMESPACE: StingBIM.ParameterManager.Engine
PERFORMANCE TARGET: 30,000+ elements/second

═══════════════════════════════════════════════════════════════════
REQUIREMENTS - MUST IMPLEMENT ALL
═══════════════════════════════════════════════════════════════════

1. CRUD OPERATIONS:
   ✓ Create parameters (single/batch)
   ✓ Read parameter values (single/batch)
   ✓ Update parameter values (single/batch)
   ✓ Delete parameters (single/batch)
   ✓ Parameter existence checks
   ✓ Type-safe parameter access

2. BATCH PROCESSING:
   ✓ Process 30,000+ elements/second
   ✓ GPU acceleration via ILGPU
   ✓ Multi-threaded CPU fallback
   ✓ Configurable batch sizes
   ✓ Progress reporting (IProgress<T>)
   ✓ Cancellation support (CancellationToken)

3. VALIDATION:
   ✓ Data type validation
   ✓ Value range validation
   ✓ Required parameter checks
   ✓ Format validation (email, URL, etc.)
   ✓ Custom validation rules
   ✓ Circular dependency detection

4. CACHING:
   ✓ In-memory parameter cache
   ✓ LRU eviction policy
   ✓ Configurable cache size (default 500MB)
   ✓ Thread-safe access
   ✓ Cache statistics

5. TRANSACTION MANAGEMENT:
   ✓ Automatic transaction wrapping
   ✓ Rollback on error
   ✓ Nested transaction support
   ✓ Transaction grouping

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (5,200 LINES TOTAL)
═══════════════════════════════════════════════════════════════════

1. ParameterEngine.cs (2,000 lines)
   
   PUBLIC API:
   
   // Single element operations
   void CreateParameter(Element element, string name, object value)
   T GetParameterValue<T>(Element element, string name)
   void SetParameterValue(Element element, string name, object value)
   void DeleteParameter(Element element, string name)
   bool ParameterExists(Element element, string name)
   
   // Batch operations (CPU)
   void CreateParameters(IEnumerable<Element> elements, string name, object value)
   Dictionary<ElementId, T> GetParameterValues<T>(IEnumerable<Element> elements, string name)
   void SetParameterValues(IEnumerable<Element> elements, string name, object value)
   void SetParameterValues(Dictionary<ElementId, Dictionary<string, object>> values)
   
   // GPU-accelerated batch operations
   void BatchUpdateGPU(Element[] elements, string paramName, float[] values)
   void BatchTransformGPU(Element[] elements, string paramName, Func<float, float> transform)
   
   // Async operations
   Task CreateParameterAsync(Element element, string name, object value, CancellationToken ct)
   Task<T> GetParameterValueAsync<T>(Element element, string name, CancellationToken ct)
   Task SetParameterValuesAsync(IEnumerable<Element> elements, string name, object value, 
                                  IProgress<int> progress, CancellationToken ct)
   
   // Advanced operations
   void CopyParameters(Element source, Element target, IEnumerable<string> parameterNames)
   void CopyParameters(Element source, IEnumerable<Element> targets, IEnumerable<string> parameterNames)
   ValidationResult ValidateParameter(Element element, string name, object value)
   
   PRIVATE METHODS:
   Parameter GetParameter(Element element, string name)
   void SetParameterInternal(Parameter param, object value)
   bool TryConvertValue(object value, ParameterType paramType, out object converted)
   void ProcessBatch(IEnumerable<Element> elements, Action<Element> operation, int batchSize)

2. ParameterCache.cs (800 lines)
   
   FEATURES:
   - Thread-safe ConcurrentDictionary
   - LRU eviction when cache exceeds limit
   - Separate caches for definitions and values
   - Cache warming on startup
   - Cache statistics tracking
   
   PUBLIC API:
   T GetValue<T>(ElementId elementId, string paramName)
   void SetValue(ElementId elementId, string paramName, object value)
   void Invalidate(ElementId elementId)
   void InvalidateAll()
   CacheStatistics GetStatistics()
   void SetCacheSize(int megabytes)
   
   CACHE STATISTICS:
   - HitCount
   - MissCount
   - EvictionCount
   - CacheSize (bytes)
   - HitRate (percentage)

3. ParameterValidator.cs (900 lines)
   
   VALIDATION TYPES:
   - Data type validation
   - Range validation (min/max)
   - Pattern validation (regex)
   - Custom validation functions
   - Required field validation
   - Format validation (email, URL, phone, etc.)
   
   PUBLIC API:
   ValidationResult Validate(Element element, string paramName, object value)
   bool ValidateDataType(object value, ParameterType expectedType)
   bool ValidateRange(object value, object min, object max)
   bool ValidatePattern(string value, string pattern)
   void AddCustomRule(string paramName, Func<object, ValidationResult> validator)
   void AddRequiredParameter(string paramName)
   
   VALIDATION RESULT:
   - IsValid (bool)
   - Errors (List<string>)
   - Warnings (List<string>)
   - ParameterName (string)
   - Value (object)

4. BatchProcessor.cs (1,200 lines)
   
   FEATURES:
   - Multi-threaded processing
   - Configurable thread count
   - Dynamic batch sizing
   - Progress reporting
   - Error handling (continue or stop)
   - Performance metrics
   
   PUBLIC API:
   void Process(IEnumerable<Element> elements, Action<Element> operation, 
                BatchOptions options = null)
   Task ProcessAsync(IEnumerable<Element> elements, Func<Element, Task> operation,
                      BatchOptions options, IProgress<BatchProgress> progress, CancellationToken ct)
   void ProcessParallel(IEnumerable<Element> elements, Action<Element> operation,
                        int maxDegreeOfParallelism = 8)
   
   BATCH OPTIONS:
   - BatchSize (default 1000)
   - MaxDegreeOfParallelism (default 8)
   - ContinueOnError (default false)
   - ReportInterval (default 100)
   - UseGPU (default true if available)
   
   BATCH PROGRESS:
   - ElementsProcessed
   - TotalElements
   - PercentComplete
   - ElementsPerSecond
   - EstimatedTimeRemaining
   - CurrentBatch
   - TotalBatches

5. ParameterEngineEventArgs.cs (300 lines)
   
   EVENTS:
   event EventHandler<ParameterCreatedEventArgs> ParameterCreated;
   event EventHandler<ParameterUpdatedEventArgs> ParameterUpdated;
   event EventHandler<ParameterDeletedEventArgs> ParameterDeleted;
   event EventHandler<BatchStartedEventArgs> BatchStarted;
   event EventHandler<BatchProgressEventArgs> BatchProgress;
   event EventHandler<BatchCompletedEventArgs> BatchCompleted;
   event EventHandler<BatchErrorEventArgs> BatchError;
   
   EVENT ARGS:
   - ParameterCreatedEventArgs (Element, ParameterName, Value, Timestamp)
   - ParameterUpdatedEventArgs (Element, ParameterName, OldValue, NewValue)
   - BatchStartedEventArgs (ElementCount, Operation, Timestamp)
   - BatchProgressEventArgs (Progress info)
   - BatchCompletedEventArgs (ElementsProcessed, Duration, Success)

═══════════════════════════════════════════════════════════════════
USAGE EXAMPLES - COPY THESE FOR TESTS
═══════════════════════════════════════════════════════════════════

EXAMPLE 1: Simple single element operation
```csharp
var engine = new ParameterEngine(document);

// Create parameter
engine.CreateParameter(wall, "Custom_Height", 3.5);

// Read parameter
double height = engine.GetParameterValue<double>(wall, "Custom_Height");

// Update parameter
engine.SetParameterValue(wall, "Custom_Height", 4.0);

// Check existence
if (engine.ParameterExists(wall, "Custom_Height"))
{
    // Delete parameter
    engine.DeleteParameter(wall, "Custom_Height");
}
```

EXAMPLE 2: Batch operation on 10,000 elements
```csharp
var walls = collector.OfClass(typeof(Wall)).ToElements();

// Update all walls at once (uses GPU if available)
engine.SetParameterValues(walls, "Fire_Rating", "2-Hour");

// Process took ~300ms for 10,000 elements
```

EXAMPLE 3: Async with progress reporting
```csharp
var progress = new Progress<int>(percent =>
{
    Console.WriteLine($"Progress: {percent}%");
});

await engine.SetParameterValuesAsync(
    elements,
    "Checked",
    true,
    progress,
    CancellationToken.None
);
```

EXAMPLE 4: Complex batch with validation
```csharp
var values = new Dictionary<ElementId, Dictionary<string, object>>();

foreach (var element in elements)
{
    values[element.Id] = new Dictionary<string, object>
    {
        ["Height"] = CalculateHeight(element),
        ["Volume"] = CalculateVolume(element),
        ["Cost"] = CalculateCost(element)
    };
}

// Validates all values before applying
engine.SetParameterValues(values);
```

EXAMPLE 5: GPU-accelerated calculation
```csharp
// Update 50,000 elements with GPU (completes in ~200ms)
var elements = collector.ToElementArray();
var heights = elements.Select(e => CalculateHeight(e)).ToArray();

engine.BatchUpdateGPU(elements, "Calculated_Height", heights);
// Falls back to CPU if GPU not available
```

═══════════════════════════════════════════════════════════════════
PERFORMANCE REQUIREMENTS - MUST PASS ALL BENCHMARKS
═══════════════════════════════════════════════════════════════════

BENCHMARK TESTS (use BenchmarkDotNet):

[Benchmark]
public void UpdateSingleElement()
{
    engine.SetParameterValue(element, "Test", 123);
    // Target: <1ms
}

[Benchmark]
public void Update1000Elements()
{
    engine.SetParameterValues(elements1000, "Test", 123);
    // Target: <100ms
}

[Benchmark]
public void Update10000Elements()
{
    engine.SetParameterValues(elements10000, "Test", 123);
    // Target: <500ms
}

[Benchmark]
public void Update30000ElementsGPU()
{
    engine.BatchUpdateGPU(elements30000, "Test", values30000);
    // Target: <1000ms (1 second)
}

[Benchmark]
public void Read10000Elements()
{
    var values = engine.GetParameterValues<int>(elements10000, "Test");
    // Target: <300ms
}

PERFORMANCE ASSERTIONS:
- Single element: <1ms
- Batch 1,000: <100ms  
- Batch 10,000: <500ms
- Batch 30,000 (GPU): <1,000ms
- Read 10,000: <300ms

═══════════════════════════════════════════════════════════════════
ERROR HANDLING - COMPREHENSIVE
═══════════════════════════════════════════════════════════════════

EXCEPTIONS TO THROW:

public class ParameterNotFoundException : Exception
{
    public Element Element { get; }
    public string ParameterName { get; }
}

public class InvalidParameterTypeException : Exception
{
    public string ParameterName { get; }
    public Type ExpectedType { get; }
    public Type ActualType { get; }
}

public class ParameterValidationException : Exception
{
    public ValidationResult ValidationResult { get; }
}

public class BatchProcessingException : Exception
{
    public int SuccessCount { get; }
    public int FailureCount { get; }
    public List<Exception> Errors { get; }
}

ERROR SCENARIOS:
- Element is null → ArgumentNullException
- Parameter doesn't exist → ParameterNotFoundException
- Wrong data type → InvalidParameterTypeException
- Validation fails → ParameterValidationException
- Batch partially fails → BatchProcessingException
- Transaction fails → TransactionException
- GPU not available → Log warning, use CPU

═══════════════════════════════════════════════════════════════════
LOGGING - USE LOGGER CLASS
═══════════════════════════════════════════════════════════════════

LOG ALL OPERATIONS:

Logger.Debug($"Creating parameter '{name}' on element {element.Id}");
Logger.Info($"Batch update: {elements.Count()} elements, parameter '{name}'");
Logger.Warn($"GPU not available, falling back to CPU for batch operation");
Logger.Error($"Failed to set parameter '{name}'", exception);
Logger.Performance("BatchUpdate", duration, new {
    ElementCount = elements.Count(),
    ParameterName = name,
    UseGPU = gpuUsed
});

═══════════════════════════════════════════════════════════════════
UNIT TESTS - COMPREHENSIVE COVERAGE (90%+)
═══════════════════════════════════════════════════════════════════

CREATE THESE TEST CLASSES:

1. ParameterEngineTests.cs (basic CRUD)
2. ParameterEngineBatchTests.cs (batch operations)
3. ParameterCacheTests.cs (caching)
4. ParameterValidatorTests.cs (validation)
5. BatchProcessorTests.cs (batch processing)
6. ParameterEnginePerformanceTests.cs (benchmarks)

SAMPLE TEST:

[Fact]
public async Task SetParameterValuesAsync_ShouldUpdateAllElements()
{
    // Arrange
    var elements = CreateTestElements(1000);
    var progress = new TestProgress();
    
    // Act
    await engine.SetParameterValuesAsync(
        elements, 
        "Test", 
        123,
        progress,
        CancellationToken.None
    );
    
    // Assert
    elements.Should().AllSatisfy(e => 
        engine.GetParameterValue<int>(e, "Test").Should().Be(123)
    );
    progress.ReportedValues.Should().HaveCount(10); // 10 progress reports
}

═══════════════════════════════════════════════════════════════════
TECH STACK
═══════════════════════════════════════════════════════════════════

REQUIRED NUGET PACKAGES:
- Autodesk.Revit.API (2024.0.0)
- System.Collections.Concurrent (for thread-safe cache)
- System.Reactive (6.0.0) - for event streaming
- BenchmarkDotNet (0.13.12) - for performance testing
- xUnit (2.6.4) - for unit testing
- FluentAssertions (6.12.0) - for test assertions
- Moq (4.20.70) - for mocking

═══════════════════════════════════════════════════════════════════
OUTPUT DELIVERABLES
═══════════════════════════════════════════════════════════════════

Provide complete, compilable C# code for:

1. ✓ ParameterEngine.cs (2,000 lines)
2. ✓ ParameterCache.cs (800 lines)  
3. ✓ ParameterValidator.cs (900 lines)
4. ✓ BatchProcessor.cs (1,200 lines)
5. ✓ ParameterEngineEventArgs.cs (300 lines)
6. ✓ All unit test files (1,500 lines)
7. ✓ Benchmark tests (300 lines)
8. ✓ XML documentation on all public members
9. ✓ README.md with usage examples

TOTAL OUTPUT: 5,200 lines of production-ready code

VERIFICATION:
- All code compiles without errors
- All tests pass (90%+ coverage)
- All benchmarks meet performance targets
- Full XML documentation
- No ReSharper warnings
```

**Expected Generation Time:** 60-90 seconds  
**Copy-Paste into:** Visual Studio 2022  
**Test Immediately:** Run all unit tests

---

### [P2.2] GPU BATCH PROCESSOR (ILGPU)

**Copy this entire prompt:**

```
Create GPU-accelerated batch processing engine using ILGPU:

PROJECT: StingBIM.ParameterManager
NAMESPACE: StingBIM.ParameterManager.Batch
PURPOSE: Process 30,000+ elements/second using GPU

═══════════════════════════════════════════════════════════════════
REQUIREMENTS
═══════════════════════════════════════════════════════════════════

1. GPU ACCELERATION:
   ✓ ILGPU 1.5.1 integration
   ✓ Automatic GPU detection
   ✓ CPU fallback if GPU unavailable
   ✓ Support NVIDIA, AMD, CPU

2. OPERATIONS:
   ✓ Batch parameter updates (numeric)
   ✓ Formula calculations
   ✓ Value transformations
   ✓ Aggregations (sum, avg, min, max)

3. PERFORMANCE:
   ✓ 30,000+ elements/second
   ✓ <1 second for 50,000 elements
   ✓ Memory efficient (stream large datasets)

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (2,700 LINES)
═══════════════════════════════════════════════════════════════════

1. GPUAccelerator.cs (1,500 lines)
   
   INITIALIZATION:
   Context Initialize()
   Accelerator GetAccelerator()
   bool IsGPUAvailable { get; }
   string AcceleratorType { get; } // "CUDA", "OpenCL", "CPU"
   
   BATCH OPERATIONS:
   void BatchUpdate(Element[] elements, string paramName, float[] values)
   void BatchTransform(Element[] elements, string paramName, Func<float, float> transform)
   float[] BatchCalculate(Element[] elements, string[] paramNames, Func<float[], float> formula)
   
   GPU KERNELS:
   static void MultiplyKernel(Index1D index, ArrayView<float> input, ArrayView<float> output, float factor)
   static void AddKernel(Index1D index, ArrayView<float> input, ArrayView<float> output, float value)
   static void FormulaKernel(Index1D index, ArrayView<float> input1, ArrayView<float> input2, ArrayView<float> output, int operation)
   static void TransformKernel(Index1D index, ArrayView<float> input, ArrayView<float> output, TransformFunction transform)

2. GPUMemoryManager.cs (600 lines)
   
   MEMORY MANAGEMENT:
   MemoryBuffer1D<T> AllocateBuffer<T>(int size)
   void CopyToDevice<T>(T[] data, MemoryBuffer1D<T> buffer)
   void CopyFromDevice<T>(MemoryBuffer1D<T> buffer, T[] data)
   void FreeBuffer(MemoryBuffer buffer)
   long GetAvailableMemory()

3. GPUKernels.cs (600 lines)
   
   CUDA KERNELS:
   - Arithmetic operations (add, subtract, multiply, divide)
   - Mathematical functions (sqrt, pow, abs, etc.)
   - Logical operations (and, or, not)
   - Comparison operations (>, <, ==, etc.)
   - Custom formula execution

═══════════════════════════════════════════════════════════════════
USAGE EXAMPLE
═══════════════════════════════════════════════════════════════════

```csharp
var gpu = new GPUAccelerator();

if (gpu.IsGPUAvailable)
{
    // Get parameter values from 50,000 walls
    var heights = walls.Select(w => GetHeight(w)).ToArray();
    
    // Multiply all heights by 1.1 on GPU
    gpu.BatchTransform(walls, "Height", h => h * 1.1f);
    
    // Completed in ~200ms vs 5 seconds on CPU
}
else
{
    Logger.Warn("GPU not available, using CPU fallback");
    // Falls back to multi-threaded CPU
}
```

═══════════════════════════════════════════════════════════════════
PERFORMANCE REQUIREMENTS
═══════════════════════════════════════════════════════════════════

BENCHMARKS:
- 10,000 elements: <100ms (GPU), <500ms (CPU)
- 30,000 elements: <300ms (GPU), <1,500ms (CPU)
- 50,000 elements: <500ms (GPU), <2,500ms (CPU)

MEMORY:
- Maximum 2GB GPU memory usage
- Stream data for large datasets (>100K elements)
- Automatic cleanup

═══════════════════════════════════════════════════════════════════
TECH STACK
═══════════════════════════════════════════════════════════════════

NUGET:
- ILGPU (1.5.1)
- ILGPU.Algorithms (1.5.1)

OUTPUT:
Provide complete C# code for all 3 files + unit tests + benchmarks.
```

---

### [P2.3] ML.NET PARAMETER CLASSIFIER

**Copy this entire prompt:**

```
Create AI-powered parameter classification using ML.NET:

PROJECT: StingBIM.ParameterManager
NAMESPACE: StingBIM.ParameterManager.Inference
PURPOSE: 90%+ accuracy on parameter suggestions

═══════════════════════════════════════════════════════════════════
ML MODELS TO CREATE
═══════════════════════════════════════════════════════════════════

1. PARAMETER CLASSIFIER (Multi-class)
   - Input: Element context (category, type, family name)
   - Output: Suggested parameters (top 5)
   - Training: 818 parameters × 50 categories = 40,900 samples
   - Algorithm: SDCA (Stochastic Dual Coordinate Ascent)
   - Accuracy Target: 90%+

2. PARAMETER VALUE PREDICTOR (Regression)
   - Input: Element properties + parameter name
   - Output: Predicted value
   - Training: 50,000 samples
   - Algorithm: FastTree
   - R² Target: >0.85

3. CATEGORY PREDICTOR (Binary Classification)
   - Input: Element features
   - Output: Applicable categories
   - Training: 10,730 category bindings
   - Algorithm: LightGBM
   - Accuracy Target: 95%+

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (3,700 LINES)
═══════════════════════════════════════════════════════════════════

1. ParameterClassifier.cs (1,500 lines)
   
   METHODS:
   List<ParameterSuggestion> SuggestParameters(Element element, int top = 5)
   bool IsParameterApplicable(Element element, string parameterName)
   float GetConfidence(Element element, string parameterName)
   void Train(IEnumerable<TrainingSample> samples)
   void SaveModel(string path)
   void LoadModel(string path)

2. MLModel.cs (1,200 lines)
   
   FEATURE EXTRACTION:
   - Element category
   - Element type name
   - Family name
   - Built-in parameters
   - Existing custom parameters
   - Discipline (Architecture, Structure, MEP)

3. ModelTrainer.cs (1,000 lines)
   
   TRAINING PIPELINE:
   - Data preparation
   - Feature engineering
   - Model training
   - Cross-validation
   - Hyperparameter tuning
   - Model evaluation

═══════════════════════════════════════════════════════════════════
TRAINING DATA GENERATION
═══════════════════════════════════════════════════════════════════

```csharp
// Generate training data from MR_PARAMETERS.txt + CATEGORY_BINDINGS.csv
var trainer = new ModelTrainer();

// Load parameters and bindings
var parameters = ParameterLoader.LoadAll(); // 818 parameters
var bindings = CategoryBindings.LoadAll(); // 10,730 bindings

// Generate samples
var samples = trainer.GenerateTrainingSamples(parameters, bindings);
// 818 params × 50 categories = 40,900 samples

// Train model
trainer.Train(samples);
trainer.Evaluate(); // Should show >90% accuracy
trainer.SaveModel("parameter-classifier.zip");
```

═══════════════════════════════════════════════════════════════════
USAGE EXAMPLE
═══════════════════════════════════════════════════════════════════

```csharp
var classifier = new ParameterClassifier();
classifier.LoadModel("parameter-classifier.zip");

// Get suggestions for a wall
var suggestions = classifier.SuggestParameters(wall, top: 5);

foreach (var suggestion in suggestions)
{
    Console.WriteLine($"{suggestion.ParameterName} ({suggestion.Confidence:P})");
    // Output:
    // BLE_WALL_THICKNESS_MM (95.2%)
    // BLE_WALL_HEIGHT_MM (92.8%)
    // BLE_WALL_TYPE_CLASSIFICATION_TXT (89.3%)
    // BLE_WALL_FINISH_TXT (85.7%)
    // BLE_WALL_FUNCTION_TXT (82.1%)
}
```

═══════════════════════════════════════════════════════════════════
ACCURACY REQUIREMENTS
═══════════════════════════════════════════════════════════════════

METRICS:
- Overall Accuracy: >90%
- Top-5 Accuracy: >95%
- Precision: >88%
- Recall: >85%
- F1 Score: >86%

CROSS-VALIDATION:
- 5-fold cross-validation
- Stratified sampling
- Report avg ± std dev

═══════════════════════════════════════════════════════════════════
TECH STACK
═══════════════════════════════════════════════════════════════════

NUGET:
- Microsoft.ML (3.0.0)
- Microsoft.ML.FastTree (3.0.0)
- Microsoft.ML.LightGbm (3.0.0)

OUTPUT:
Complete C# code for all 3 files + training script + model evaluation + unit tests.
```

---

## 🎯 PHASE 3: GENIUS TAG SYSTEM

### [P3.1] GENIUS TAG CORE ENGINE

**Copy this entire prompt to Claude Code:**

```
Create the intelligent tagging engine - the revolutionary feature of StingBIM:

PROJECT: StingBIM.GeniusTag
NAMESPACE: StingBIM.GeniusTag.Core
PURPOSE: <500ms per tag, <100ms collision detection, 85%+ quality

═══════════════════════════════════════════════════════════════════
CORE ALGORITHMS
═══════════════════════════════════════════════════════════════════

1. TAG PLACEMENT (K-Nearest Neighbors)
   - Find optimal tag position
   - Avoid overlaps with existing tags
   - Minimize leader length
   - Respect view boundaries
   - Consider readability

2. COLLISION DETECTION (Quadtree)
   - Spatial indexing for O(log n) queries
   - Detect tag-tag collisions
   - Detect tag-element collisions
   - <100ms for 1,000 tags

3. LEADER ROUTING (A* Algorithm)
   - Find shortest obstacle-free path
   - Avoid crossing other leaders
   - Minimize bends
   - Orthogonal or curved leaders

4. QUALITY SCORING (Machine Learning)
   - Predict tag quality before placement
   - Score: position, readability, leader length
   - 0-100 scale (>80 = good, <60 = poor)

═══════════════════════════════════════════════════════════════════
FILES TO CREATE (7,200 LINES)
═══════════════════════════════════════════════════════════════════

1. IntelligentTagger.cs (2,000 lines)
   
   PUBLIC API:
   TagResult PlaceTag(Element element, View view, TagConfiguration config = null)
   List<TagResult> PlaceTags(IEnumerable<Element> elements, View view, IProgress<int> progress = null)
   TagResult RelocateTag(Tag tag, XYZ newPosition)
   void AutoCorrectTag(Tag tag)
   TagQuality PredictQuality(Element element, XYZ proposedPosition, View view)
   
   FEATURES:
   - Intelligent position selection
   - Automatic collision avoidance
   - Leader optimization
   - Quality prediction
   - User correction learning

2. TagPlacementEngine.cs (1,500 lines)
   
   PLACEMENT STRATEGIES:
   - Above element (default)
   - Below element
   - Left of element
   - Right of element
   - Nearest clear space
   - Custom algorithm (extensible)
   
   METHODS:
   XYZ FindOptimalPosition(Element element, View view, TagConfiguration config)
   List<XYZ> GenerateCandidatePositions(Element element, View view, int count = 20)
   XYZ SelectBestPosition(List<XYZ> candidates, Element element, View view)

3. CollisionDetector.cs (1,200 lines)
   
   QUADTREE IMPLEMENTATION:
   class QuadTree
   {
       void Insert(BoundingBox tagBounds, Tag tag)
       List<Tag> Query(BoundingBox region)
       void Remove(Tag tag)
       void Clear()
   }
   
   COLLISION DETECTION:
   bool HasCollision(XYZ position, BoundingBox tagBounds, View view)
   List<Tag> GetCollidingTags(XYZ position, BoundingBox tagBounds, View view)
   XYZ FindNearestClearSpace(XYZ startPosition, BoundingBox tagBounds, View view)
   
   PERFORMANCE:
   - Insert: O(log n)
   - Query: O(log n)
   - Total for 1,000 tags: <100ms

4. LeaderRouter.cs (1,000 lines)
   
   A* PATHFINDING:
   List<XYZ> RoutLeader(XYZ tagPosition, XYZ elementPosition, View view)
   float CalculateLeaderCost(List<XYZ> path)
   bool IsPathClear(XYZ from, XYZ to, View view)
   List<XYZ> SimplifyPath(List<XYZ> path) // Remove unnecessary bends
   
   LEADER STYLES:
   - Straight
   - Orthogonal (90° bends only)
   - Curved (spline)
   - Custom

5. QualityAnalyzer.cs (700 lines)
   
   QUALITY METRICS:
   - Position quality (0-100)
   - Readability score (0-100)
   - Leader quality (0-100)
   - Overlap penalty
   - Distance from element
   
   MACHINE LEARNING:
   float PredictQuality(TagPlacementContext context)
   void TrainModel(List<UserCorrection> corrections)
   void UpdateModel(UserCorrection correction)

6. TagConfiguration.cs (200 lines)
   
   SETTINGS:
   - Preferred direction (Above, Below, Left, Right)
   - Minimum distance from element
   - Maximum leader length
   - Leader style
   - Tag type
   - Text size
   - Allow overlaps (bool)

7. TagResult.cs (600 lines)
   
   RESULT DATA:
   - Tag (IndependentTag)
   - Position (XYZ)
   - Leader path (List<XYZ>)
   - Quality score (0-100)
   - Collision count
   - Processing time
   - Success (bool)
   - Error message

═══════════════════════════════════════════════════════════════════
USAGE EXAMPLES
═══════════════════════════════════════════════════════════════════

EXAMPLE 1: Tag single element
```csharp
var tagger = new IntelligentTagger(document);

var result = tagger.PlaceTag(wall, view);

if (result.Success)
{
    Console.WriteLine($"Tag placed with quality {result.QualityScore}");
    Console.WriteLine($"Processing time: {result.ProcessingTime.TotalMilliseconds}ms");
}
```

EXAMPLE 2: Tag 1,000 elements with progress
```csharp
var progress = new Progress<int>(p => Console.WriteLine($"{p}% complete"));

var results = tagger.PlaceTags(elements, view, progress);

var avgQuality = results.Average(r => r.QualityScore);
var avgTime = results.Average(r => r.ProcessingTime.TotalMilliseconds);

Console.WriteLine($"Average quality: {avgQuality:F1}");
Console.WriteLine($"Average time: {avgTime:F1}ms per tag");
// Target: >85 quality, <500ms per tag
```

EXAMPLE 3: Pre-check quality before placing
```csharp
var proposedPosition = new XYZ(10, 20, 0);

var quality = tagger.PredictQuality(element, proposedPosition, view);

if (quality.Score > 80)
{
    // Good position, proceed
    var result = tagger.PlaceTag(element, view);
}
else
{
    // Poor position, warn user
    Console.WriteLine($"Warning: Low quality ({quality.Score}). {quality.Issues}");
}
```

EXAMPLE 4: Custom configuration
```csharp
var config = new TagConfiguration
{
    PreferredDirection = TagDirection.Above,
    MinimumDistance = 5.0, // feet
    MaximumLeaderLength = 20.0, // feet
    LeaderStyle = LeaderStyle.Orthogonal,
    AllowOverlaps = false
};

var result = tagger.PlaceTag(wall, view, config);
```

═══════════════════════════════════════════════════════════════════
PERFORMANCE REQUIREMENTS (CRITICAL)
═══════════════════════════════════════════════════════════════════

BENCHMARKS:

[Benchmark]
public void PlaceSingleTag()
{
    var result = tagger.PlaceTag(wall, view);
    // Target: <500ms
}

[Benchmark]
public void CollisionDetection1000Tags()
{
    quadtree.Insert(boundingBox, tag);
    var collisions = quadtree.Query(region);
    // Target: <100ms for 1,000 tags
}

[Benchmark]
public void RouteLeaderAstar()
{
    var path = router.RouteLeader(tagPos, elemPos, view);
    // Target: <50ms
}

[Benchmark]
public void Tag1000Elements()
{
    var results = tagger.PlaceTags(elements1000, view);
    // Target: <10 seconds (avg 10ms/tag)
}

PERFORMANCE TARGETS:
- Single tag: <500ms
- Collision detection (1,000 tags): <100ms
- Leader routing: <50ms
- 1,000 elements: <10 seconds

QUALITY TARGETS:
- Average quality score: >85
- Good tags (>80 score): >90%
- Poor tags (<60 score): <5%

═══════════════════════════════════════════════════════════════════
ALGORITHMS IMPLEMENTATION
═══════════════════════════════════════════════════════════════════

K-NEAREST NEIGHBORS (Tag Placement):
```csharp
private List<XYZ> GenerateCandidatePositions(Element element, View view, int count)
{
    var elementBounds = element.GetBoundingBox(view);
    var center = GetCenter(elementBounds);
    
    var candidates = new List<XYZ>();
    
    // Generate positions in a circle around element
    for (int i = 0; i < count; i++)
    {
        double angle = (2 * Math.PI * i) / count;
        double distance = config.MinimumDistance;
        
        var candidate = new XYZ(
            center.X + distance * Math.Cos(angle),
            center.Y + distance * Math.Sin(angle),
            center.Z
        );
        
        candidates.Add(candidate);
    }
    
    return candidates;
}
```

QUADTREE (Collision Detection):
```csharp
class QuadTreeNode
{
    BoundingBox Bounds { get; set; }
    List<Tag> Tags { get; set; }
    QuadTreeNode[] Children { get; set; } // 4 children
    
    public void Insert(BoundingBox tagBounds, Tag tag)
    {
        // O(log n) insertion
        if (!Bounds.Contains(tagBounds))
            return;
            
        if (Tags.Count < MaxTagsPerNode && Children == null)
        {
            Tags.Add(tag);
        }
        else
        {
            if (Children == null)
                Subdivide();
                
            foreach (var child in Children)
                child.Insert(tagBounds, tag);
        }
    }
}
```

A* PATHFINDING (Leader Routing):
```csharp
public List<XYZ> RouteLeader(XYZ start, XYZ goal, View view)
{
    var openSet = new PriorityQueue<Node>();
    var cameFrom = new Dictionary<XYZ, XYZ>();
    
    openSet.Enqueue(new Node(start, 0, Heuristic(start, goal)));
    
    while (openSet.Count > 0)
    {
        var current = openSet.Dequeue();
        
        if (current.Position.IsAlmostEqualTo(goal))
            return ReconstructPath(cameFrom, current.Position);
            
        foreach (var neighbor in GetNeighbors(current.Position))
        {
            if (!IsPathClear(current.Position, neighbor, view))
                continue;
                
            var tentativeScore = current.GScore + Distance(current.Position, neighbor);
            
            if (tentativeScore < GetGScore(neighbor))
            {
                cameFrom[neighbor] = current.Position;
                openSet.Enqueue(new Node(neighbor, tentativeScore, Heuristic(neighbor, goal)));
            }
        }
    }
    
    return new List<XYZ>(); // No path found
}
```

═══════════════════════════════════════════════════════════════════
MACHINE LEARNING (Quality Prediction)
═══════════════════════════════════════════════════════════════════

FEATURES:
- Distance from element
- Number of collisions
- Leader length
- Leader bends
- View congestion
- Tag size
- Element category

ML MODEL:
```csharp
var mlContext = new MLContext();

var pipeline = mlContext.Transforms
    .Concatenate("Features", 
        "DistanceFromElement",
        "CollisionCount",
        "LeaderLength",
        "LeaderBends",
        "ViewCongestion")
    .Append(mlContext.Regression.Trainers.FastTree(
        labelColumnName: "QualityScore",
        featureColumnName: "Features"
    ));

var model = pipeline.Fit(trainingData);
```

═══════════════════════════════════════════════════════════════════
TESTING
═══════════════════════════════════════════════════════════════════

UNIT TESTS:
- Test all placement strategies
- Test collision detection (accuracy)
- Test A* pathfinding (shortest path)
- Test quality scoring (predictions match reality)
- Test performance (all benchmarks pass)

INTEGRATION TESTS:
- Tag 1,000 elements in real Revit project
- Verify no overlaps
- Verify all tags readable
- Measure average quality
- Measure processing time

═══════════════════════════════════════════════════════════════════
TECH STACK
═══════════════════════════════════════════════════════════════════

NUGET:
- Autodesk.Revit.API (2024.0.0)
- Microsoft.ML (3.0.0) - for quality prediction
- MathNet.Numerics (5.0.0) - for geometry calculations
- BenchmarkDotNet (0.13.12) - for performance testing

═══════════════════════════════════════════════════════════════════
OUTPUT DELIVERABLES
═══════════════════════════════════════════════════════════════════

Provide complete C# code for:

1. ✓ IntelligentTagger.cs (2,000 lines)
2. ✓ TagPlacementEngine.cs (1,500 lines)
3. ✓ CollisionDetector.cs (1,200 lines) with Quadtree
4. ✓ LeaderRouter.cs (1,000 lines) with A* implementation
5. ✓ QualityAnalyzer.cs (700 lines) with ML.NET
6. ✓ TagConfiguration.cs (200 lines)
7. ✓ TagResult.cs (600 lines)
8. ✓ Unit tests (1,500 lines)
9. ✓ Benchmark tests (400 lines)
10. ✓ Integration tests (600 lines)

TOTAL: 7,200 lines + 2,500 test lines

VERIFICATION CHECKLIST:
□ All code compiles
□ All unit tests pass (>95% coverage)
□ All benchmarks pass performance targets
□ QuadTree correctly detects collisions
□ A* finds optimal paths
□ ML model predicts quality >85% accuracy
□ Integration test tags 1,000 elements successfully
□ Average quality score >85
□ Average processing time <500ms per tag
```

**This is THE revolutionary feature. Take time to get it right!**

---

I'll continue with the remaining phases. This prompt library is becoming comprehensive! Should I:

1. Continue with Phase 3 (Learning System, Advisory, Corrective)
2. Continue with Phase 4 (DWG Converter, Image-to-BIM)
3. Continue with Phase 5 (UI & Integration)
4. Create all remaining prompts in one go

What would be most valuable?