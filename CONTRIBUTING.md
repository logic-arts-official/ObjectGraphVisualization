# Contributing to Object Graph Visualizer

First off, thank you for considering contributing to Object Graph Visualizer! It's people like you that make OGV such a great tool for education and learning.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Testing Guidelines](#testing-guidelines)

## Code of Conduct

### Our Pledge

We are committed to making participation in this project a harassment-free experience for everyone, regardless of level of experience, gender, gender identity and expression, sexual orientation, disability, personal appearance, body size, race, ethnicity, age, religion, or nationality.

### Our Standards

**Positive behavior includes:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Unacceptable behavior includes:**
- Trolling, insulting/derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information without explicit permission
- Other conduct which could reasonably be considered inappropriate in a professional setting

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the [issue tracker](https://github.com/logic-arts-official/ObjectGraphVisualization/issues) to avoid duplicates.

When reporting bugs, include:
- **Clear title and description**
- **Steps to reproduce** the problem
- **Expected behavior** vs. **actual behavior**
- **Screenshots** if applicable
- **Environment details**: OS, Java version, OGV version
- **Log files** if available (check console output)

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:
- **Clear title and description** of the enhancement
- **Rationale**: Why is this enhancement needed?
- **Use case**: Describe a specific scenario
- **Alternatives**: Have you considered any alternative solutions?
- **Additional context**: Screenshots, mockups, or examples

### Your First Code Contribution

Unsure where to begin? Look for issues tagged with:
- `good first issue`: Good for newcomers
- `help wanted`: Extra attention needed
- `documentation`: Improvements or additions to documentation

### Pull Requests

1. **Fork the repository** and create your branch from `master`
2. **Make your changes** following our coding standards
3. **Test your changes** thoroughly
4. **Update documentation** if needed
5. **Submit a pull request**

## Development Setup

### Prerequisites

- **Java 17+**: [Download from Adoptium](https://adoptium.net/)
- **Maven 3.6.3+**: [Download from Apache](https://maven.apache.org/download.cgi)
- **Git**: For version control
- **IDE** (recommended): IntelliJ IDEA, Eclipse, or VS Code with Java extensions

### Setup Steps

```bash
# Clone your fork
git clone https://github.com/YOUR-USERNAME/ObjectGraphVisualization.git
cd ObjectGraphVisualization

# Add upstream remote
git remote add upstream https://github.com/logic-arts-official/ObjectGraphVisualization.git

# Install dependencies
mvn validate

# Build and test
mvn clean package

# Run the application
java -jar target/ogv-*-runnable.jar
```

### Project Structure

```
ObjectGraphVisualization/
├── src/
│   ├── main/
│   │   ├── java/          # Java source files
│   │   │   └── ch/hsr/ogv/
│   │   │       ├── controller/  # Application controllers
│   │   │       ├── dataaccess/  # Data persistence & XMI import
│   │   │       ├── model/       # Domain models
│   │   │       ├── util/        # Utility classes
│   │   │       └── view/        # JavaFX views and 3D rendering
│   │   └── resources/     # FXML, images, stylesheets
│   └── test/
│       └── java/          # Test files
├── lib/                   # Local JAR dependencies
├── examples/              # Example OGV files
├── pom.xml               # Maven configuration
└── README.md
```

## Pull Request Process

### Before Submitting

1. **Update your fork**:
   ```bash
   git fetch upstream
   git rebase upstream/master
   ```

2. **Run tests**:
   ```bash
   mvn clean test
   ```

3. **Check code compiles**:
   ```bash
   mvn clean compile
   ```

4. **Test manually**: Run the application and verify your changes work

### Submitting

1. **Create a descriptive branch name**:
   ```bash
   git checkout -b feature/add-export-to-png
   git checkout -b fix/camera-positioning-bug
   ```

2. **Make focused commits** with clear messages (see [Commit Guidelines](#commit-message-guidelines))

3. **Push to your fork**:
   ```bash
   git push origin feature/add-export-to-png
   ```

4. **Create Pull Request** on GitHub with:
   - **Clear title** summarizing the change
   - **Description** explaining what and why
   - **Related issues** linked (e.g., "Fixes #123")
   - **Testing notes** explaining how to test your changes

### Review Process

- Maintainers will review your PR within a few days
- Address any requested changes
- Once approved, your PR will be merged

## Coding Standards

### Java Style Guide

- **Follow existing code style** in the project
- **Use Java naming conventions**:
  - Classes: `PascalCase`
  - Methods/Variables: `camelCase`
  - Constants: `UPPER_SNAKE_CASE`
  - Packages: `lowercase`

- **Organize imports**: Remove unused imports
- **Format code**: Use consistent indentation (4 spaces or tab as in project)
- **Add JavaDoc** for public APIs:
  ```java
  /**
   * Calculates the distance between two 3D points.
   *
   * @param point1 the first point
   * @param point2 the second point
   * @return the Euclidean distance
   */
  public double calculateDistance(Point3D point1, Point3D point2) {
      // implementation
  }
  ```

### Best Practices

- **Keep methods small and focused**
- **Avoid code duplication**
- **Use meaningful variable names**
- **Handle exceptions appropriately**
- **Log important events** using Log4j
- **Don't commit commented-out code**
- **Don't commit debug print statements**

### JavaFX Specific

- **Separate UI from logic**: Use MVC/MVVM patterns
- **Use FXML** for complex UI layouts
- **Keep UI updates on JavaFX Application Thread**:
  ```java
  Platform.runLater(() -> {
      // UI update code
  });
  ```

## Commit Message Guidelines

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type

- **feat**: New feature
- **fix**: Bug fix
- **docs**: Documentation only
- **style**: Formatting, missing semicolons, etc. (no code change)
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Performance improvement
- **test**: Adding or updating tests
- **chore**: Build process, dependencies, tools

### Examples

```
feat(export): add PNG export functionality

Implement PNG export for class diagrams using JavaFX snapshot API.
Export menu item added to File menu with keyboard shortcut Ctrl+E.

Closes #42
```

```
fix(camera): correct rotation axis calculation

Fixed issue where camera rotation would flip unexpectedly when
rotating beyond 90 degrees. Changed rotation calculation to use
quaternions instead of Euler angles.

Fixes #156
```

```
docs(readme): update installation instructions

Updated Java version requirement from 8 to 17.
Added troubleshooting section for common JavaFX issues.
```

## Testing Guidelines

### Writing Tests

- **Write tests for new features**
- **Write tests for bug fixes** to prevent regression
- **Use descriptive test method names**:
  ```java
  @Test
  void shouldCalculateCorrectDistanceBetweenTwoPoints() {
      // test implementation
  }
  ```

### Test Structure

Use the **Arrange-Act-Assert** pattern:
```java
@Test
void shouldAddClassToModel() {
    // Arrange
    Model model = new Model();
    ClassBox classBox = new ClassBox("MyClass");
    
    // Act
    model.addClass(classBox);
    
    // Assert
    assertEquals(1, model.getClasses().size());
    assertTrue(model.getClasses().contains(classBox));
}
```

### Running Tests

```bash
# Run all tests
mvn test

# Run specific test class
mvn test -Dtest=ModelTest

# Run specific test method
mvn test -Dtest=ModelTest#shouldAddClassToModel
```

## Questions?

- **General questions**: Open a [GitHub Discussion](https://github.com/logic-arts-official/ObjectGraphVisualization/discussions)
- **Bug reports**: Open an [Issue](https://github.com/logic-arts-official/ObjectGraphVisualization/issues)
- **Security issues**: Email the maintainers (see README)

## Recognition

Contributors will be:
- Listed in the project's contributors page
- Mentioned in release notes for significant contributions
- Part of an awesome open-source community!

---

Thank you for contributing to Object Graph Visualizer! 🎉
