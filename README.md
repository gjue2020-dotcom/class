# 학급 기록장 설치 안내

깃허브 페이지(화면)와 Firebase(저장)를 연결해서, 휴대폰·컴퓨터·전자칠판에서 같은 기록을 실시간으로 쓰는 방법이에요.
처음 한 번만 설정하면 되고, 30분 정도 걸려요. 두 서비스 모두 무료로 쓸 수 있어요.

## 들어 있는 파일

| 파일 | 하는 일 |
|---|---|
| index.html | 학급 기록장 화면 |
| config.js | Firebase 연결 정보 (2단계에서 직접 채워요) |
| manifest.json, icon-192.png, icon-512.png, apple-touch-icon.png | 홈 화면에 앱처럼 설치할 때 쓰는 이름과 아이콘 |
| firestore.rules | 기록을 선생님만 볼 수 있게 막는 보안 규칙 (4단계) |

---

## 1단계. 깃허브에 올리기

1. https://github.com 에 가입하고 로그인해요.
2. 오른쪽 위 **+** → **New repository** 를 눌러요.
3. Repository name에 영어로 이름을 적어요. 예: `class-record`
4. **Public** 을 고르고 **Create repository** 를 눌러요.
   - 무료 계정은 Public이어야 깃허브 페이지를 쓸 수 있어요.
   - 공개되는 건 화면 코드뿐이고, 학생 기록은 Firebase에 따로 저장돼서 보이지 않아요.
5. 다음 화면에서 **uploading an existing file** 링크를 눌러요.
6. 압축을 푼 파일 8개를 모두 끌어다 놓고 **Commit changes** 를 눌러요.
7. 저장소 위쪽 **Settings** → 왼쪽 **Pages** 로 가요.
8. Source는 **Deploy from a branch**, Branch는 **main** / **(root)** 로 고르고 **Save** 를 눌러요.
9. 1~2분 뒤 같은 화면 위쪽에 주소가 나와요. 예: `https://아이디.github.io/class-record/`
   - 지금 열면 "설정이 필요해요"가 나오는 게 정상이에요.

## 2단계. Firebase 프로젝트 만들고 연결 정보 넣기

1. https://console.firebase.google.com 에 구글 계정으로 들어가요.
2. **프로젝트 만들기** → 이름 입력(예: `class-record`) → Google 애널리틱스는 꺼도 돼요 → 만들기.
3. 프로젝트 첫 화면에서 **웹 아이콘 `</>`** 을 눌러 웹 앱을 추가해요.
   - 앱 닉네임: 아무거나 (예: `기록장`)
   - "Firebase 호스팅도 설정"은 체크하지 않아요.
4. **앱 등록** 을 누르면 `firebaseConfig = { apiKey: ... }` 코드가 보여요.
5. 깃허브 저장소에서 **config.js** 를 누르고, 오른쪽 위 **연필(Edit)** 버튼을 눌러요.
6. `"여기에"` 자리 6곳에 Firebase 화면의 값을 하나씩 옮겨 적어요. 따옴표는 그대로 두세요.

   ```js
   window.FIREBASE_CONFIG = {
     apiKey: "AIza...",
     authDomain: "class-record-xxxx.firebaseapp.com",
     projectId: "class-record-xxxx",
     storageBucket: "class-record-xxxx.firebasestorage.app",
     messagingSenderId: "1234567890",
     appId: "1:1234567890:web:abcd..."
   };
   ```
7. **Commit changes** 를 눌러 저장해요.

## 3단계. 구글 로그인 켜기

1. Firebase 왼쪽 메뉴 **빌드 → Authentication** → **시작하기**.
2. **Sign-in method** 탭 → **Google** → 사용 설정 켜기 → 지원 이메일 고르기 → **저장**.
3. **설정** 탭 → **승인된 도메인** → **도메인 추가** → `아이디.github.io` 를 적고 추가해요.
   - `https://` 나 `/class-record` 는 빼고 `아이디.github.io` 만 적어요.

## 4단계. 저장소(데이터베이스) 만들고 보안 규칙 넣기

1. Firebase 왼쪽 메뉴 **빌드 → Firestore Database** → **데이터베이스 만들기**.
2. 위치는 **asia-northeast3 (서울)** 을 골라요. 나중에 바꿀 수 없어요.
3. **프로덕션 모드에서 시작** 을 고르고 만들기.
4. 위쪽 **규칙** 탭으로 가서, 들어 있는 내용을 모두 지우고 `firestore.rules` 파일 내용을 붙여 넣은 뒤 **게시** 를 눌러요.

## 5단계. 쓰기 시작하기

1. 1단계의 주소를 열고 **구글 계정으로 로그인** 을 눌러요.
2. 학생 수를 확인하고 **2026학년도 시작** 을 눌러요.
3. **설정** 에서 요일별 시간표와 전자칠판 나가기 비밀번호를 정해요.

### 홈 화면에 앱처럼 설치하기
- **아이폰**: Safari로 주소 열기 → 아래 **공유** 버튼 → **홈 화면에 추가**
- **안드로이드**: Chrome으로 주소 열기 → 오른쪽 위 **⋮** → **앱 설치** 또는 **홈 화면에 추가**
- **컴퓨터**: Chrome·Edge 주소창 오른쪽의 **설치** 아이콘을 누르면 따로 창이 뜨는 프로그램처럼 쓸 수 있어요.
- **전자칠판**: 브라우저로 주소를 열고 같은 구글 계정으로 한 번 로그인해 두면 돼요.

설치해서 열면 주소창 없이 앱처럼 보여요.

---

## 나중에 화면을 고칠 때
- 새 `index.html` 을 받으면 깃허브 저장소에서 **Add file → Upload files** 로 덮어 올리면 돼요.
- `config.js` 는 다시 올릴 필요 없어요. 기록도 그대로 남아요.

## 무료 사용량
- 깃허브 페이지: 공개 저장소는 무료예요.
- Firebase 무료 요금제(Spark): 카드 등록 없이 쓸 수 있고, 하루에 문서 읽기 5만 번·쓰기 2만 번까지 무료예요. 한 학급 기록에는 충분해요.
- 한도를 넘어도 요금이 나가지 않고, 그날만 저장이 잠시 멈춰요.

## 문제가 생기면
| 화면에 나오는 말 | 확인할 것 |
|---|---|
| 설정이 필요해요 | config.js에 `"여기에"`가 남아 있지 않은지 (2단계) |
| 로그인하지 못했어요 (auth/unauthorized-domain) | 승인된 도메인에 `아이디.github.io` 를 넣었는지 (3단계) |
| 기록을 불러오지 못했어요 · 보안 규칙 | 규칙을 붙여 넣고 **게시** 를 눌렀는지 (4단계) |
