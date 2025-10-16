# Example CMake Project

이 프로젝트는 CMake기반의 프로젝트 템플릿입니다.

## 폴더 구조
```
CMakeLists.txt
include/
src/
    main.cpp
external/
    spdlog/
    CLI11/
```

## 빌드 방법

1. 빌드 디렉토리 생성 및 이동
   ```bash
   mkdir -p build
   cd build
   ```
2. CMake로 빌드 파일 생성
   ```bash
   cmake ..
   ```
3. Make로 빌드
   ```bash
   make
   ```

## 실행 방법

빌드가 완료되면, `build/example_project` 실행 파일이 생성됩니다.

```bash
./example_project
```

## 외부 라이브러리
- [spdlog](https://github.com/gabime/spdlog)
- [CLI11](https://github.com/CLIUtils/CLI11)

## 문의
- 작성자: Eunggi Kim
