# Step 1 - Install Gradle

Gradle is the build automation tool used to compile, test, and package the Java application.

### Install Gradle

```bash
sudo apt install gradle -y
```

### Verify the Installation

```bash
gradle -v
```

The command should display the installed Gradle version and Java environment.

---

# Step 2 - Clone the Project Repository

Clone the project from GitHub and navigate to the project directory.

### Clone Repository

```bash
git clone https://github.com/Ibrahim-Adel15/calculator-gradle.git
```

### Navigate to the Project

```bash
cd calculator-gradle
```

### Verify Project Files

```bash
ls
```

You should see files such as:

- `build.gradle`
- `gradlew`
- `settings.gradle`
- `src/`

### Screenshot

![Clone Repository](screenshots/clone_repo.png)

---

# Step 3 - Run Unit Tests

Before running the project, execute the unit tests to verify that the source code works correctly.

### Grant Execute Permission

```bash
chmod +x gradlew
```

### Run Unit Tests

```bash
./gradlew test
```

### Expected Result

```text
BUILD SUCCESSFUL
```

### Screenshot

![Run Unit Tests](screenshots/gradle_test.png)

---

# Step 4 - Build the Application

Build the project and generate the executable JAR file.

### Build Command

```bash
./gradlew build
```

### Expected Result

```text
BUILD SUCCESSFUL
```

### Screenshot

![Build Application](screenshots/build.png)

---

# Step 5 - Verify the Generated Artifact

Verify that the JAR file has been generated successfully.

### Command

```bash
ls build/libs/
```

### Expected Output

```text
calculator.jar
```

### Screenshot

![Generated Artifact](screenshots/list_repo.png)

---

# Step 6 - Run the Application

Run the generated JAR file.

### Command

```bash
java -jar build/libs/calculator.jar
```

### Screenshot

![Run Application](screenshots/run_program.png)

---

# ✅ Conclusion

In this lab, the Java application was successfully:

- Installed Gradle.
- Cloned from GitHub.
- Tested using Gradle.
- Built successfully.
- Packaged into a JAR file.
- Executed successfully.