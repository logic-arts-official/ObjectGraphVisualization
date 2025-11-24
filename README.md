# Object Graph Visualizer v3.2

![Object Graph Visualizer Logo](https://github.com/Nurtak/ObjectGraphVisualization/blob/master/src/main/resources/images/OGV.png?raw=true)

## Table of Contents
- [Description](#description)
- [Features](#features)
- [Quick Start for Developers](#quick-start-for-developers)
- [Installation](#installation)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [Building from Source](#building-from-source)
- [Pros and Cons](#pros-and-cons)
- [Backlog and Roadmap](#backlog-and-roadmap)
- [Contributing](#contributing)
- [License](#license)

## Description

Object Graph Visualizer (OGV) is an educational tool designed primarily for Computer Science courses to help students understand Object-Oriented Programming (OOP) paradigms and design patterns. 

The application provides **3D visualization** of both class diagrams and object diagrams:
- **Classes** are displayed in the XZ-plane as UML class diagrams
- **Objects** are instantiated directly above their classes along the Y-axis as object diagrams
- Classes and objects can be connected with various UML relationships (Associations, Compositions, Generalization, etc.)

OGV bridges the gap between theoretical OOP concepts and their practical implementation, making it an invaluable resource for educators and students alike.

### Developer Note
The architecture supports adding an API for remote application control, enabling real-time visualization and debugging of running programs. See `ModelViewConnector` class for integration points. **Contributions are welcome!**

## Features

### Educational Features
- **3D Visualization**: Interactive 3D rendering of class and object diagrams
- **Real-time Editing**: Add, edit, and remove classes, objects, relations, attributes, and values on the fly
- **Object Graph Mode**: Visualize complete object graphs with all relationships
- **Inheritance Simulation**: Support for virtual multiple inheritance patterns

### UML Support
- **Class Diagrams**: Full UML class diagram creation with attributes, methods, and visibility
- **Object Diagrams**: Create object instances with actual values
- **Relationships**: 
  - Associations (undirected, directed, bidirected)
  - Aggregations
  - Compositions
  - Dependencies
  - Generalization/Inheritance
- **Multiplicities and Roles**: Define cardinalities and role names for relationships

### Data Management
- **Save/Load Projects**: Persist your work in OGV's native format
- **XMI Import**: Import UML models from Enterprise Architect (XMI v1.1 format)
- **Customization**: Choose colors for classes, objects, relations, and background

### Technical Features
- **Cross-platform**: Runs on Windows, macOS, and Linux
- **Modern Runtime**: Java 17 with JavaFX 21 LTS
- **Free Camera**: Rotational camera placement for optimal viewing angles

## Quick Start for Developers

Get up and running in minutes:

```bash
# Prerequisites: Java 17+, Maven 3.6+

# 1. Clone the repository
git clone https://github.com/logic-arts-official/ObjectGraphVisualization.git
cd ObjectGraphVisualization

# 2. Build the project
mvn clean package

# 3. Run the application
java -jar target/ogv-3.2.0-runnable.jar
```

For detailed developer documentation, see [DEVELOPER_GUIDE.md](DEVELOPER_GUIDE.md).

## Installation

### Option 1: Pre-built Release (Recommended for Users)
Download the latest release from the [Releases page](https://github.com/Nurtak/ObjectGraphVisualization/releases).

- **Windows Installer**: Comes with bundled Java runtime
- **Windows Standalone**: Comes with bundled Java runtime
- **JAR File (All Platforms)**: Requires Java 17 or higher

### Option 2: Build from Source (Developers)
See [Building from Source](#building-from-source) section below.

## Usage

### Starting the Application

#### From Pre-built JAR:
```bash
java -jar ogv-3.2.0-runnable.jar
```

#### From IDE:
Run the `ch.hsr.ogv.Main` class as a Java application.

### Basic Workflow

1. **Create Classes**: Use the toolbar to add UML classes to your diagram
2. **Define Attributes**: Add attributes with types and visibility modifiers
3. **Add Relationships**: Connect classes with associations, compositions, or inheritance
4. **Instantiate Objects**: Create object instances from your classes
5. **Set Values**: Assign values to object attributes
6. **Visualize**: Rotate the camera to view your object graph from different angles
7. **Save**: Save your work in OGV format for later editing

### Importing from Enterprise Architect

1. Export your EA model as XMI 1.1
2. In OGV, use `File > Import > XMI 1.1`
3. Select your exported `.xml` file

For detailed instructions, refer to the [Instruction Manual](https://github.com/Nurtak/ObjectGraphVisualization/releases/download/v3.1/Instruction.Manual.pdf).

## Screenshots

![Screenshot 1: Class Diagram View](https://a.fsdn.com/con/app/proj/ogvisualizer/screenshots/screenshot1.PNG)
*Example of a class diagram with multiple relationships*

![Screenshot 2: Object Diagram View](https://a.fsdn.com/con/app/proj/ogvisualizer/screenshots/screenshot2.PNG)
*Object instances visualized above their classes*

![Screenshot 3: 3D Object Graph](https://a.fsdn.com/con/app/proj/ogvisualizer/screenshots/screenshot3.PNG)
*Complete object graph in 3D space*

## Building from Source

### Prerequisites

- **Java Development Kit (JDK)**: Version 17 or higher
  - Download from [Adoptium](https://adoptium.net/) or [Oracle](https://www.oracle.com/java/technologies/downloads/)
- **Apache Maven**: Version 3.6.3 or higher
  - Download from [Maven Downloads](https://maven.apache.org/download.cgi)

### Build Steps

```bash
# Clone the repository
git clone https://github.com/logic-arts-official/ObjectGraphVisualization.git
cd ObjectGraphVisualization

# Install local dependencies (required first-time only)
mvn validate

# Compile the project
mvn compile

# Run tests
mvn test

# Create runnable JAR with all dependencies
mvn package

# The runnable JAR will be at:
# target/ogv-3.2.0-runnable.jar
```

### Running Tests

```bash
# Run all tests
mvn test

# Run tests with coverage
mvn clean test jacoco:report
```

### IDE Setup

#### IntelliJ IDEA
1. Open IntelliJ IDEA
2. Select `File > Open` and choose the `pom.xml` file
3. Wait for Maven to import dependencies
4. Right-click `ch.hsr.ogv.Main` and select `Run 'Main.main()'`

#### Eclipse
1. Open Eclipse
2. Select `File > Import > Maven > Existing Maven Projects`
3. Browse to the repository directory
4. Select the project and click Finish
5. Right-click the project, select `Run As > Java Application`
6. Choose `Main - ch.hsr.ogv` as the main class

#### VS Code
1. Open VS Code
2. Install the "Extension Pack for Java" extension
3. Open the repository folder
4. Maven will automatically detect the project
5. Use the Run button or `F5` to start debugging

## Pros and Cons

### Advantages ✅

- **Educational Value**: Excellent tool for teaching OOP concepts with immediate visual feedback
- **3D Visualization**: Unique 3D approach helps students understand spatial relationships between objects
- **Cross-platform**: Works on all major operating systems
- **Open Source**: Free to use and modify under MIT license
- **XMI Import**: Integrates with professional tools like Enterprise Architect
- **Active Development**: Modern dependencies and ongoing maintenance
- **Low System Requirements**: Runs on modest hardware

### Current Limitations ⚠️

- **Learning Curve**: Initial setup and understanding the 3D interface may take time
- **XMI Support**: Limited to XMI 1.1 format (older Enterprise Architect versions)
- **No Export**: Currently doesn't export to standard UML formats (only native format)
- **Manual Layout**: Automatic layout algorithms not yet implemented
- **No Code Generation**: Cannot generate source code from diagrams
- **Limited Undo/Redo**: Undo functionality is basic
- **Documentation**: Could benefit from more tutorials and examples

## Backlog and Roadmap

### Planned Features 🚀

#### High Priority
- [ ] **API for Remote Control**: Enable integration with live applications for runtime visualization
- [ ] **Modern XMI Support**: Add support for XMI 2.x formats
- [ ] **Enhanced Undo/Redo**: Implement comprehensive undo/redo functionality
- [ ] **Auto-layout Algorithms**: Automatic arrangement of classes and objects
- [ ] **Export to Standard Formats**: PNG, SVG, PDF, and standard XMI export

#### Medium Priority
- [ ] **Code Generation**: Generate skeleton code (Java, C++, Python) from class diagrams
- [ ] **Reverse Engineering**: Import existing code to generate diagrams
- [ ] **Enhanced Examples**: More example projects and tutorials
- [ ] **Collaboration Features**: Multi-user editing capabilities
- [ ] **Plugin System**: Allow community extensions

#### Low Priority
- [ ] **Additional UML Diagrams**: Support for sequence, activity, and state diagrams
- [ ] **Theme Support**: Dark mode and customizable UI themes
- [ ] **Cloud Storage**: Save/load projects from cloud services
- [ ] **Mobile Viewer**: Read-only mobile app for viewing diagrams

### Known Issues 🐛

- Rare camera positioning edge cases in complex diagrams
- Performance degradation with very large diagrams (>100 classes)
- Some XMI 1.1 features not fully supported

### Contributing to Roadmap

Have ideas for new features? See [CONTRIBUTING.md](CONTRIBUTING.md) for how to propose features and contribute code.

## Contributing

We welcome contributions from the community! Whether it's:
- 🐛 Bug reports
- 💡 Feature suggestions
- 📝 Documentation improvements
- 🔧 Code contributions

Please read our [Contributing Guide](CONTRIBUTING.md) for details on:
- How to set up your development environment
- Our code style and standards
- How to submit pull requests
- Our code of conduct

## Additional Resources

- **Detailed Manual**: [Instruction Manual (PDF)](https://github.com/Nurtak/ObjectGraphVisualization/releases/download/v3.1/Instruction.Manual.pdf)
- **Academic Thesis** (German): [HSR Thesis](http://eprints.hsr.ch/459/)
- **SourceForge**: [Project Page](https://sourceforge.net/projects/ogvisualizer/)

## Technical Stack

- **Language**: Java 17
- **UI Framework**: JavaFX 21 LTS
- **Build Tool**: Maven 3.9+
- **3D Graphics**: JavaFX 3D + FXyz3D Library
- **Testing**: JUnit 5
- **Logging**: Log4j 2

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Acknowledgments

- Original development as part of HSR (Hochschule für Technik Rapperswil) thesis project
- Thanks to all contributors and users who have provided feedback
- Built with JavaFX and the FXyz3D library

---

**Project Status**: Active Development | **Current Version**: 3.2.0 | **Java Version**: 17+

For questions, issues, or discussions, please use the [GitHub Issues](https://github.com/logic-arts-official/ObjectGraphVisualization/issues) page.
