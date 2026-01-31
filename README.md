```bash
# ===== Project Environment Lock =====
# Change these paths to match your installed versions

# 1️⃣ Java
export JAVA_HOME="$HOME/.linuxbrew/opt/openjdk@21"
export PATH="$JAVA_HOME/bin:$PATH"

# 2️⃣ Maven
export M2_HOME="$HOME/.linuxbrew/opt/maven"
export PATH="$M2_HOME/bin:$PATH"

# 3️⃣ Optional: Gradle (if used)
export GRADLE_HOME="$HOME/.linuxbrew/opt/gradle"
export PATH="$GRADLE_HOME/bin:$PATH"

# ✅ Optional: Print versions to confirm
java -version
javac -version
mvn -version
gradle -version  # if you use Gradle
```


```bash
# ===== JDK Switcher =====
# Add this to ~/.bashrc or ~/.zshrc

function usejdk() {
  if [ -z "$1" ]; then
    echo "Usage: usejdk <version>"
    return 1
  fi

  local jdk_path=""

  case "$1" in
    21)
      jdk_path="$HOME/.linuxbrew/opt/openjdk@21"
      ;;
    22)
      jdk_path="$HOME/.linuxbrew/opt/openjdk@23"
      ;;
    25)
      jdk_path="$HOME/.linuxbrew/opt/openjdk"
      ;;
    *)
      echo "Unknown JDK version: $1"
      return 1
      ;;
  esac

  export JAVA_HOME="$jdk_path"
  export PATH="$JAVA_HOME/bin:$PATH"

  echo "Switched to JDK $1"
  java -version
  javac -version
}

```

# Reload bashrc 
```bash
source ~/.bashrc
```

### Switch to version

```bash
usejdk 21   # switch to JDK 21
usejdk 23   # switch to JDK 23
usejdk 25   # switch back to Leyden (if you ever want to experiment)
```
