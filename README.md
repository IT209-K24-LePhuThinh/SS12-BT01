# BT01 - CI đa phiên bản JDK với Matrix Strategy

## Workflow

File `.github/workflows/ci-matrix.yml` chạy khi push vào `main` với ma trận Java 17 và 21, dùng `actions/checkout@v5`, `actions/setup-java@v5`, Temurin và Gradle cache.

## Kết quả chạy thật

Run: https://github.com/IT209-K24-LePhuThinh/SS12-BT01/actions/runs/38770533536

```text
Test on Java 17    success    2026-10-15 16:37:20 - 16:37:57 UTC
Test on Java 21    success    2026-10-15 16:37:20 - 16:38:04 UTC

Java 17
  java-version: 17
  distribution: temurin
  cache: gradle
  > Task :test
  BUILD SUCCESSFUL in 30s
  2 actionable tasks: 2 executed

Java 21
  java-version: 21
  distribution: temurin
  cache: gradle
  > Task :test
  BUILD SUCCESSFUL
```

## Cấu hình chính

```yaml
strategy:
  matrix:
    java-version: ['17', '21']
```
