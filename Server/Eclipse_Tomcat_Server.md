# 이클립스 톰캣 서버 설정

### 1. 기본적인 인코딩 설정
- Perspective Java EE 변경
- window
- Preferences
- Encoding 검색
    - Workspace, CSS, HTML, JSP, XML 인코딩 UTF-8 수정
- Spelling 검색 인코딩 UTF-8 수정

<br>

### 2. 서버 생성하기
- window
- Preferences
- Server
- Runtime Environments
    - Add
    - 서버선택
    - 파일경로 설정
    - Create a new local server체크하면 서버탭에 바로 추가됨
- 서버 생성 후
    - 포트번호 수정
    - Server modules without publishing 체크

<br>

### 3. 프로젝트 설정
- 프로젝트 오른쪽 클릭
- properties
    - Project Facets
    - Dynamic Web Module, Java, JavaScript 체크확인
    - Java버전11 변경
- Java Build Path
    - Default output folder경로 src/main/webapp/WEB_INF/classes 설정(프로젝트 생성시 설정 가능)
- 서버탭 Add and Remove 프로젝트 연결
- WEB-INF/lib에 ojdbc.jar붙여넣기