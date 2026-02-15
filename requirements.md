# Requirements Document: TantuAI - The Generative Loom Interface

## Introduction

TantuAI (from Sanskrit "tantu" meaning thread/fiber) is a dual-interface generative AI system that bridges modern digital design with traditional Indian handloom weaving mechanics. The system translates between two worlds: the aesthetic language of fashion designers ("vintage monsoon vibe") and the technical precision of master weavers (hook counts, reed numbers, warp/weft density). By integrating a Multi-Modal Large Language Model with physics-based validation and rendering, TantuAI enables the creation of physically weaveable designs while preserving and democratizing India's rich textile heritage.

The system addresses three critical problems:
1. **The Language Barrier**: Designers and weavers speak different languages
2. **The Visualization Gap**: Standard AI generates beautiful but unweavable patterns
3. **Loss of Heritage**: Traditional motifs exist only in aging weavers' memories or decaying paper graphs

## Glossary

- **TantuAI**: The complete dual-interface generative AI system for handloom pattern creation
- **Visionary_Mode**: Natural language interface for designers using aesthetic prompts
- **Master_Weaver_Mode**: Technical specification interface for precise loom instructions
- **Pattern_Converter**: Component that transforms AI-generated images into grid-based weaving patterns
- **Constraint_Validator**: Component that verifies patterns meet weaving technical requirements (also called "Physics Validator")
- **Loom_Logic_Transformer**: AI model trained on point paper designs with constraint awareness
- **Gharana_Module**: Region-specific weaving style module (Banarasi, Ikat, Jamdani, etc.)
- **Weaving_Pattern**: A grid-based representation of a textile design with thread-level specifications
- **Point_Paper_Design**: Technical graph showing the binary lifting plan for a loom
- **Thread_Count**: The number of warp and weft threads per unit measurement
- **Warp_Thread**: Vertical threads held in tension on a loom
- **Weft_Thread**: Horizontal threads woven through warp threads
- **EPI**: Ends Per Inch - warp thread density
- **PPI**: Picks Per Inch - weft thread density
- **Ikat**: A dyeing technique where threads are resist-dyed before weaving
- **Jamdani**: A fine muslin weaving technique with supplementary weft patterns (discontinuous weft)
- **Brocade**: A richly decorative shuttle-woven fabric with raised patterns (continuous supplementary weft)
- **Banarasi**: Weaving style from Varanasi characterized by heavy silk, dense Zari coverage
- **Zari**: Metallic thread (gold or silver) used in traditional Indian textiles
- **Kanchipuram**: South Indian silk weaving style with distinct borders and pallus
- **Color_Palette**: The set of thread colors available for a specific weaving project
- **Structural_Integrity**: The physical stability and durability of a woven textile
- **Weave_Structure**: The interlacement pattern of warp and weft threads (plain, twill, satin, etc.)
- **Draft_Pattern**: Technical notation showing how threads interlace in weaving
- **Reed_Count**: The number of dents (spaces) per unit in the reed that spaces warp threads
- **Pick_Count**: The number of weft threads per unit measurement
- **Float**: A portion of thread that passes over or under multiple perpendicular threads without interlacing
- **Float_Length**: The number of threads a float passes over, measured in thread count
- **Maximum_Safe_Float**: The longest float length that maintains structural integrity for a given thread type and thickness
- **Binding_Point**: An interlacement point inserted to secure long floats and prevent snagging
- **Shuttle_Capacity**: The maximum number of different colored threads that can be carried simultaneously in a shuttle or weaving mechanism
- **Unweavable_Pattern**: A design that violates physical loom constraints and cannot be manufactured
- **Hook_Count**: Number of hooks in a Jacquard loom mechanism (determines pattern complexity)
- **Lifting_Plan**: The sequence of warp thread lifts that creates the weaving pattern
- **WIF**: Weaving Information File - standard format for weaving drafts
- **Motif_Library**: Digital repository of traditional weaving motifs and patterns
- **Drape_Simulation**: Physics-based rendering showing how fabric hangs and moves
- **Digital_Twin**: Virtual representation of the final woven textile before physical production

## Requirements

### Requirement 1: Dual-Mode Interface

**User Story:** As a user of TantuAI, I want to interact with the system in a way that matches my expertise level, so that designers can use natural language while weavers can use precise technical specifications.

#### Acceptance Criteria

1. THE TantuAI SHALL provide two distinct operational modes: Visionary_Mode and Master_Weaver_Mode
2. WHEN a user selects Visionary_Mode, THE TantuAI SHALL accept natural language prompts describing aesthetic qualities, cultural references, and design intent
3. WHEN a user selects Master_Weaver_Mode, THE TantuAI SHALL accept structured technical specifications including hook count, thread types, densities, and weave structures
4. WHEN switching between modes, THE TantuAI SHALL preserve the underlying pattern data and allow users to view the same design through different interfaces
5. THE TantuAI SHALL translate between natural language descriptions and technical parameters bidirectionally

### Requirement 2: Natural Language Pattern Generation (Visionary Mode)

**User Story:** As a fashion designer, I want to describe textile designs using cultural references and aesthetic language, so that I can create patterns without knowing technical weaving terminology.

#### Acceptance Criteria

1. WHEN a user enters a natural language prompt, THE TantuAI SHALL parse cultural context, style references, color descriptions, and motif requests
2. WHEN the prompt references specific Indian textile traditions (Kanchipuram, Banarasi, Patola), THE TantuAI SHALL apply appropriate style constraints and characteristics
3. WHEN the prompt includes mood or theme descriptors, THE TantuAI SHALL translate these into concrete design parameters (color palettes, pattern density, motif selection)
4. THE TantuAI SHALL convert natural language prompts into structured JSON parameter files containing motif, style, warp_density, weft_density, colors, and technique specifications
5. WHEN ambiguous prompts are received, THE TantuAI SHALL ask clarifying questions to refine the design intent

### Requirement 3: Technical Specification Input (Master Weaver Mode)

**User Story:** As a master weaver, I want to specify exact loom parameters and thread specifications, so that I can generate patterns that precisely match my equipment capabilities and material inventory.

#### Acceptance Criteria

1. WHEN a user enters Master_Weaver_Mode, THE TantuAI SHALL provide structured input fields for Hook_Count, thread types, denier specifications, EPI, PPI, and Weave_Structure
2. THE TantuAI SHALL accept thread specifications including fiber type (silk, cotton, art silk), ply count, and denier measurements
3. WHEN a user specifies a Hook_Count, THE TantuAI SHALL constrain pattern complexity to match the loom's mechanical capabilities
4. THE TantuAI SHALL validate that specified EPI and PPI values are compatible with the selected thread types and reed configuration
5. WHEN generating patterns in Master_Weaver_Mode, THE TantuAI SHALL produce binary Lifting_Plans that directly map to loom operations

### Requirement 4: AI Design Input Processing

**User Story:** As a textile designer, I want to input generative AI-created designs or reference images into the system, so that I can explore converting digital art into weavable patterns.

#### Acceptance Criteria

1. WHEN a user uploads a generative AI image file, THE TantuAI SHALL accept common image formats (PNG, JPEG, SVG, TIFF)
2. WHEN an image is uploaded, THE TantuAI SHALL extract and analyze the design's color palette, complexity, and structural elements
3. WHEN the image resolution exceeds system limits, THE TantuAI SHALL provide options to scale or crop the design
4. WHEN an image contains transparency, THE TantuAI SHALL handle alpha channels appropriately for weaving context

### Requirement 5: Grid-Based Pattern Conversion with Loom Logic

**User Story:** As a weaving technician, I want AI designs converted to grid-based patterns using loom-aware logic, so that they align with the fundamental structure of handloom weaving and respect physical constraints.

#### Acceptance Criteria

1. WHEN converting an AI design, THE Loom_Logic_Transformer SHALL transform the continuous image into a discrete grid representation based on Point_Paper_Design principles
2. WHEN specifying grid dimensions, THE Pattern_Converter SHALL accept custom thread count specifications for warp and weft
3. WHEN performing grid conversion, THE Loom_Logic_Transformer SHALL preserve the visual essence and key features of the original design
4. WHEN the design contains curves, THE Loom_Logic_Transformer SHALL apply anti-aliasing to convert curves into step-patterns that a loom can execute
5. WHEN the design contains gradients or continuous tones, THE Pattern_Converter SHALL apply appropriate dithering or color quantization techniques
6. THE Pattern_Converter SHALL generate output with thread-level precision matching standard handloom capabilities (minimum 20 threads per inch, maximum 200 threads per inch)
7. THE Loom_Logic_Transformer SHALL be trained on Point_Paper_Designs rather than photographs of finished textiles

### Requirement 6: Color Constraint Management

**User Story:** As a production manager, I want to limit patterns to available thread colors, so that designs can be manufactured with existing inventory.

#### Acceptance Criteria

1. WHEN a user defines a Color_Palette, THE TantuAI SHALL accept thread color specifications with standard color models (RGB, CMYK, Pantone, or custom thread codes)
2. WHEN converting a design, THE Pattern_Converter SHALL map all colors in the AI output to the nearest available colors in the defined Color_Palette
3. WHEN the Color_Palette contains fewer colors than the original design, THE Pattern_Converter SHALL apply color reduction while maintaining visual fidelity
4. WHEN color mapping is complete, THE TantuAI SHALL provide a color usage report showing thread quantities needed for each color
5. WHERE a user specifies maximum color count, THE Pattern_Converter SHALL limit the output pattern to that number of distinct colors

### Requirement 7: Region-Specific Weaving Styles (Gharana Modules)

**User Story:** As a textile heritage specialist, I want the system to understand and apply region-specific Indian weaving traditions, so that generated patterns respect cultural authenticity and technical characteristics of different weaving clusters.

#### Acceptance Criteria

1. THE TantuAI SHALL provide Gharana_Modules for major Indian weaving traditions: Banarasi, Kanchipuram, Ikat/Patola, Jamdani, and Chanderi
2. WHEN a user selects the Banarasi_Module, THE TantuAI SHALL prioritize continuous supplementary weft (brocade) patterns and dense Zari coverage characteristic of Varanasi weaving
3. WHEN a user selects the Ikat_Module, THE TantuAI SHALL simulate the characteristic "blur" of pre-dyed yarns and align patterns to grids that mimic the resist-dyeing and tying process
4. WHEN a user selects the Jamdani_Module, THE TantuAI SHALL generate patterns with discontinuous supplementary weft where motifs float independently like embroidery
5. WHEN a user selects the Kanchipuram_Module, THE TantuAI SHALL apply design constraints for heavy silk, distinct borders, contrasting pallus, and temple-inspired motifs
6. WHEN a Gharana_Module is active, THE TantuAI SHALL enforce region-specific constraints on thread types, color palettes, and structural techniques
7. THE TantuAI SHALL allow users to blend characteristics from multiple Gharana_Modules for contemporary fusion designs

### Requirement 8: Traditional Motif Library and Cultural Preservation

**User Story:** As a heritage conservationist, I want to digitize and preserve traditional weaving motifs, so that rare and dying patterns are not lost and can be remixed for contemporary designs.

#### Acceptance Criteria

1. THE TantuAI SHALL maintain a Motif_Library containing digitized traditional Indian textile motifs (Annapakshi, Rudraksha, temple architecture, floral patterns, geometric designs)
2. WHEN users upload historical pattern graphs or photographs, THE TantuAI SHALL digitize them into the Motif_Library with metadata about origin, region, and technique
3. WHEN a user references a traditional motif by name in a prompt, THE TantuAI SHALL retrieve the authentic pattern from the Motif_Library
4. THE TantuAI SHALL allow users to search the Motif_Library by region, technique, cultural significance, or visual similarity
5. WHEN generating new patterns, THE TantuAI SHALL offer to incorporate traditional motifs while allowing contemporary reinterpretation
6. THE Motif_Library SHALL store both the visual representation and the technical Point_Paper_Design for each motif
7. THE TantuAI SHALL track motif provenance, including the master weaver or community that contributed the pattern

### Requirement 9: Unweavable Design Detection

**User Story:** As a textile designer, I want the system to detect unweavable designs early in the conversion process, so that I don't waste time refining patterns that cannot be physically manufactured.

#### Acceptance Criteria

1. WHEN an AI design is first uploaded, THE TantuAI SHALL perform a preliminary weavability analysis before detailed conversion
2. WHEN the preliminary analysis detects fundamental unweavability issues, THE TantuAI SHALL alert the user with specific reasons why the design cannot be woven
3. THE Constraint_Validator SHALL maintain a database of Maximum_Safe_Float values for common thread types (cotton, silk, wool, synthetic)
4. WHEN analyzing a pattern, THE Constraint_Validator SHALL identify all floats and measure their Float_Length against Maximum_Safe_Float thresholds
5. IF the design requires more colors in a single row than the specified Shuttle_Capacity, THEN THE TantuAI SHALL flag this as an Unweavable_Pattern
6. WHEN an Unweavable_Pattern is detected, THE TantuAI SHALL provide alternative suggestions such as color reduction, pattern simplification, or technique changes
7. THE TantuAI SHALL distinguish between "impossible to weave" (violates physics) and "difficult to weave" (requires advanced skill or equipment)
8. WHEN a pattern is validated as weavable, THE TantuAI SHALL provide a weavability score indicating manufacturing difficulty

### Requirement 10: Structural Integrity Validation with Automatic Correction

**User Story:** As a quality control specialist, I want patterns validated for structural integrity with automatic corrections, so that the resulting textile will be durable and manufacturable without thread breakage or snagging.

#### Acceptance Criteria

1. WHEN a pattern is generated, THE Constraint_Validator SHALL verify that the Weave_Structure maintains fabric stability
2. WHEN analyzing a pattern, THE Constraint_Validator SHALL identify areas where thread interlacement may cause structural weakness
3. IF a pattern contains long floats exceeding the maximum safe float length for the thread type, THEN THE Constraint_Validator SHALL automatically insert Binding_Points to secure the structure
4. WHEN long floats are detected, THE Constraint_Validator SHALL calculate the exact float length and compare it against thread-specific safety thresholds
5. WHEN Binding_Points are inserted, THE TantuAI SHALL minimize visual impact on the design while ensuring structural safety
6. THE Constraint_Validator SHALL verify that warp and weft thread densities are compatible and within manufacturable ranges
7. IF a pattern requires more simultaneous thread colors than the specified shuttle capacity, THEN THE Constraint_Validator SHALL flag this as a manufacturing constraint violation
8. WHEN validating patterns, THE Constraint_Validator SHALL check for thread tension imbalances that could cause fabric distortion or loom jamming

### Requirement 11: Physics-Based Rendering and Drape Simulation

**User Story:** As a textile designer, I want to see a photorealistic simulation of how the fabric will look and drape, so that I can evaluate the final product before physical production.

#### Acceptance Criteria

1. WHEN a pattern is converted, THE TantuAI SHALL generate a Digital_Twin with photorealistic rendering of the woven textile
2. WHEN rendering Zari threads, THE TantuAI SHALL simulate specular reflection characteristic of metallic threads
3. WHEN rendering silk threads, THE TantuAI SHALL simulate anisotropic reflection showing directional sheen
4. WHEN rendering cotton threads, THE TantuAI SHALL simulate diffuse reflection with appropriate matte appearance
5. THE TantuAI SHALL calculate and display thread thickness variations showing the characteristic unevenness of handloom versus power loom
6. WHEN displaying Drape_Simulation, THE TantuAI SHALL show how the fabric hangs, folds, and moves based on thread types, densities, and weave structure
7. THE TantuAI SHALL provide interactive 3D visualization allowing users to rotate and examine the fabric from different angles
8. WHEN light conditions are adjusted, THE TantuAI SHALL update the rendering to show how the fabric appears under different lighting

### Requirement 12: Draft Pattern Generation

**User Story:** As a loom operator, I want technical draft patterns generated from the converted design, so that I can set up and operate the handloom correctly.

#### Acceptance Criteria

1. WHEN a weaving pattern is finalized, THE TantuAI SHALL generate a complete Draft_Pattern with threading, tie-up, and treadling sequences
2. WHEN generating drafts, THE TantuAI SHALL produce output in standard weaving notation formats
3. THE TantuAI SHALL calculate and display Reed_Count and Pick_Count specifications for the pattern
4. WHEN the draft is complex, THE TantuAI SHALL provide sectional views and detailed instructions for loom setup
5. THE TantuAI SHALL generate a thread color sequence chart showing the order and position of colored threads in warp and weft

### Requirement 13: Pattern Preview and Comparison

**User Story:** As a textile designer, I want to preview and compare the converted pattern with the original design, so that I can make adjustments before production.

#### Acceptance Criteria

1. WHEN a pattern is converted, THE TantuAI SHALL generate a realistic visual simulation of the woven textile
2. THE TantuAI SHALL provide side-by-side comparison views of the original AI design and the converted weaving pattern
3. WHEN a user modifies pattern parameters, THE TantuAI SHALL update the preview in real-time or near-real-time
4. THE TantuAI SHALL allow users to zoom into thread-level detail in the preview
5. THE TantuAI SHALL highlight areas where the converted pattern differs significantly from the original design

### Requirement 14: Constraint Feedback and Iteration

**User Story:** As a textile designer, I want clear feedback on constraint violations, so that I can iteratively refine the design to meet manufacturing requirements.

#### Acceptance Criteria

1. WHEN the Constraint_Validator identifies issues, THE TantuAI SHALL provide specific, actionable feedback describing each constraint violation
2. WHEN displaying constraint violations, THE TantuAI SHALL highlight the affected areas in the pattern visualization
3. THE TantuAI SHALL categorize constraint violations by severity (critical, warning, suggestion)
4. WHEN a user requests suggestions, THE TantuAI SHALL propose specific modifications to resolve constraint violations
5. THE TantuAI SHALL maintain a history of pattern iterations, allowing users to compare versions and revert changes

### Requirement 15: Export and Integration

**User Story:** As a production coordinator, I want to export finalized patterns in industry-standard formats, so that they can be used with existing weaving tools and documentation systems.

#### Acceptance Criteria

1. WHEN a pattern is finalized, THE TantuAI SHALL export patterns in WIF (Weaving Information File) format
2. THE TantuAI SHALL export patterns as PDF documents with complete technical specifications and visual representations
3. THE TantuAI SHALL export thread color lists in CSV format with color codes, quantities, and positions
4. WHERE digital jacquard looms are used, THE TantuAI SHALL export patterns in jacquard-compatible formats
5. WHEN exporting, THE TantuAI SHALL include metadata about the original AI design, conversion parameters, and validation results

### Requirement 16: Thread Count and Density Optimization

**User Story:** As a production planner, I want the system to optimize thread counts and densities, so that patterns are manufacturable within equipment capabilities and cost constraints.

#### Acceptance Criteria

1. WHEN a user specifies target thread density ranges, THE Pattern_Converter SHALL optimize the grid resolution to match these specifications
2. WHEN thread density affects pattern detail, THE TantuAI SHALL provide trade-off analysis showing detail loss versus manufacturability
3. THE Constraint_Validator SHALL verify that specified thread counts are achievable with standard reed sizes and loom configurations
4. WHEN optimizing thread density, THE Pattern_Converter SHALL maintain aspect ratio and proportions of the original design
5. THE TantuAI SHALL calculate estimated production time based on thread counts and pattern complexity

### Requirement 17: Multi-Layer Pattern Support

**User Story:** As an advanced textile designer, I want to work with multi-layer weaving patterns, so that I can create complex textiles with depth and dimensional effects.

#### Acceptance Criteria

1. WHERE multi-layer weaving is specified, THE Pattern_Converter SHALL generate separate layer patterns with interlacement specifications
2. WHEN creating multi-layer patterns, THE Constraint_Validator SHALL verify that layers are structurally connected and stable
3. THE TantuAI SHALL support up to 4 independent weaving layers
4. WHEN generating multi-layer drafts, THE TantuAI SHALL provide layer-specific threading and treadling sequences
5. THE TantuAI SHALL calculate total thread requirements across all layers

### Requirement 18: Pattern Scaling and Repetition

**User Story:** As a textile designer, I want to define pattern repeats and scaling, so that small AI-generated motifs can be arranged into larger textile designs.

#### Acceptance Criteria

1. WHEN a user specifies repeat parameters, THE Pattern_Converter SHALL tile the converted pattern horizontally and vertically
2. THE TantuAI SHALL support mirror repeats, half-drop repeats, and brick repeats
3. WHEN creating repeats, THE Pattern_Converter SHALL ensure seamless transitions at pattern boundaries
4. THE TantuAI SHALL allow independent scaling of warp and weft dimensions while maintaining weave structure
5. WHEN scaling patterns, THE TantuAI SHALL recalculate thread counts and update all technical specifications accordingly
