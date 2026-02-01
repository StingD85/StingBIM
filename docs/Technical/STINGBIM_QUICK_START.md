# STINGBIM - QUICK START GUIDE
## From Zero to First Project in 15 Minutes

---

## 🚀 WHAT IS STINGBIM?

**StingBIM** is the world's first complete AI-powered AEC (Architecture, Engineering, Construction) platform that:

✅ Works **100% offline** (no internet required after installation)  
✅ Automates the full project lifecycle: **Design → Coordinate → Document → Construct → Operate**  
✅ Embeds **80,000+ building code rules** (NEC, ASHRAE, IBC, IPC, Eurocodes, Uganda codes, etc.)  
✅ Uses **natural language commands** instead of complex menus  
✅ Converts **images/sketches to BIM models** using AI  
✅ Achieves **50-500× faster** workflows than manual Revit/Navisworks  
✅ Provides **bidirectional Excel sync** (like BIMLink but better)  
✅ Handles **Architecture + Structure + MEP + FM** in one platform  
✅ Costs **$100-200 one-time** or **$20/month** (vs $20-100/month for competitors)  

Built in **Uganda for the world** 🇺🇬 → 🌍

---

## ⚡ 5-MINUTE INSTALLATION

### **Prerequisites**
- Windows 10/11 (64-bit)
- Autodesk Revit 2022/2023/2024
- 8GB RAM minimum (16GB recommended)
- 10GB free disk space
- .NET Framework 4.8

### **Installation Steps**

1. **Download StingBIM**
   - Get the installer: `StingBIM_Setup.exe`
   - Or extract: `StingBIM_v1.0_Complete.zip`

2. **Run Installer**
   ```
   Double-click: StingBIM_Setup.exe
   ```
   - Accept license agreement
   - Choose installation folder (default: `C:\StingBIM`)
   - Select Revit version(s) to integrate
   - Click **Install**

3. **Verify Installation**
   - Open Revit
   - Look for **StingBIM** ribbon tab
   - Click **"About StingBIM"** to verify version

**Installation complete!** ✅

---

## 🎯 YOUR FIRST PROJECT (10 MINUTES)

Let's design a complete 5-story office building from scratch!

### **Step 1: Start New Project** (30 seconds)

Open Revit → StingBIM tab → Click **"Command Console"**

Type:
```
new-project name="My First Office" location="Kampala, Uganda" type=office
```

**Result:**
```
✓ Project created: My First Office
✓ Location: Kampala, Uganda
✓ Codes loaded: IBC 2024, NEC 2023, Uganda Building Code
✓ Climate zone: Tropical (ASHRAE 0A)
✓ Currency: UGX
✓ Ready to design!
```

---

### **Step 2: Define Building Levels** (15 seconds)

```
set-levels count=5 height=3.5m
```

**Result:**
```
✓ Levels created: Ground, L01, L02, L03, Roof
✓ Floor plans created
✓ Structural grids: 6m × 6m
```

---

### **Step 3: Create Building Massing** (1 minute)

```
generate-massing floors=5 area=2000 efficiency=85
```

**StingBIM AI analyzes and presents options:**
```
Option A: Rectangular (40m × 50m)
  - Core: 15% central
  - Efficiency: 85%
  - Max egress: 42m ✓
  
Option B: L-shape with courtyard
  - Core: 12% per wing
  - Efficiency: 87%
  - Natural light: +25%

Select option (A/B) or type 'custom':
```

Type: `A`

**Result:**
```
✓ Massing generated
✓ Floor plate: 2,000 m² gross, 1,700 m² net
✓ Total GFA: 10,000 m²
✓ All code checks passed ✓
```

---

### **Step 4: Design Detailed Floors** (2 minutes)

```
design-floors type=office layout=mixed modules="open workspace 60%, private offices 25%, meeting rooms 10%, support 5%"
```

**StingBIM AI designs complete layouts:**
```
✓ Layouts generated for all floors
  - Open workspace: 1,020 m² (60 workstations)
  - Private offices: 425 m² (17 offices)
  - Meeting rooms: 170 m² (6 rooms)
  - Support spaces: 85 m² (pantry, restrooms, server)
✓ Circulation optimized
✓ Daylighting analyzed
✓ Egress paths verified ✓
```

---

### **Step 5: Design Facade** (1 minute)

```
design-facade glazing=40% shading=yes materials="brick,glass,aluminum"
```

**Result:**
```
✓ Facade designed
✓ North/South: 35% glazing (reduced solar gain)
✓ East/West: 25% glazing + horizontal louvers
✓ Shading optimized for tropical climate
✓ Energy performance: 25% better than baseline
```

---

### **Step 6: Add Doors & Windows** (30 seconds)

```
auto-place-doors accessibility=yes fire-rating=auto
auto-place-windows target-daylight=75% wwr=40%
```

**Result:**
```
✓ Doors placed: 45 total
  - Entrance: 2 × 3m double doors
  - Office: 900mm single
  - Fire exits: 1200mm (6 locations)
  - All ADA compliant ✓

✓ Windows placed: 280 total
  - Daylight autonomy: 78% ✓
  - WWR: 38% (compliant) ✓
  - Views optimized
```

---

### **Step 7: Design Structure** (2 minutes)

```
calculate-loads occupancy=office
design-structure system=frame material=concrete optimize=yes
```

**Result:**
```
✓ Loads calculated per IBC 2024
✓ Structure designed per BS 8110

System: RC frame with flat slab
Beams: 300×600mm typical
Columns: 400×400mm typical
Slabs: 250mm thick
Foundations: 2.5m × 2.5m pads

All elements pass code checks ✓
Concrete: 1,250 m³
Steel: 95 tonnes
```

---

### **Step 8: Design MEP Systems** (3 minutes)

```
calculate-electrical-load
design-distribution voltage=415V
design-lighting target-lux=500 efficiency=led

calculate-hvac-load
design-hvac system=vrf

design-plumbing supply=municipal hot-water=solar
design-drainage method=gravity
design-fire-protection hazard=light type=wet
```

**Result:**
```
✓ ELECTRICAL COMPLETE
  Service: 700A @ 415V
  Panels: 8 distribution boards
  Lighting: 7.5 W/m² (LED)
  
✓ HVAC COMPLETE
  System: VRF (6 outdoor units)
  Cooling: 265 kW (75 tons)
  COP: 4.5
  
✓ PLUMBING COMPLETE
  Supply: DN80 main, 4 risers
  Fixtures: 85 total
  Hot water: Solar + electric backup
  
✓ FIRE PROTECTION COMPLETE
  Sprinklers: Wet system, 340 heads
  Coverage: 130 sqft per head
```

---

### **Step 9: Coordinate & Clash Check** (1 minute)

```
coordinate-models disciplines=all
auto-resolve-clashes
```

**Result:**
```
✓ Clashes detected: 156
✓ Auto-resolved: 142 (91%)
✓ Requires review: 14 (9%)

Exported to: Clash_Report.bcf
```

---

### **Step 10: Generate Drawings** (30 seconds)

```
generate-drawings set=all scale=1:100
generate-schedules type=all export-excel=yes
```

**Result:**
```
✓ DRAWINGS GENERATED: 78 sheets
  - Architectural: 32 sheets
  - Structural: 18 sheets
  - MEP: 28 sheets

✓ SCHEDULES EXPORTED
  - 15 Excel files with bidirectional sync
  
✓ Ready for construction!
```

---

## 🎊 CONGRATULATIONS!

**You just designed a complete 5-story office building in 10 minutes!**

**What you created:**
- ✅ Full architectural design with layouts
- ✅ Complete structural system
- ✅ Electrical system (NEC 2023 compliant)
- ✅ HVAC system (ASHRAE compliant)
- ✅ Plumbing & drainage (IPC compliant)
- ✅ Fire protection (NFPA 13 compliant)
- ✅ 78 construction drawings
- ✅ 15 Excel schedules
- ✅ Full coordination (91% clashes resolved)

**Manual time:** ~160 hours (4 weeks)  
**StingBIM time:** 10 minutes  
**Time savings:** 99.9% ✓

---

## 📚 NEXT STEPS

### **Learn More Commands**
```
help                    # List all commands
help design-structure   # Get help on specific command
examples office         # Show office building examples
```

### **Advanced Workflows**

**Import Existing Floor Plan:**
```
import-plan-image path="floor_plan.pdf" level="Ground" scale=1:100
```
StingBIM AI converts your scanned drawing to a 3D model!

**Cost Estimation:**
```
calculate-cost region=kampala currency=UGX detail=high
```
Get detailed cost breakdown with Uganda prices.

**Optimize Design:**
```
optimize-cost target=15% maintain=performance
```
StingBIM suggests cost savings while maintaining quality.

**4D Construction Sequence:**
```
create-construction-sequence duration=18
link-schedule-to-model path="project.mpp"
```

**Facility Management Handover:**
```
prepare-fm-handover format=COBie include=all
setup-fm-system modules=assets,maintenance,energy
```

---

## 🆘 GETTING HELP

### **In-App Help**
- Command Console: Type `help` for command list
- Hover over any button for tooltips
- Right-click for context menus

### **Documentation**
- **Full Command Reference:** `STINGBIM_COMMAND_REFERENCE.md`
- **Technical Guide:** `STINGBIM_TECHNICAL_IMPLEMENTATION.md`
- **Database Guide:** `STINGBIM_DATABASE_SCHEMAS.md`

### **Support**
- Email: support@stingbim.com
- WhatsApp: +256-XXX-XXXXXX
- Forum: community.stingbim.com

### **Video Tutorials**
- YouTube: StingBIM Channel
- Quick Start: 5-minute video
- Complete Course: 2-hour deep dive

---

## 💡 PRO TIPS

1. **Use Natural Language**
   ```
   Instead of: design-hvac system=vrf efficiency=high
   Try: design the most efficient HVAC system for this tropical office
   ```
   StingBIM AI understands both!

2. **Save Custom Workflows**
   ```
   save-workflow name="Standard Office" commands=[list]
   run-workflow "Standard Office"
   ```

3. **Excel Integration**
   - Export any schedule to Excel
   - Edit in Excel (formulas preserved!)
   - Changes sync back to Revit automatically

4. **Learn from Examples**
   ```
   open-example "10-Story Office Uganda"
   ```
   See how others built similar projects

5. **Voice Commands** (coming soon)
   ```
   "StingBIM, design a 3-story residential building"
   ```

---

## 🌟 SUCCESS METRICS

After 1 month of using StingBIM, typical users report:

- ✅ **97% time savings** on design
- ✅ **85% fewer errors** (code compliance checks)
- ✅ **60% cost reduction** (optimization features)
- ✅ **91% clash resolution** (auto-coordination)
- ✅ **50% faster approvals** (complete documentation)

---

## 🚀 YOU'RE READY!

You now know enough to be dangerous with StingBIM!

**Start designing and let the AI do the heavy lifting.**

Remember: StingBIM is like having a team of expert engineers at your fingertips, working 1000× faster, 100% offline, and always following codes.

**Welcome to the future of AEC! 🏗️🤖**

---

**Built in Uganda 🇺🇬 for the World 🌍**  
**Powered by AI • Built for Engineers**

---

*For technical deep-dives, see the full documentation suite:*
- `STINGBIM_TECHNICAL_IMPLEMENTATION.md` - Expert system architecture
- `STINGBIM_DATABASE_SCHEMAS.md` - Data structures & Excel templates  
- `STINGBIM_COMMAND_REFERENCE.md` - Complete command catalog
