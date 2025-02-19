### 💥 설계

### 요구사항

1. 개요

본 프로젝트는 AASX 패키지 파일을 업로드하여 JSON 형식으로 변환하고, 첨부파일을 해시 기반으로 탐색하여 다운로드 링크를 제공하는 기능을 제공합니다. 이를 통해 AASX 파일 내 중복된 첨부파일을 최소화하여 효율적으로 처리하고, 이를 URL로 변환하여 관리 및 접근을 용이하게 만듭니다.

### 시스템 구조

1. 기능
2. 플로우 차트

### 사용 언어/라이브러리

- Backend (Java)
    - Spring boot
    - https://github.com/eclipse-aas4j/aas4j
- Frondend (Typescript)
    - https://nextjs.org/
    - https://ui.shadcn.com/
- 사용 DB
    - 
- 개발도구
    - VS CODE
- 형상 관리
    - https://github.com/downying/AASX-Transformer.git

### 💥 AASX to JSON (Phase 1)

### Back-end

1. API를 통해 AASX 패키지 파일 업로드
    1. API URL : /api/transformer/aasx
2. AASX 패키지 파일 역직렬화 : 외부 파일의 데이터를 프로그램 내 object로 읽어옴 aas4j
3. AASX 내 XML 정보모델을 JSON 정보모델로 변환 aas4j
    1. 혹은 JSON으로 나중에 바꿔도 됨
4. File SubmodelElement 탐색
    1. SME에 저장된 첨부파일의 위치 확인 : 상대 경로로 되어있음
    2. 해당 첨부파일의 SHA256 해싱 값 계산 : 해싱 알고리즘 라이브러리 사용 (파일을 해싱)
    3. 첨부파일 해싱 값을 기반으로 동일 파일 검색
        1. 동일 파일 ❌ : 첨부파일의 이름을 해싱 값으로 변경하여 저장 
            
            → 해싱값은 다른데 파일 이름이 같은 경우를 방지 
            
        2. 해당 해싱 값으로 파일 다운로드 URL 구성

### Front-end

1. AASX-to-JSON 테스트 화면 
2. 첨부파일 탐색 (Phase 1)
    - 해시 기반 검색
    - 첨부파일 다운로드

### 프로젝트 생성

- Spring boot
    1. JDK-21 설치 (필수)
    
    https://www.oracle.com/java/technologies/javase/jdk21-archive-downloads.html
    
    - Java SE Development Kit 21.0.5
        - Windows x64 Installer
    - 시스템 환경 변수 설정
        - JAVA_HOME : ~/Java/JDK-17
    1. Gradle 설치 (선택)
    
    https://gradle.org/releases/
    
    - v8.12.1
        - Download:  complete
    - 시스템 환경 변수 설정
        - GRADLE_HOME : ~/gradle-x.x
        - path : C:\Program Files\gradle\gradle-8.12.1-all\gradle-8.12.1\bin
    1. VS CODE Spring Boot 확장 설치
    - Spring Boot Extension Pack
    - Spring Boot Developer Extension Pack
    - Spring Code Generator
    - Gradle for Java
    1. 프로젝트 생성
    
    ```
    Create Spring Initailizer
    ```
    
    - version : 3.x.x
    - language : Java
    - Group Id : com.aasx
    - Artifact Id : transformer
    - Packaging Type : War
    - Java Version : 17
    - Dependencies
        - Spring Web
        - SpringBoot DevTools
        - 추후 추가
    1. 서버 실행
    - Spring Boot Dashboard
- Next.js
    1. 프로젝트 생성
    
    ```bash
    npx create-next-app@latest aasx-transformer
    ```
    
    ![image.png](attachment:9e5e3387-845c-4132-996e-22a53f8cadcf:image.png)
    
    1. 서버 실행
    
    ```bash
    npm run dev
    ```
    
    ```
    http://localhost:3000/
    ```
    
    ![image.png](attachment:ee856eb2-f5bb-433c-b476-f63d6cb23e93:image.png)