# 📦 Kotlin Reflection-Based Serializer Project

# Table of Contents

- [Project Objective](#-project-objective)
- [Technical Requirements](#-technical-requirements)
  - [Functional Requirements](#-functional-requirements)
  - [Constraints](#-constraints)
- [Project Structure](#-project-structure)
- [Suggested Development Steps](#-suggested-development-steps)
  - [Define Annotations](#1-define-annotations)
  - [Implement Reflection Utilities](#2-implement-reflection-utilities)
  - [Design Core Interfaces](#3-design-core-interfaces)
  - [Format-Specific Implementations](#4-format-specific-implementations)
    - [YAML](#yaml)
- [Examples](#-examples)
- [Testing](#-testing)
- [Deliverables](#-deliverables)
- [Extra Challenge (Optional)](#-extra-challenge-optional)
    - [XML](#xml)
- [Links and Resources](#-links-and-resources)
- [Collaborating on the Project](#-collaborating-on-the-project)
  - [Prerequisites](#prerequisites)
  - [Git Basics](#git-basics)
  - [Create the Repository](#create-the-repository)
  - [Clone the Repository](#clone-the-repository)
  - [Create a New Branch for Your Work](#create-a-new-branch-for-your-work)
  - [Make Your Changes Locally](#make-your-changes-locally)
  - [Push Your Branch to GitHub](#push-your-branch-to-github)
  - [Open a Pull Request (PR)](#open-a-pull-request-pr)
  - [Review Each Other's Code](#review-each-others-code)
  - [Sync with Main Branch Regularly](#sync-with-main-branch-regularly)
  - [Avoid Merge Conflicts](#avoid-merge-conflicts)
  - [Best Practices](#best-practices)


## 🧠 Project Objective

Your goal is to create a **serialization and deserialization library** in **Kotlin** using **reflection**. The library must work with _any Kotlin data class_ and support multiple output formats:

- **YAML**
- **XML** (see Extra Challenge below)

You **must not** use libraries like `kotlinx.serialization`, Jackson, Gson, Moshi, or similar. The aim is to deeply understand how serialization works and how frameworks like Spring use reflection.

## 🔧 Technical Requirements

### 🔹 Functional Requirements

Ensure that your serializers and deserializers are robust by testing with different and complex data class structures. Consider edge cases, such as data classes with nullable properties, properties with default values, and deeply nested structures.

- Serialize and deserialize _any Kotlin data class_ to/from:

  - **YAML** (key-value indented)
  - **XML** (with root and field tags, see Extra Challenge below)

- Support:

  - **Lists of objects**
  - **Nested data classes**
  - **Annotations** to customize field names and class root

### 🔹 Constraints

- Use **only reflection** to access properties and types (`KClass`, `KProperty1`, `KParameter`). Familiarize yourself with `KClass`, `KMutableProperty1`, and other useful types in Kotlin's reflection library. These will allow you to access and manipulate properties dynamically.
- Do **not** use external serialization libraries
- Use `StringBuilder` or similar to build the format strings manually
- Use **Kotlin** features like `data class`, `sealed class`, `enum class`, etc.
- Use **Kotlin** collections (`List`, `Map`, etc.) for nested structures

## 🌐 Project Structure

Keep your code modular with clear separations between the annotations, core interfaces, and format-specific implementations. Start by ensuring your basic structure is sound before diving into complex format implementations.

```text
converter/
├── annotations/
│   ├── SerializableRoot.kt
│   └── SerializableField.kt
├── core/
│   ├── Serializer.kt
│   ├── Deserializer.kt
│   └── ReflectUtils.kt
├── formats/
│   ├── xml/
│   │   ├── XmlSerializer.kt
│   │   └── XmlDeserializer.kt
│   └── yaml/
│       ├── YamlSerializer.kt
│       └── YamlDeserializer.kt
├── model/
│   └── SampleData.kt
├── testcases/
│   ├── input/
│   └── expected/
└── Main.kt
```

## 🪡 Suggested Development Steps

### 1. Define Annotations

Annotations can help customize serialization behavior by providing metadata about how each class or property should be treated.

```kotlin
@Target(AnnotationTarget.CLASS)
annotation class SerializableRoot(val name: String)

@Target(AnnotationTarget.PROPERTY)
annotation class SerializableField(val name: String)
```

Use these to customize how class names and property names appear in the output formats.

### 2. Implement Reflection Utilities

Create utility functions that can traverse all properties of a data class, including nested ones. These utilities should be able to retrieve annotations and their values to guide the serialization process.
Create helper functions to:

- Access all declared properties
- Access annotations and their values
- Match constructor parameters to values
- Recursively handle nested classes:

### 3. Design Core Interfaces

The interfaces will define the contract for your serializers and deserializers. Think about how you can make these interfaces generic and flexible to support any data type and nested structures.

```kotlin
interface Serializer {
    fun <T : Any> serialize(entity: T): String
    fun <T : Any> serializeList(entities: List<T>): String
}

interface Deserializer {
    fun <T : Any> deserialize(input: String, clazz: KClass<T>): T
    fun <T : Any> deserializeList(input: String, elementClazz: KClass<T>): List<T>
}
```

### 4. Format-Specific Implementations

For each format, create:

- A `Serializer` class implementing serialization logic
- A `Deserializer` class to parse back the string into objects

#### YAML

YAML's significant whitespace can be tricky. Make sure your implementation captures correct indentation levels for nested structures.

- Use `key: value` structure
- Use indentation for nesting
- Lists are prefixed with `-`

## 🔮 Examples

```kotlin
@SerializableRoot("book")
data class Book(
    @SerializableField("title") val title: String,
    val author: Author,
    val year: Int
)

data class Author(val name: String, val birthdate: String)
```

**YAML example:**

```yaml
title: Don Quixote
author:
  name: Miguel de Cervantes
  birthdate: 1547-09-29
year: 1605
```

## 🕹️ Testing

Create comprehensive test cases to cover all supported formats and edge cases. Use both positive (valid data) and negative (incorrect or malformed data) test scenarios to ensure robustness.

- Create a `testcases/` folder with files:

  - `book.yaml`
  - Corresponding expected files

- Write a test script to:

  - Read the input
  - Run deserialization and serialization
  - Compare results

## ✅ Deliverables

- Source code for:

  - YAML serializers and deserializers
  - Annotations
  - Error handling and reporting when serialization/deserialization fails (e.g., missing fields, nulls, incorrect types)
  - Example models

- Implement **unit tests** for each component
  - Test cases for:
    - Edge cases
    - Serialization
    - Deserialization
    - Error handling
  - Use `testcases/` folder for input and expected output files
  - Use `testcases/input/` for input Files

- README with:

  - Setup instructions
  - Usage examples
  - Team members

- GitHub repo with:

  - Commit history
  - At least 3 pull requests

## 🚀 Extra Challenge (Optional)

- Support **default values** for missing fields
- Add type inference and advanced error reporting during deserialization
- Support **custom types** (e.g., `LocalDate`, `UUID` and to use String for this types)
- Support **enums** and **sealed classes**
- XML support

### XML

When writing XML, ensure proper use of tags and consider edge cases where your XML might need to handle attributes versus nested tags.

- Use tags for fields
- Use the class name (or `@SerializableRoot`) as the root element

**XML example:**

```xml
<book>
    <title>Don Quixote</title>
    <author>
        <name>Miguel de Cervantes</name>
        <birthdate>1547-09-29</birthdate>
    </author>
    <year>1605</year>
</book>
```

## 📚 Links and Resources

- [Hiperskill: Introduction to Kotlin reflection](https://hyperskill.org/learn/step/25896)
- [Hiperskill: Reflection](https://hyperskill.org/learn/step/30991)
- [Hiperskill: Generics and Reflection](https://hyperskill.org/learn/step/10088)
- [Hiperskill: Intro to annotations](https://hyperskill.org/learn/step/22296)
- [Hiperskill: Custom annotations](https://hyperskill.org/learn/step/23245)
- [Kotlin Reflection Documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/)
- [Kotlin Data Classes](https://www.baeldung.com/kotlin/reflection)
- [Kotlin Annotations](https://kotlinlang.org/docs/annotations.html)
- [Kotlin Data Classes](https://kotlinlang.org/docs/data-classes.html)
- [YAML specification](https://yaml.org/spec/1.2.2/)
- [XML specification](https://www.w3.org/TR/xml/)
- [Kotlin reflection and prepared statement tutorial](https://dev.to/keyridan/kotlin-reflection-and-prepared-statement-tutorial-477l)
- [Mastering Java Reflection: Building a Custom JSON Parser from Scratch](https://www.youtube.com/watch?v=dLDXsq8Nr4o)
- [YAML Tutorial : A Complete Language Guide with Examples](https://spacelift.io/blog/yaml)


# Collaborating on the Project

## Prerequisites

- A GitHub account.
- Git installed on your computer.

## Basic knowledge of Git (clone, commit, push, pull).

1. Create the Repository
   One student (or the teacher) should:

- Create a new GitHub repository (e.g. library-system-kotlin).
- Initialize it with a README file and .gitignore for Kotlin/IntelliJ.
- Add collaborators in Settings > Collaborators (if using a private repo).

2. Clone the Repository
   Each team member should clone the repository to their local machine:

```bash
git clone https://github.com/username/library-system-kotlin.git
cd library-system-kotlin
```

3. Create a New Branch for Your Work
   Always create a new branch to work on a specific feature or task.

```bash
git checkout -b feature/add-book-class
```

Use descriptive names like feature/, bugfix/, or refactor/.

4. Make Your Changes Locally
   Implement your feature or fix. Use meaningful commit messages.

```bash
git add .
git commit -m "Add Book class with initial fields"
```

5. Push Your Branch to GitHub

```bash
git push origin feature/add-book-class
```

6. Open a Pull Request (PR). This is a request to merge your changes into the main branch.

- Go to GitHub and:
  - Click Compare & pull request.
  - Write a clear title and description:
  - What the branch does.
  - What files were changed.
  - Mention if review or testing is needed.
  - Assign it to your partner or a teammate.

7. Review Each Other's Code

- Go to the Pull Request tab.
  - Click on the PR you want to review.
  - Check the "Files changed" tab to see what has been modified.
  - Read the code and comment if needed.
  - If you find issues, leave comments on specific lines.
  - If everything looks good, approve the PR.
  - Click on the "Review changes" button and select one of the options:
    - Approve: If everything is fine.
    - Request changes: If you find issues that need to be fixed.
    - Comment: If you have questions or suggestions but don't want to block the merge.
  - When ready, click Merge to add it to the main branch.

8. Sync with Main Branch Regularly

- Before starting new work:

```bash
git checkout main
git pull origin main
```

- This ensures you have the latest changes from the main branch.
- If you have uncommitted changes, stash them first:

```bash
git stash
```

- Then create a new branch from up-to-date main.

9. Avoid Merge Conflicts

- Communicate regularly.
- Don’t work on the same files in parallel.
- Pull and push often.

## Best Practices

- Use meaningful commit messages.
- Use branches for features, bug fixes, or experiments.
- Use descriptive names for branches (e.g., feature/add-book-class, bugfix/fix-serialization).
- Keep Pull Requests small and focused.
- Review before merging.
- Don't commit .idea/ or build/ directories.
- Use .gitignore properly.
