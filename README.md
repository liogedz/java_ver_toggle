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

  local brew_prefix="/home/linuxbrew/.linuxbrew"
  local jdk_path=""

  case "$1" in
    21) jdk_path="$brew_prefix/opt/openjdk@21" ;;
    25) jdk_path="$brew_prefix/opt/openjdk@25" ;;
    27) jdk_path="$brew_prefix/opt/openjdk@27" ;;
    *)
      echo "Unknown JDK version: $1"
      return 1
      ;;
  esac

  if [ ! -x "$jdk_path/bin/java" ]; then
    echo "JDK not found at $jdk_path"
    return 1
  fi

  export JAVA_HOME="$jdk_path"

  ln -sf "$JAVA_HOME/bin/java"  "$brew_prefix/bin/java"
  ln -sf "$JAVA_HOME/bin/javac" "$brew_prefix/bin/javac"
  ln -sf "$JAVA_HOME/bin/jar"   "$brew_prefix/bin/jar"

  export PATH="$JAVA_HOME/bin:$(echo "$PATH" | tr ':' '\n' | grep -v "$brew_prefix/opt/openjdk" | paste -sd ':' -)"

  hash -r

  echo "Switched to JDK $1"
  echo "JAVA_HOME=$JAVA_HOME"
  which java
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
usejdk 25   # switch to JDK 25
usejdk 27   # switch to JDK 27
```
