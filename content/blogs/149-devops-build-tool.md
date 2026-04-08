---
title: "DevOps - Step By Step Learning : Part 26 (Build Tools and Its Necessity)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-03-10T00:00:00Z"
tags: ["devops" , "build-tool"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/149-devops-build-tool.jfif"
    caption: "DevOps Build Tools"
    alt: "DevOps Build Tools"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 25:** [DevOps - Step By Step Learning : Part 25 (Docker Networking With Help Of Linux Namespace)]({{< ref "blogs/148-devops-docker-networking.md" >}})
---

{{< figure
    src="/img/blogs/149-devops-build-tool.jfif"
    caption="DevOps Build Tools (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel observed some of his junior software developer colleagues limited to an IDE. This means they were skilled at writing code and running it with a single click of the IDE's run button. But they didn't know how the code was built on the server side. They should know beyond the IDE, as the server has no IDE or run buttons at all. So Rasel decided to assist them in understanding the build tools, how they work, and their importance.

* * *

### What is a Build Process?

A **build process** is the sequence of automated steps to transform source code into a final executable or deployable artifact.

## Common Build Steps:

*   **Clean**: Remove old build artifacts (e.g., target/, bin/)
*   **Restore/Install**: Download dependencies from package managers
*   **Compile**: Convert source code into machine-readable format (bytecode, binary, etc.)
*   **Test**: Run automated tests (unit, integration, etc.)
*   **Package**: Bundle compiled code into deployable formats like .jar, .exe, .zip
*   **Publish** (Optional): Deploy or export final package to a registry or environment

## Problems Build Tools Solve:

*   **Manual repetition & human error**: Automate every build step
*   **Dependency management complexity**: Automatically resolve and install packages
*   **Inconsistent builds across developers**: Ensure same results through scripts/configs
*   **Tedious testing and packaging**: Integrate tests and packaging in the build process
*   **CI/CD integration**: Seamlessly connect to pipelines (GitHub Actions, etc.)

## Popular Build Tools for Different Cases:

*   **Java**: Maven, Gradle, Ant
*   **.NET (C#)**: MSBuild, dotnet CLI
*   **JavaScript**: Webpack, npm scripts, Gulp
*   **Go**: go build, Make
*   **Python**: Poetry, setuptools, pip
*   **C/C++**: Make, CMake, Ninja
*   **Rust**: Cargo
*   **Android**: Gradle
*   **iOS/macOS**: Xcode, Fastlane

* * *

Examples of Some Build Tools
----------------------------

### Java with Maven

**Structure**:

```bash
myapp/
├── pom.xml
└── src/main/java/com/example/App.java        
```

**pom.xml (example)**:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>myapp</artifactId>
  <version>1.0-SNAPSHOT</version>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>        
```

**Commands**:

```bash
cd myapp
mvn clean           # Step 1: Clean previous builds
mvn compile         # Step 2: Compile Java source
mvn test            # Step 3: Run tests
mvn package         # Step 4: Package as JAR
mvn install         # Step 5: Install to local Maven repo        
```

**Output**: target/myapp-1.0-SNAPSHOT.jar

### .NET (C#) with dotnet CLI / MSBuild

**Structure**:

```bash
myapp/
├── myapp.csproj
└── Program.cs        
```

**Using dotnet CLI**:

```bash
dotnet new console -n myapp     # Step 1: Create project
cd myapp

dotnet restore                  # Step 2: Restore dependencies
dotnet build                    # Step 3: Compile
dotnet test                     # Step 4: Run tests (if present)
dotnet publish -c Release       # Step 5: Create deployable        
```

**Using MSBuild**:

```bash
msbuild myapp.csproj /p:Configuration=Release        
```

**Output**:

*   bin/Debug/net8.0/myapp.dll
*   bin/Release/net8.0/publish/myapp.exe (for deployment)

### JavaScript with Webpack

**Structure**:

```bash
myapp/
├── package.json
├── webpack.config.js
└── src/index.js        
```

**webpack.config.js**:

```js
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: __dirname + '/dist',
  },
};        
```

**Commands**:

```bash
npm init -y                               # Step 1: Init package.json
npm install webpack webpack-cli --save-dev  # Step 2: Install Webpack
npx webpack                               # Step 3: Run the build        
```

**Output**: dist/bundle.js

### Go with go build and Make

**Structure**:

```bash
myapp/
├── main.go
└── Makefile        
```

**Makefile**:

```bash
build:
    go build -o myapp main.go

test:
    go test ./...        
```

**Commands**:

```bash
make build         # Step 1: Compile Go code
make test          # Step 2: Run tests        
```

**Output**: Binary file myapp

### Python with Poetry

**Structure**:

```bash
myapp/
├── pyproject.toml
└── myapp/__init__.py        
```

**Commands**:

```bash
pip install poetry                 # Step 1: Install Poetry
poetry init                       # Step 2: Create pyproject.toml
poetry add requests               # Step 3: Add dependencies
poetry install                    # Step 4: Install deps
poetry build                      # Step 5: Build sdist and wheel        
```

**Output**: dist/myapp-0.1.0.tar.gz and .whl

### C/C++ with CMake

**Structure**:

```bash
myapp/
├── CMakeLists.txt
├── main.cpp
└── build/        
```

**CMakeLists.txt**:

```bash
cmake_minimum_required(VERSION 3.10)
project(MyApp)
add_executable(myapp main.cpp)        
```

**Commands**:

```bash
mkdir build && cd build
cmake ..              # Step 1: Generate build system
make                  # Step 2: Compile the project        
```

**Output**: build/myapp

* * *

## Summary:

*   Build tools automate the complete lifecycle from source to deployable output.
*   They reduce errors, save time, and integrate well with pipelines.
*   Learning the steps for your language's tool helps you build faster and more reliably.