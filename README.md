# BT01 - CI đa phiên bản JDK với Matrix Strategy

## 1. Tạo file `.github/workflows/ci-matrix.yml`

```yaml
name: CI Matrix

on:
  push:
    branches: [main]

jobs:
  test-matrix:
    name: Test on Java ${{ matrix.java-version }}
    runs-on: ubuntu-latest
    strategy:
      matrix:
        java-version: ['17', '21']
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-java@v5
        with:
          java-version: ${{ matrix.java-version }}
          distribution: 'temurin'
          cache: 'gradle'
      - run: chmod +x gradlew
      - run: ./gradlew test
```

## 2. Push code lên nhánh main

```bash
git add .github/workflows/ci-matrix.yml
git commit -m "ci: matrix test JDK 17 va 21"
git push origin main
```

## 3. Kết quả trên tab Actions

Job `test-matrix` tách thành 2 sub-job chạy song song:

```text
CI Matrix
  Test on Java 17    ✓  (1m 42s)
  Test on Java 21    ✓  (1m 55s)

Test on Java 17
  Set up job                                  ✓
  Run actions/checkout@v5                     ✓
  Run actions/setup-java@v5                   ✓
    java-version: 17
    distribution: temurin
    cache: gradle
  Run chmod +x gradlew                        ✓
  Run ./gradlew test                          ✓
    > Task :test
    BUILD SUCCESSFUL in 38s
    4 actionable tasks: 4 executed

Test on Java 21
  Set up job                                  ✓
  Run actions/checkout@v5                     ✓
  Run actions/setup-java@v5                   ✓
    java-version: 21
    distribution: temurin
    cache: gradle
  Run chmod +x gradlew                        ✓
  Run ./gradlew test                          ✓
    > Task :test
    BUILD SUCCESSFUL in 44s
    4 actionable tasks: 4 executed
```
