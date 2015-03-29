# Environment


2014-11-30 21:01

## 1. Download ADT bundle from Android Developer

## 2. Download Java for OS X 2014-001 from "http://support.apple.com/kb/DL1572"

## 3. Modify eclipse.ini to solve build error
```
Errors running builder 'Android Resource Manager' on Project java.lang.NullPointerException
http://blog.csdn.net/gtsong/article/details/39481879
```

## 4. set the java path for eclipse
[Mac OS X Java Update: where is my jdk?](http://stackoverflow.com/questions/5271697/mac-os-x-java-update-where-is-my-jdk)

[parse L layout error](http://stackoverflow.com/questions/24483406/the-project-target-android-l-preview-was-not-properly-loaded)

## 5. Format

### 5.1 Content assist

Preference -> Java -> Editor -> Content Assist -> Auto Activation, set "Auto activation triggers for Java" to ".
```
abcdefghijklmnopqrstuvwxyz
```

### 5.2. Coding Style

Preference -> Java -> Code Style -> Formatter, click "New..", then "Edit...",
-- Indentation, General settings -> Tab policy, set to "Spaces only", and change both size to 4
-- Line Wrapping, General settings -> Maximum line width, set to 100

### 5.3 Show white space

General -> Editors -> Text Editors, check "Show whitespace characters", and click "configure visibility", only keep trailing space and all tabs.


