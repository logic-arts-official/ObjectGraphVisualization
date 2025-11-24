# Developer Guide - Object Graph Visualizer

This guide helps developers get up and running with OGV development quickly.

## Table of Contents

- [Quick Setup](#quick-setup)
- [Development Environment](#development-environment)
- [Architecture Overview](#architecture-overview)
- [Building and Running](#building-and-running)
- [Development Workflow](#development-workflow)
- [Key Components](#key-components)
- [Debugging](#debugging)
- [Common Tasks](#common-tasks)
- [Troubleshooting](#troubleshooting)

## Quick Setup

**Goal**: Get from checkout to running application in under 5 minutes.

### Prerequisites Check

```bash
# Check Java version (need Java 17+; this is the minimum required for this project)
java -version

# Check Maven version (need 3.6+)
mvn -version

# If missing, install:
# Java: https://adoptium.net/
# Maven: https://maven.apache.org/download.cgi
```

### Get Running

```bash
# 1. Clone and enter directory
git clone https://github.com/logic-arts-official/ObjectGraphVisualization.git
cd ObjectGraphVisualization

# 2. Install local dependencies (first time only)
mvn validate

# 3. Build and run
mvn clean package && java -jar target/ogv-*-runnable.jar
```

**That's it!** You should see the OGV application window open.

## Development Environment

### Recommended IDE Setup

#### IntelliJ IDEA (Recommended)

1. **Open Project**:
   - `File > Open` → Select `pom.xml`
   - Let IntelliJ import the Maven project

2. **Configure JDK**:
   - `File > Project Structure > Project`
   - Set SDK to Java 17 or higher

3. **Run Configuration**:
   - `Run > Edit Configurations > + > Application`
   - Name: "OGV Main"
   - Main class: `ch.hsr.ogv.Main`
   - Module: `ogv`
   - Save and click Run

4. **Useful Plugins**:
   - **Maven Helper**: Better Maven integration
   - **JavaFX Runtime**: JavaFX development support

#### Eclipse

1. **Import Project**:
   - `File > Import > Maven > Existing Maven Projects`
   - Select the repository directory

2. **Set JDK**:
   - Right-click project → `Properties`
   - `Java Build Path > Libraries`
   - Ensure JDK 17+ is configured

3. **Run**:
   - Right-click `Main.java`
   - `Run As > Java Application`

#### VS Code

1. **Install Extensions**:
   - Extension Pack for Java
   - Maven for Java

2. **Open Folder**:
   - `File > Open Folder` → Select repository

3. **Run**:
   - Open `Main.java`
   - Click `Run` above the `main` method

### Version Control

```bash
# Configure Git (first time)
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Create feature branch
git checkout -b feature/my-new-feature

# Stage and commit changes
git add .
git commit -m "feat: add new feature"

# Push to your fork
git push origin feature/my-new-feature
```

## Architecture Overview

OGV follows a **Model-View-Controller (MVC)** architecture:

```
┌─────────────────────────────────────────────┐
│              View Layer                      │
│  (JavaFX UI + 3D Rendering)                 │
│  - SubScenes (Class/Object/Relation)        │
│  - FXML Controllers                         │
└─────────────┬───────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────────┐
│           Controller Layer                   │
│  (Business Logic)                           │
│  - ViewController                           │
│  - SelectionManager                         │
└─────────────┬───────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────────┐
│             Model Layer                      │
│  (Domain Objects)                           │
│  - ClassBox, ObjectBox                      │
│  - Relations                                │
│  - Attributes                               │
└─────────────┬───────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────────┐
│          Data Access Layer                   │
│  - Persistence (Save/Load)                  │
│  - XMI Import                               │
└─────────────────────────────────────────────┘
```

### Package Structure

```
ch.hsr.ogv/
├── controller/     # Controllers and business logic
│   ├── ViewController.java
│   └── ...
├── dataaccess/     # File I/O and XMI parsing
│   ├── Persistence.java
│   └── XMI_1_1.java
├── model/          # Domain models
│   ├── ModelClass.java
│   ├── ModelObject.java
│   └── ...
├── util/           # Utilities
│   ├── GeometryUtil.java
│   └── ...
├── view/           # UI and 3D visualization
│   ├── Arrow.java
│   ├── ClassBox.java
│   └── ...
└── Main.java       # Application entry point
```

## Building and Running

### Maven Lifecycle

```bash
# Clean build artifacts
mvn clean

# Compile source code
mvn compile

# Run tests
mvn test

# Package into JAR
mvn package

# Install to local Maven repo
mvn install

# Full clean build with tests
mvn clean install
```

### Build Profiles

Currently, OGV uses a single build configuration. The pom.xml includes dependencies for all platforms (Windows, Linux, macOS).

### Running from Command Line

```bash
# Quick run during development
mvn compile exec:java

# Run packaged JAR
java -jar target/ogv-*-runnable.jar

# Run with more memory (for large diagrams)
java -Xmx2048m -jar target/ogv-*-runnable.jar

# Run with JavaFX verbose logging
java -Djavafx.verbose=true -jar target/ogv-*-runnable.jar
```

## Development Workflow

### Typical Development Cycle

1. **Create branch** for your feature/fix
2. **Write code** in small, focused commits
3. **Test locally** after each change
4. **Run full test suite** before pushing
5. **Push to your fork**
6. **Create Pull Request**

### Making Changes

#### Adding a New Feature

1. **Identify** where the feature fits (Model/View/Controller)
2. **Create** new classes if needed
3. **Update** existing classes to integrate
4. **Add tests** for new functionality
5. **Update documentation** if user-facing

#### Fixing a Bug

1. **Reproduce** the bug
2. **Write a failing test** that demonstrates the bug
3. **Fix** the bug
4. **Verify** the test now passes
5. **Check** for similar issues elsewhere

### Code Style

OGV follows standard Java conventions:
- **Indentation**: 4 spaces (no tabs)
- **Line length**: ~120 characters max
- **Braces**: Opening brace on same line
- **Naming**: See [CONTRIBUTING.md](CONTRIBUTING.md) for details

## Key Components

### Model Layer

**ModelClass** (`ch.hsr.ogv.model.ModelClass`):
- Represents a UML class
- Contains attributes, methods
- Manages relationships to other classes

**ModelObject** (`ch.hsr.ogv.model.ModelObject`):
- Represents an instance of a class
- Contains attribute values
- Links to object relations

### View Layer

**ClassBox** (`ch.hsr.ogv.view.ClassBox`):
- 3D visual representation of ModelClass
- Handles rendering and user interaction
- Updates when model changes

**Arrow** (`ch.hsr.ogv.view.Arrow`):
- Visual representation of relationships
- Dynamically updates position
- Different styles for different relation types

### Controller Layer

**ViewController** (`ch.hsr.ogv.controller.ViewController`):
- Central controller for the application
- Manages view state and user interactions
- Coordinates between Model and View

**ModelViewConnector**:
- Synchronizes Model and View
- Observer pattern implementation
- **Extension Point**: Add API hooks here

## Debugging

### Enabling Debug Logging

Edit `src/main/resources/log4j2.xml`:

```xml
<Configuration status="DEBUG">
  <Loggers>
    <Root level="DEBUG">  <!-- Change from INFO to DEBUG -->
      <AppenderRef ref="Console"/>
    </Root>
  </Loggers>
</Configuration>
```

### Common Debugging Scenarios

#### UI Not Updating

Check that changes are on JavaFX Application Thread:

```java
Platform.runLater(() -> {
    // UI update code here
});
```

#### 3D Rendering Issues

Enable JavaFX verbose output:
```bash
java -Dprism.verbose=true -jar target/ogv-*-runnable.jar
```

#### Memory Issues

Monitor with:
```bash
java -XX:+PrintGCDetails -Xmx1024m -jar target/ogv-*-runnable.jar
```

### IDE Debugging

Set breakpoints in:
- `ViewController` methods for user interaction
- `ModelClass`/`ModelObject` for data changes
- `ClassBox`/`Arrow` for rendering issues

## Common Tasks

### Adding a New Relation Type

1. **Model**: Add enum to `RelationType`
2. **View**: Add rendering logic to `Arrow`
3. **UI**: Add menu option to create relation
4. **Persistence**: Update save/load logic

### Adding Menu Item

1. **FXML**: Edit `MainStage.fxml`
2. **Controller**: Add handler method in controller
3. **Wire**: Use `fx:id` to connect FXML to code

### Importing New File Format

1. **Parser**: Create new class in `dataaccess` package
2. **Implement**: Parse format to Model objects
3. **Integrate**: Add to File menu
4. **Test**: Use example files

### Exporting to New Format

1. **Exporter**: Create class to convert Model to format
2. **Implement**: Export logic
3. **UI**: Add to File > Export menu
4. **Test**: Verify round-trip if applicable

## Troubleshooting

### Build Issues

**Problem**: Maven can't find local dependencies
```bash
# Solution: Re-install local JARs
mvn validate
```

**Problem**: Compilation errors with JavaFX
```bash
# Solution: Ensure Java 17+ is active
java -version

# Check Maven is using correct Java
mvn -version
```

### Runtime Issues

**Problem**: Application won't start
```bash
# Check JavaFX is available
java --list-modules | grep javafx

# If missing, verify pom.xml JavaFX dependencies
```

**Problem**: 3D rendering not working
- Update graphics drivers
- Try software rendering: `-Dprism.order=sw`

**Problem**: OutOfMemoryError
```bash
# Increase heap size
java -Xmx2048m -jar target/ogv-*-runnable.jar
```

### IDE Issues

**IntelliJ: "Cannot resolve symbol"**
1. `File > Invalidate Caches > Invalidate and Restart`
2. `Maven > Reimport`

**Eclipse: "Project configuration is not up-to-date"**
1. Right-click project
2. `Maven > Update Project`

**VS Code: JavaFX classes not recognized**
1. Check Extension Pack for Java is installed
2. Run `Java: Clean Language Server Workspace`

## Getting Help

- **Documentation**: Check this guide first
- **Code Comments**: Many classes have detailed JavaDoc
- **Issues**: Search [GitHub Issues](https://github.com/logic-arts-official/ObjectGraphVisualization/issues)
- **Contributing**: See [CONTRIBUTING.md](CONTRIBUTING.md)

## Next Steps

1. **Explore the code**: Start with `Main.java` and follow the execution
2. **Run examples**: Open `.ogv` files from `examples/` directory
3. **Make a small change**: Try adding a log statement or button
4. **Pick an issue**: Look for "good first issue" labels

Happy coding! 🚀
