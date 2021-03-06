# H+ground Frontend

목차 (지금은 링크가 불발이네요)


* [0. Requirement](#0.-Requirements)
* [1. 설치하기](#1.-설치하기)
  - [1.1 백엔드 설치하기](#1.1-백엔드-설치하기)
  - [1.2 프론트엔드 설치하기](#1.2-프론트엔드-설치하기)
* [2. 병원 프로필 만들기](#2.-병원-프로필-만들기-(백엔드))
  - [2.1 참고용 레이아웃](#2.1-참고용-레이아웃)
  - [2.2 데이터모델 만들기](#2.2-데이터모델-만들기)
  - [2.3 Resolver 만들기](#2.3-Resolver-만들기)
  - [2.4 Computed Field 만들기](#2.4-Computed-Field-만들기)
* [3. 병원 프로필 컴포넌트 만들기 (프론트엔드)](#3.-병원-프로필-컴포넌트-만들기-(프론트엔드))
  - [3.0 들어가기 전에 ](#3.0-들어가기-전에)
  - [3.1 컴포넌트에 접근하는 Route (URL) 만들기](#3.1-컴포넌트에-접근하는-Route-(URL)-만들기)
  - [3.2 컴포넌트 디자인: 개요](#3.2-컴포넌트-디자인:-개요)
  - [3.3 컴포넌트 디자인: Container](#3.3-컴포넌트-디자인:-Container)
  - [3.4 컴포넌트 디자인: Presenter](#3.4-컴포넌트-디자인:-Presenter)


# 0. Requirements


**Node js** (버젼은 10 이상이면 괜찮습니다)


**npm** / **yarn**: 둘 다 package를 manage해주는데 역할은 같다고 알아요. npm을 써도 무방하지만 체감상 속도가 빨라서 저는 yarn을 쓰고 있어요.


**git** 터미널(VS Code 터미널, Git Bash, 윈도우 파워셸/커맨드라인 등)에서 깃허브에 Commit, Push, Pull 등을 하기위해 필요합니다. 처음에 리포지토리를 clone 하는데도 필요하고요.


위의 세 종류 프로그램은 꼭 설치해주세요!


프론트엔드가 실행되는 모습은 [Netlify](https://hgroundtest.netlify.com)에서 확인하실 수 있습니다.

---

# 1. 설치하기

## 1.1 백엔드 설치하기

### 깃허브 폴더 받아오기

아직 받지 않으셨다면, 백엔드 [깃허브 리포지토리](https://github.com/slee333/prismagram)에서 백엔드를 받아주세요. 방법은 다음과 같습니다.


우선 터미널 (혹 커맨드라인) 내에서 프로젝트를 집어놓고 싶은 폴더 내로 이동합니다.


(예를 들어 저는 ~Documents/Projects 폴더에 설치했습니다.)


그리고 아래 커맨드를 실행해서 리포지토리를 다운받아주세요. 그리고 cd 커맨드를 통해 해당 리포지토리 내로 이동합니다.


```
git clone https://github.com/slee333/prismagram.git 
cd prismagram
```

---

### 패키지 설치하기

이제 프로젝트를 구동하는데 필요한 패키지 (일종의 자바스크립트 라이브러리)와 프리즈마 클라이언트를 설치할 차례입니다. 우선 아래 커맨드를 실행하여 패키지를 설치합니다.


```
yarn install
OR
npm install
```


이러면 패키지들이 설치됩니다. 다소 시간이 걸릴 수 있어요. (사실 yarn install 말고 그냥 yarn만 쳐도 똑같이 패키지 인스톨 과정이 실행되요.)

---


### 프리즈마 클라이언트 설치


yarn 혹은 npm을 이용해 패키지를 설치했다면, 이제 프리즈마 클라이언트를 설치할 차례입니다.

- **프리즈마**는 데이터베이스 관리도구 및 UI라 생각하시면 편합니다.

* **프리즈마 클라이언트**는 프리즈마에 접근할 수 있도록 해주는 자바스크립트 라이브러리입니다.


프리즈마를 설치하기 이전, 우선 슬랙에 있는 .env 파일이 필요합니다. 슬랙 > 백엔드방에 있는 해당 파일을 다운받아서 프로젝트 폴더에 넣어주세요. (datamodel.prisma, prisma.yml 등과 같은 폴더에 넣어주시면 됩니다.)


![Imgur](https://i.imgur.com/sUicnH5.png)


<<<<<<< HEAD
**`.env` 파일은 `prisma.yml` 파일과 같이 이렇게 프로젝트 최상단 폴더에 넣어주셔야합니다.**
=======
**이렇게 prisma.yml 파일과 .env 파일은 `src` 폴더가 아닌 프로젝트 최상단 폴더에 넣어주셔야합니다.**
>>>>>>> hospitalprofile


이후 다음 커맨드를 이용해 프리즈마 클라이언트를 설치해줍니다.


```
prisma generate
```


제가 백엔드 해설 적을때는 _prisma deploy_ 이후 *prisma generate*를 해야한다 적었는데요. 다시보니 prisma deploy는 현재 가지고 있는 데이터모델을 서버에다 올리는 작업을 합니다. 다시 말해 이미 데이터모델이 서버에 올라갔다면 굳이 실행할 이유가 없는 커맨드입니다. 따라서 prisma generate만 실행해줍니다.


혹시 이 과정에서 로그인을 하라고 한다면 마찬가지로 Slack에 백엔드방에 올려놓은 프리즈마 계정을 입력하시면 될 것 같습니다.


제가 이전에는 prisma.yml 파일이 prisma endpoint라는 데이터베이스에 직접적인 엑세스를 가지는 링크를 가지고 있어 깃허브에 올라가 있지 않다 말씀드렸습니다.


그런데 지금 이 리포지토리에서 보시면 prisma.yml이 올라가 있는데요. prisma endpoint를 prisma.yml 파일 내에 직접 적어두는게 아니라 .env 파일 안에 넣어두어서 그렇습니다.


---


### 백엔드 구동하기


이제 백엔드 구동에 필요한 요소들은 설치가 완료되었습니다. 백엔드를 실행하려면 다음 커맨드를 입력하여 백엔드를 구동합니다.


```
yarn dev
```


왜 구동에 이 커맨드를 쓰는지는 [백엔드 리포지토리](https://github.com/slee333/prismagram)에서 2.1.2 *package.json*에 대해 설명한 부분을 참고해주세요.


성공적으로 백엔드를 구동했다면, 이제 인터넷 URL에 localhost:4000를 쳐서 GraphQL Playground에 접속할 수 있습니다.


GraphQL playground를 통해 서버 내 데이터들을 수정도 해보고 DB를 수정하는 커맨드들을 실행도 해보고 할 수 있어요.


예를 들어 데이터베이스 내 유저를 검색하는 query를 실행해보겠습니다. localhost:4000을 들어가서 Playground를 실행해주시고 거기 뜨는 창에 다음과 같은 커맨드를 실행해주세요.


```js
query {
  seeUser (username:"ghouse") {
    id
    fullName
    bio
    createdAt
    adminof {
      id
      name
    }
    staffof {
      name
    }
  }
}
```


그러면 아마 다음과 같은 데이터를 받을겁니다.


```json
{
  "data": {
    "seeUser": {
      "id": "ck18ini0o000d071364eysphw",
      "fullName": "Gregory House",
      "bio": "Gregory House, M.D. (born 1959) is the title character of the American medical drama series House. Created by David Shore and portrayed by English actor Hugh Laurie, he leads a team of diagnosticians as the Head of Diagnostic Medicine at the fictional Princeton-Plainsboro Teaching Hospital in Princeton, New Jersey.",
      "createdAt": "2019-10-02T00:12:03.127Z",
      "adminof": [],
      "staffof": [
        {
          "name": "삼성서울병원"
        }
      ]
    }
  }
}
```


창 자체는 이렇게 뜰거에요.
![GraphQL Playground 창](https://i.imgur.com/hfmllVz.png)


부가설명을 조금 해놓겠습니다.


```js
query {
  seeUser (username:"ghouse") {
    // seeUser는 username이란 input 값을 받아 User를 찾아오는 query입니다.
    // 여기서는 input 인 username 값은 "ghouse"입니다. 이제 쿼리를 실행하면 "ghouse"란 사용자명을 가진 유저를 찾아옵니다.
    // 이 아래로는 찾은 사용자의 어떤 필드를 받을지를 결정합니다.
    // 보시면 저는 ghouse란 사용자 이름을 가진 유저의 id, fullName, bio(소개) 등을 받아옵니다.
    id
    fullName
    bio
    createdAt
    adminof {
      id
      name
    }
    staffof {
      name
    }
  }
}
```


이런식으로 그래프큐엘 플레이그라운드 내에서는 저희가 만든 쿼리들, 혹은 뮤테이션들을 이용해서 어떻게 데이터를 조회하거나 변형할 수 있는지 시험해 볼 수 있습니다. 나중에 이런 쿼리들을 프론트엔드에서도 실행해서 저희가 원하는 데이터를 서버로부터 불러올텐데, 어떻게 쿼리를 짜서 데이터를 원하는 모양으로 불러올지 등을 플레이그라운드를 통해 테스트할 수 있습니다.


GraphQL에 관해 자세한 내용은 [백엔드 리포지토리](https://github.com/slee333/prismagram)의 README.MD 파일에서 2.2.1번 목차를 참고해주세요.


---


### 데이터 생성하기


데이터를 만드는건 GraphQL Playground를 통해서도 할 수 있지만 아니라 프리즈마 사이트에서도 만들 수 있습니다.


[프리즈마 웹사이트](https://prisma.io) 접속 후 로그인 > 좌측 상단에서 드롭다운 메뉴 클릭 후 dhh10-workspace 선택 > hground-test 선택.


이렇게 해서 hground-test라는 프리즈마 서비스에 들어가면 저희 데이터베이스를 한눈에 보실 수 있습니다. 이런 창이 뜰겁니다.


![Imgur](https://i.imgur.com/4SS6wWo.jpg)


여기에서 저희 데이터를 직접 만져줄 수 있는데요. 10/02일 현재 사용자의 프로필 사진을 바꿀 수 있는 기능이 저희 프론트엔드에 아직 없습니다. 따라서 제 경우 아래와 같이 프로필 사진을 직접 바꾸어주었습니다.


![Imgur](https://i.imgur.com/b01Jrqy.jpg)


## 1.2 프론트엔드 설치하기


프론트엔드도 마찬가지로 설치합니다.


백엔드 때와 마찬가지로, 프로젝트 파일을 생성하고 싶은 디렉토리 내에서 다음 커맨드를 실행하여 프론트엔드 폴더를 다운받은 후 해당 폴더 내로 이동합니다.


```
git clone https://github.com/slee333/prismagram-frontend.git

cd prismagram-frontend
```


프론트앤드도 마찬가지로 패키지 설치가 필요합니다. 백엔드 때와 같이 yarn, 혹은 npm을 이용해 패키지를 설치해줍니다.


```
yarn install
or
npm install
```


모든 패키지 설치가 완료되었다면, 다음 커맨드를 이용해 프런트엔드를 실행해줍니다.


```
yarn start
```


성공적으로 완료되면 터미널에 다음과 같은 메시지가 뜨며 프론트엔드가 실행됩니다.


[Imgur](https://i.imgur.com/lp1BUsh.jpg)


여기까지 완료하시면 localhost:3000 주소를 통해 로컬에서 프런트엔드에 접속하실 수 있습니다. 이때 백엔드를 구동하고 있는 상황이셔야 해요!


그러지않으면 프런트엔드가 localhost:4000에 접속할 수 없어 **400 NOT FOUND** 에러가 뜰 수 있습니다.


### 접속하기


프런트엔드를 실행하면 다음과 같은 화면이 뜹니다.


![Imgur](https://i.imgur.com/CfcSyKr.png)


아마 이메일을 입력하면 (전에 회원가입하지 않은 이상) 없는 회원이라며 회원가입을 하라 할텐데요.


회원가입 후 로그인을 시도하면 Secret을 적으라는 창이 뜨고, 로그인시 입력했던 이메일로 secret을 담고 있는 이메일이 오게 됩니다.


![Imgur](https://i.imgur.com/dSdOvuv.png)


이메일로 받은 secret을 입력 후 접속해주시면 됩니다. 이후에는 자유롭게 둘러보실 수 있을텐데, 상단 서치바에 "slee333"을 검색하면 제 계정을 확인하실 수 있고, 제 계정을 팔로우하실 시 제가 올려놓은 포스트를 피드에서 보실 수 있을겁니다.


만일 접속하는 과정이 오래 걸린다면 백엔드와 연결되는 프리즈마 서버가 구동되는 중이라 그럴 수 있습니다. (2시간 정도 활동이 없으면 프리즈마 서버가 자동으로 꺼집니다..)


![Imgur](https://i.imgur.com/GLXdBCq.png)


계속 접속이 안된다면 프리즈마 워크스페이스(dhh10-workspace)에서 hground-test 의 status를 확인해주세요. Not reachable이라고 뜰 때가 있는데 접속을 누군가 시도하면 조금 시간이 지나고 다시 활성화될겁니다.


### 로그아웃


로그아웃은 상단 맨 오른쪽 프로필 페이지 > 로그아웃 버튼을 통해 하실 수 있습니다.


또는 저희가 로그인시 받아온 JWT token을 삭제함으로서 행하실수도 있습니다. 토큰이 무엇이었는지 궁금하시면 [백엔드 리포지토리](https://github.com/slee333/prismagram)에서 목차 **2.3.1**, **2.3.4**를 살펴보아주세요.


저희가 로그인시 받아온 토큰은 localStorage에 저장됩니다. 아마 웹 브라우저들은 다들 localStorage에 접근하는 방법이 있을텐데, 저는 크롬을 사용하니 일단 크롬 기준으로 설명하겠습니다.


크롬에서 F12를 눌러 Developer tool을 실행 - Application - LocalStorage - https://localhost:3000를 클릭하시면 해당 url 안의 localStorage에 저장된 내용들을 볼수 있습니다.


![Imgur](https://i.imgur.com/1Oq5cls.png)


여기서 token을 선택해서 지운 후 다시 페이지를 새로고침하면 로그아웃된 상태가 될거에요.


이 방법을 굳이 왜 알아야 하냐 하실수도 있지만 GraphQL Playground에서 로그인한 상태로 mutation을 실행해야 하는 경우, 예를 들어 어떤 포스트에 댓글을 단다거나 포스트를 새로 올리는 경우에는 이런 token을 playground 내에서 정의해줘야지 포스트가 올라갑니다. 이 내용은 아래 병원 프로필 만들기에서 더 자세히 다루어 보겠습니다.


---

# 2. 병원 프로필 만들기 (백엔드)

일단 제가 만들어놓은 병원 프로필 페이지 레이아웃은 (프런트엔드와 백엔드를 둘 다 구동중이시라면) http://localhost:3000/#/hospital/삼성서울병원 에서 확인하실 수 있습니다. 또는 제가 프론트엔드를 배포중인 링크인 https://hgroundtest.netlify.com/#/hospital/삼성서울병원 에서도 확인하실 수 있고요.

---

## 2.1 참고용 레이아웃


우선 제가 참고한 레이아웃은 [브런치](https://brunch.co.kr/@soyuly)입니다. 브런치에서 개인 프로필에 들어가면


1. 작가소개
2. 글
3. 작품


이렇게 3가지 상단 탭이 존재하는데요. 이와 유사한 구조로 병원 프로필 페이지 역시


1. 병원 소개
2. 병원 포스트
3. 병원 내 커뮤니티 기능?


등으로 구성을 목표했습니다.


또한 어플리케이션 중 '강남언니'에서 병원 정보를 찾아봤을 시 나오는 정보 페이지 역시 참고했습니다.


---

## 2.2 데이터모델 만들기

**Prisma**에 들어갈 데이터모델을 만듭니다.

우선 병원 프로필 페이지를 구성하는데 필요한 데이터를 구성해야합니다. 먼저 병원이란 객체가 어떻게 구성되어 있을지를 정의해야 하는데요.

병원이란 객체가 가져야 할 기능들 및 정보는 다음과 같습니다.

- 이름
- 주소
- 소개
- 연락처 (이메일 혹은 전화번호)
- 병원 사진 (배경사진)
- (병원 측에서 올리는) 포스트
- 병원 프로필 사진
- 병원 관리자, 소속 의료진, 소속 환자 명단

일단 이 정도가 있겠는데요.

병원 데이터에 이런 요소들이 포함되어야 한다는 사실을 알았으니 이제 병원 데이터모델을 한번 짜 보겠습니다.

### 2.2.1 datamodel.prisma

**백엔드** 폴더 안에서 datamodel.prisma를 찾아 열어줍니다. [백엔드 리포지토리](https://github.com/slee333/prismagram)에 2.1.3 부분을 보시면 이해에 도움되실거에요.

우선 병원이라는 데이터 객체를 정의해주겠습니다.

```js
type Hospital {
  id: ID! @id
}
```

여기서 id는 병원이라는 객체가 생성될 시 자동으로 생성되는 객체의 고유번호입니다.

#### 이름, 소개, 병원 연락처 필드 추가

앞서 병원이라는 데이터 객체 안에 들어갈 요소들로 이름, 주소, 병원 소개, 병원 연락처 (이메일 혹은 전화번호)가 있었는데요. 해당 요소들을 추가해주겠습니다.

```js
type Hospital {
  id: ID! @id
  location: String
  bio: String
  name: String! @unique
  email: String @unique
  contact: String @unique
}
```

> location: String

위치는 "모모시 모모구 모모동..." 과 같이 `String`으로 정의될테니 `String`이라 정의해줍니다. 병원 소개글을 뜻하는 `bio` 역시 마찬가지입니다.

> name: String! @unique

병원 이름 역시 `String`인데 끝에 `unique`가 붙어 있습니다.

병원 이름은 고유해야 하니 붙여 놓았습니다. 이렇게 할 시 같은 이름을 가진 병원을 또 하나 더 만들려 하면 "이미 존재하는 병원 이름입니다"며 에러가 뜨게 됩니다.

또한 `String` 뒤에 느낌표 (!) 가 붙어있는데, 이는 해당 요소가 필수라는 사실을 의미합니다. 병원이라는 데이터 객체를 만들 때엔 `name`이라는 필드에 무엇인가 반드시 필요하다는 의미입니다.

이메일과 연락처 역시 고유해야 하지만 필수는 아니기에 !는 붙이지 않았습니다.

#### 병원 사진 추가

데이터모델 파일 내에는 `file`이란 객체가 있습니다. 이 객체를 살펴보면

```js
type File {
  id: ID! @id
  url: String!
  post: Post @relation(name: "FilesOfPost")
  createdAt: DateTime! @createdAt
  updatedAt: DateTime! @updatedAt
}
```

이렇게 되어있는데요. 파일 url을 저장하고 있는, `post`와 연결되는 객체입니다. 파일 url을 전달하는 객체라 생각하시면 됩니다. 이론적으론 어떤 종류의 파일이건 url을 통해 전달할 수 있겠지만 일단은 이미지 url을 집어넣어 사진을 전달하는 용도로 쓸 수 있다 정도만 알면 될 것 같습니다.

병원 내 인테리어 사진 등을 정보 페이지에 띄워야 하니 병원 객체 안에 파일이라는 필드도 추가해줍니다. 마찬가지로 파일 객체 안에도 병원이라는 필드를 추가해줍니다.

```js
type Hospital {
  id: ID! @id
  location: String
  bio: String
  name: String! @unique
  email: String @unique
  contact: String @unique
  files: [File!]! @relation(name: "FilesOfHospital", onDelete: CASCADE)
}

type File {
  id: ID! @id
  url: String!
  post: Post @relation(name: "FilesOfPost")
  hospital: Hospital @relation(name: "FilesOfHospital")
  createdAt: DateTime! @createdAt
  updatedAt: DateTime! @updatedAt
}
```

병원과 파일 객체 안에 파일과 병원 필드를 추가했습니다. 하지만 `relation`을 비롯해서 생소한 내용들이 보이는데요. 더 자세히 살펴보겠습니다.

>     files: [File!]! @relation(name: "FilesOfHospital", onDelete: CASCADE)

- 병원이란 객체 안에 files란 필드는 파일들의 array를 가집니다. 따라서 `File`이 아닌 `[File!]!`을 사용해서 `array` 형태로 정의해줍니다.

- 여기서 우리는 `Hospital`과 `File` 간의 관계를 정의한다 볼 수 있는데요. 이렇게 한 객체를 다른 객체의 field로서 정의할 경우에 **prisma**에서 이 관계를 보다 명확히 정의해줄 수 있습니다.

- 관계의 정의는 `@relation(name: "~~~~~")`을 통해 이루어집니다. 각 관계에는 이 경우와 같이 이름이 필요합니다. 용도를 알 수 있도록 적당히 지어줍니다.

- 이 경우 병원 객체 내 `files`와 `File` 객체 내 `hospital`에 관계를 동일한 이름으로 (`@relation(name: "FilesOfHospital")`) 추가해줍니다.

- 사실 같은 종류의 관계가 여러개 있지 않는 이상 관계를 반드시 이름으로 정의해줄 필요는 없습니다. 예를 들어, 이따 소개할 두 필드 `staffs`와 `patients`는 둘 다 `User`의 `array`라서 관계 정의가 필요하지만, 병원이 참여하고 있는 채팅방들을 뜻하는 `rooms`는 `Room`이라는 객체의 `array`이지만 `Hospital`이 `Room`과 맺는 유일한 종류의 관계이기 때문에 별도의 관계 정의가 필요하지 않습니다.

- 그럼 우리는 왜 `files` 필드에 굳이 관계지정을 해주었느냐. `onDelete`기능을 활용하기 위해서입니다.

- `onDelete: CASCADE` 부분은 병원 데이터 객체가 삭제되었을 시 이 병원과 관계를 맺고 있던 파일들을 어떻게 처리할지를 정의합니다. 이 경우 `CASCADE`라 정의하였는데, 병원이 삭제될 시 이 병원과 관계를 맺고 있든 파일들도 함께 삭제한다는 의미입니다.

#### 병원 포스트 추가

마찬가지로 병원에서 올리는 포스트들도 있을테니 앞에서 파일을 추가한 것과 같은 요령으로 추가해줍니다.

```js
type Hospital {
  id: ID! @id
  location: String
  bio: String
  name: String! @unique
  email: String @unique
  contact: String @unique
  files: [File!]! @relation(name: "FilesOfHospital", onDelete: CASCADE)
  posts: [Post!]! @relation(name:"PostsOfHospital", onDelete: CASCADE)
}

type Post {
  id: ID! @id
  location: String
  caption: String!
  user: User @relation(name: "PostsOfUser")
  hospital: Hospital @relation(name:"PostsOfHospital")
  files: [File!]! @relation(name: "FilesOfPost", onDelete: CASCADE)

  (...이하 생략)
  }
}
```

마찬가지로 files 필드를 추가한 것과 같은 요령으로 Hospital 객체 내에 Post를 추가해줍니다.

이 경우 `@relation(name: "PostsOfHospital")`라는 관계를 추가해주었네요.

#### 병원 프로필 사진 추가

이제 병원의 프로필 사진을 추가할 차례입니다. `avatar`라는 이름으로 병원 객체 내에 필드를 하나 추가해줍니다.

```js
type Hospital {
  id: ID! @id
  avatar: String
    @default(
      value:"https://image.flaticon.com/icons/svg/1546/1546074.svg"
    )
  location: String
  bio: String
  name: String! @unique
  email: String @unique
  contact: String @unique
  files: [File!]! @relation(name: "FilesOfHospital", onDelete: CASCADE)
  posts: [Post!]! @relation(name:"PostsOfHospital", onDelete: CASCADE)
}
```

`avatar`은 `String`으로 병원 프로필 사진 url을 보관하는 필드입니다.

여기서 `@default(value: XXX)`은 해당 필드의 기본값을 지정해주는데, 저는 병원의 [벡터 이미지](https://image.flaticon.com/icons/svg/1546/1546074.svg)를 하나 골라서 넣어놓았어요.

#### 병원 소속 관리자, 의료진, 환자 명단

병원 소속 관리자나 의료진 명단, 환자 명단은 사용자, 혹은 사용자의 `array`로 정의할 수 있습니다

다음 필드들을 `Hospital` 객체 안에 넣어줍니다.

```js
  admin: User! @relation(name: "AdminOfHospital")
  staffs: [User!]! @relation(name: "StaffOfHospital")
  patients: [User!]! @relation(name: "PatientOfHospital")
```

- `admin`: 관리자입니다. 기본적으로 Hospital 객체를 만든 사용자를 해당 병원의 관리자로 설정합니다. (이 부분은 추후 `addhospital` mutation에서 설명하겠습니다.)
- `staffs` / `patients`: `User`의 `array`로 설정합니다.

이렇게 `Hospital`과 `User`간의 관계를 세개 만들었으니, `User` 객체 역시 수정해줍니다. `User`객체의 마지막 부분에 다음과 같은 필드 3개를 추가하였습니다.

```js
adminof: [Hospital!]! @relation(name: "AdminOfHospital")
staffof: [Hospital!]! @relation(name: "StaffOfHospital")
patientof: [Hospital!]! @relation(name: "PatientOfHospital")
```

- `adminof`: 사용자가 `admin`으로 있는 병원들의 array입니다.
- `staffof`: 사용자가 `staff`로 있는 병원들의 array입니다.
- `patientof`: 사용자가 `patient`로 있는 병원들의 array입니다.

---

#### 병원 데이터모델 (완성)

완성된 병원 데이터모델입니다.
(Post, File, User의 변경내용은 생략했습니다)

```js
type Hospital {
  id: ID! @id
  avatar: String
    @default(
      value:"https://image.flaticon.com/icons/svg/1546/1546074.svg"
    )
  location: String
  bio: String
  posts: [Post!]! @relation(name:"PostsOfHospital", onDelete: CASCADE)
  files: [File!]! @relation(name: "FilesOfHospital", onDelete: CASCADE)
  rooms: [Room!]!
  name: String! @unique
  email: String @unique
  contact: String @unique
  admin: User! @relation(name: "AdminOfHospital")
  staffs: [User!]! @relation(name: "StaffOfHospital")
  patients: [User!]! @relation(name: "PatientOfHospital")
}
```

이후 `prisma deploy`를 이용해 이 데이터모델을 프리즈마에 올리고 `prisma generate`를 통해 현 데이터모델에 상응하는 prisma client를 다시 생성했습니다.

### 2.2.2 models.graphql

이제 프리즈마에서 인지하는 데이터모델을 만들었으면, 이 데이터모델에서 정의한 데이터 type들을 똑같이 GraphQL에서도 정의해주어야 합니다.

`./api/models.graphql`:

이 파일에서는 우리가 GraphQL에서 사용하는 type들(User, Post, Like, 등등)을 정의합니다. 이때까지 만든 datamodel.prisma 파일과 거의 같습니다. 다만 `@relation`, `@unique` 와 같은 것들은 **GraphQL**이 아니라 **Prisma**의 문법이기 때문에 빼주어야합니다.

따라서 `./api/models.graphql`에 다음과 같은 type을 추가해줍니다.

```js
type Hospital {
  id: ID!
  avatar: String
  location: String
  bio: String
  files: [File!]!
  posts: [Post!]!
  rooms: [Room!]!
  name: String!
  email: String
  contact: String
  admin: User
  staffs: [User!]!
  patients: [User!]!
}
```

사실상 데이터모델에서 정의한 내용에서 프리즈마 문법만 뺀 내용입니다. `Hospital` 타입 말고도 변경된 다른 `type`들 (`User`, `Post`, `File`)에도 변화된 데이터모델을 반영하여 `models.graphql`을 수정해줍니다

그런데 실제 `models.graphql` 파일을 보면 다음과 같은 필드들이 더 있을겁니다.

```
patientsCount: Int!
staffsCount: Int!
isYours: Boolean!
```

이 필드들이 왜 들어가있고, 어디서 왔고, 무엇을 의미하는진 이따 computed field에 대해 설명할 때 추가로 설명하겠습니다.

---

## 2.3 Resolver 만들기

이제 데이터 모델을 완성하였으니 이 데이터들을 불러오거나 주무를 수 있는 **Resolver**들을 만들어보겠습니다. Resolver는 데이터 Query나 Mutation을 행하는 함수입니다. 아까 **GraphQL Playground**에서 다음과 같은 query를 실험해봤던 것 기억하시나요?

```js
query {
  seeUser (username:"ghouse") {
    id
    fullName
    bio
    createdAt
    adminof {
      id
      name
    }
    staffof {
      name
    }
  }
}
```

여기서 사용한 seeUser가 query를 해주는 resolver입니다. username이란 입력을 받아 해당 user의 데이터를 돌려주는 query를 만들 수 있도록 해주는거죠.

Resolver에는 두 종류가 있습니다.

1. Query: 데이터를 찾아옵니다. 위에 있는 seeUser의 경우가 대표적입니다.
2. Mutation: 데이터를 변화시킵니다. 삭제하거나, 수정하거나, 두 데이터를 연결해서 관계를 설정해주거나 할 수 있을겁니다.

이런 resolver들은 백엔드 폴더 내의 `./api/` 폴더 안에 다 정리되어 습니다. 저는 `./api/Hosptial` 폴더를 만들어 이 안에 병원과 관련된 모든 Resolver들을 넣어주겠습니다.

우선 새 병원을 추가하는 `addHospital` resolver를 만들어보겠습니다.

---

Resolver는 자바스크립트 코드와 GraphQL 코드 하나씩으로 이루어지는데, 저는 이 두 코드들을 포함할 `./api/Hosptial/addHospital` 폴더를 만들었습니다. (꼭 이렇게 Resolver별로 폴더를 만들 필요는 없는걸로 압니다. 하지만 이 편이 정리가 편한 것 같아요.)

### 2.3.1 addHospital.graphql

기본적으로 graphql 파일에서는 resolver의 input과 output을 정의합니다. 구조를 정의한다고 볼 수 있을 것 같습니다.

`./api/Hospital/addHospital/addHospital.graphql` 파일을 보시면 이렇게 되어있습니다:

```js
type Mutation {
  addHospital(
    name: String!
    email: String
    location: String
    contact: String
    bio: String
  ): Hospital!
}
```

- 새 병원을 추가하는 행위. 즉 기존 데이터베이스에 변화를 주는 행위를 하기 때문에 `type`은 `Mutation`입니다.

* Resolver의 이름을 정의해줍니다 (addHospital)

- Resolver의 input을 정의해줍니다. 이 경우엔 `name`, `email`, `location`, `contact`, `bio` 가 `String` 형태로 들어가네요. 여기서 `name`에는 `!` 표시가 붙어있어서 이 항목이 필수적으로 요구됨을 알 수 있습니다.

  - 저희가 아까 데이터모델의 정의할때 `Hospital` 타입에서 `name` 필드를 필수적으로 요구했던걸 기억하시나요? 그러니 마찬가지로 여기서도 `name`을 필수적으로 요구해줍니다. 그러지 않는다면 `Hospital` 데이터를 추가하려고 할때 필수항목인 name이 부재하다고 에러가 뜰거에요.

- Resolver의 output을 또 정의해줍니다. 이 경우에는 `Hospital!`입니다. 만들어진 병원 데이터를 `return`하여서 옳게 만들어졌는지 확인할 수 있도록 해보겠습니다.

이렇게 어떤 input이 addHospital resolver안에 들어가고 어떤 output을 받는지 그 구조를 정의했습니다. 이제 이 구조대로 input을 넣고 output을 받는 자바스크립트 함수를 만들어보겠습니다.

---

### 2.3.2 addHospital.js

`addHospital.js` 파일은 다음과 같이 되어있습니다:

```js
import { prisma } from "../../../../generated/prisma-client";

export default {
  Mutation: {
    addHospital: async (_, args, { request, isAuthenticated }) => {
      isAuthenticated(request);
      const { name, email = "", location = "", contact = "", bio = "" } = args;
      const { user } = request;
      console.log(user.id);
      return prisma.createHospital({
        name,
        admin: {
          connect: {
            id: user.id
          }
        },
        email,
        location,
        contact,
        bio
      });
    }
  }
};
```

하나하나 뜯어서 살펴볼게요.

```js
import { prisma } from "../../../../generated/prisma-client";
```

프리즈마 클라이언트를 불러오는 코드입니다.

```js
export default {
  Mutation: {
    addHospital: async (_, args, { request, isAuthenticated }) => {
      isAuthenticated(request);
```

- `export default`는 해당 자바스크립트에서 기본적으로 `export`하는 함수 혹은 객체 등을 정의해줍니다. 이 경우에는 당연히 `addHospital`이란 `mutation`이겠죠? 따라서 이런 식으로 정의해줍니다.

* `async`: `addHospital`은 asynchronous한 함수입니다. 자바스크립트에서 **비동기 처리** 란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미합니다.
  - 페이스북 페이지 등을 로드할 때 먼저 로드되는 애들이 있고 아닌 애들이 있습니다. 어떤 부분들이 로드되지 않았다 해서 로드된 부분의 기능에는 영향을 주지 않습니다. 이는 **비동기 처리**로 데이터를 불러 처리하기 때문에 가능한 일입니다.

- `async()` 안의 세 요소는 각각 ( `parent`, `args`, `context` ) 입니다.
  1. `parent`는 아래에서 computed field에 대해 이야기할 때 추가로 설명하겠습니다. 이 함수가 속한 객체의 상위 객체를 가져오는데, 이 경우엔 그런 상위객체가 존재하지 않습니다. 따라서 변수 이름도 딱히 없고 `_`로 되어있죠.
  2. `args`: 저희가 받아오는 input들이 모아져있는 객체입니다.
  3. `context`: `GraphQL Context`는 현 execution에서의 모든 resolver들에서 공유되는 객체들입니다. 주로 authentication이나 사용자 정보 같은 정보들을 주로 여기 담아 공유합니다. 저희 경우엔 `isAuthenticated`라는 함수와 `request`가 context로 전해졌습니다. 보다 자세한 내용이 궁금하시면 [GraphQL Context](https://graphql-modules.com/docs/introduction/context) 문서를 참고해주세요.

* `isAuthenticated`: 간단히 설명하자면 사용자에게서 온 요청을 받아서 이것이 로그인된 사용자에 의한 요청인지 아닌지를 판별해주는 함수입니다. 로그인을 요하는 기능들에 전부 붙어있습니다. (예를 들어 코멘트를 로그인 없이 남기면 안되니 해당 기능을 수행하는 resolver에도 이게 붙어있습니다.)

- `request`: 사용자에게서 온 요청입니다. 사용자가 누구인지 판별할 수 있는 JWT Token이 요청의 'header'에 담겨 오게 되는데요. header에 담긴 토큰을 해독해서 사용자가 로그인된 사용자인지 아닌지를 판별합니다. 자세한 내용은 [백엔드 리포지토리](https://github.com/slee333/prismagram)에서 **2.3.4** 를 참고해주세요.

이제 사용자가 로그인된 사용자인지 아닌지를 판별했습니다. 코드의 다음 부분으로 넘어가겠습니다.

```js
const { name, email = "", location = "", contact = "", bio = "" } = args;
const { user } = request;
console.log(user.id);
```

- `args`에서 input 값들을 다 가져옵니다. args 객체는 대충 `{ name="~~", email ="~~~" }` 이런 구조일텐데요. 자바스크립트 문법상 이런 경우

```js
const { name, email = "", location = "", contact = "", bio = "" } = args;
```

이런 방법으로 객체 안에 있는 필드들을 변수로 간편하게 빼와줄 수 있습니다.

햇갈리실거 같아 크롬 Developer Tool (구글 크롬 - F12)에서 간단한 예제를 만들어보았습니다.

![Imgur](https://i.imgur.com/clJ91vo.png)

여기서 a,b는 test라는 객체 안의 field입니다. 당연히 외부에는 a, b라는 변수가 존재하지 않죠. 하지만 test 내의 필드 a와 우리가 정의하고자 하는 변수 a의 이름이 일치하기 때문에, `const {a,b} = test` 라는 코드로 변수 a,b를 간편히 정의해줄 수 있습니다.

- 마찬가지로 `request`라는 객체 안에서 `user` 필드를 가져옵니다.

- console.log 부분은 제가 코드 잘 돌아가는지 보려고 넣은거니 무시해주세요. 나머지를 보겠습니다.

```js
return prisma.createHospital({
  name,
  admin: {
    connect: {
      id: user.id
    }
  },
  email,
  location,
  contact,
  bio
});
```

- Prisma client는 데이터모델이 만들어지면 기본적으로 각 데이터 타입을 (우리 경우엔 User, Hospital 등을) 만들거나, 업데이트하거나, 없애거나 하는 함수들을 만들어놓습니다.

- Prisma endpoint 링크로 들어가시면 어떤 기능들이 만들어져있는지 확인하실 수 있습니다. Prisma endpoint 링크는 Prisma admin으로 저희가 사용하는 서비스 안에 접속했을 시 왼쪽 하단에서 확인하실 수 있는데요.

![Imgur](https://i.imgur.com/IVGSSo7.png)

이 링크입니다. 이 링크를 클릭해서 복사할 수 있는데, 한번 복사해서 이 링크로 접속해볼게요.

![Imgur](https://i.imgur.com/LcCE9HS.png)

- Prisma endpoint 링크로 들어갔을 때 보이는 화면인데요. 오른쪽의 DOCS 버튼을 누르면 **Prisma client**에서 어떤 기본적인 함수들을 제공하는지 보실 수 있습니다.

- 여기서 `createHospital(...)`을 눌러보았습니다. 그러면 오른쪽 상단에서 `createHospital`이란 함수는 `HospitalCreateInput`, 즉 `Hospital` 객체를 구성하는 요소들을 `input`으로 받고, `Hospital` 객체를 return함을 알 수 있습니다.

* `prisma.createHospital()` 기능을 통해 `Hospital` 객체를 만들어주겠습니다. 안에 들어가는 데이터는 우리가 input으로 받은 내용들을 넣고요. 이 `addHospital`이란 `mutation`을 실행한 유저를 또 `admin`으로 포함시킵니다.

```js
  admin: {
    connect: {
      id: user.id
    }
  },
```

이 코드를 보시면 `connect`라는걸 볼 수 있는데요. `admin` 필드에는 `User`가 들어가지요? 간단히 생각하면 `user.id`를 가진 사용자를 admin 필드에 들어가는 사용자로 넣어주는 작업입니다. 단순한 definition이 아니라 connect인 이유는 relation 때문인데요.

`Hospital`의 `admin` 필드와 `User`의 `adminof` 필드는 연결되어 있습니다. 따라서 유저를 병원의 `admin`에 **`connect`** 시키면, 해당 `User`의 `adminof`에는 이 `Hospital`이 자동으로 들어가게 됩니다.

- createHospital() 함수는 Hospital 객체를 return해줍니다. 따라서

```js
return prisma.createHospital({ .... })
```

이런식으로 써주게 되면 prisma.createHospital로 만들어진 `Hospital` 객체가 자동으로 `return` 되게 됩니다.

정리하자면, `addHospital.js`는 우리가 graphql 파일에서 정의한 input들을 받고 프로세싱해서 output을 만들어주는 함수입니다. 이로서 Resolver 구성이 끝났습니다.

---

### 2.3.3 addHospital.js 시험해보기 (GraphQL playground)

이제 Resolver를 만들었으니 GraphQL playground에서 이 resolver가 잘 돌아가는지 시험해보겠습니다. localhost:4000을 통해 GraphQL playground에 접속합니다.

그리고 addHosptial resolver를 시험해봅니다. 예를 들어,

```js
mutation {
  addHospital(name: "Testopital", bio: "This is test") {
    id
    name
  }
}
```

이런 식의 mutaiton을 playground 내에 넣고 실행시켜볼 수 있겠죠. 한번 실행시켜 보겠습니다.

![Imgur](https://i.imgur.com/jJDJLum.png)

에러 메시지가 뜹니다. 잘 안보이실까봐 따로 적어보면:

```js
{
  "data": null,
  "errors": [
    {
      "message": "You need to log in to perform this action",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "addHospital"
      ]
    }
  ]
}
```

로그인을 해야 한다 합니다. 저희가 보낸 request의 header에 유저를 의미하는 Token이 없기 때문입니다.

하지만 GraphQL playground에는 이런 header를 만들수 있는 기능이 내장되어 있습니다. 방법은 다음과 같습니다.

저희가 GraphQL mutatino이나 query를 입력하는 칸 아래에 http headers라 써진 부분이 보이시나요?

![Imgur](https://i.imgur.com/zUPuIIR.png)

```
{
  "Authorization": "Bearer <JWT>"
}
```

여기서 `<JWT>` 자리에 Token을 집어넣어줍니다. Token은 프론트엔드에 접속하여 획득할 수 있습니다.

![Imgur](https://i.imgur.com/1Oq5cls.png)

위에서 로그아웃에 대해 이야기할 때 구글 크롬 Developer tool로 LocalStoarge를 확인해 token 값을 조회할 수 있었단 걸 기억하시나요? 여기서 토큰값을 얻어올 수 있습니다. 해당 토큰값을 `<JWT>` 자리에 넣고 addHospital을 다시 시험해봅니다.

![Imgur](https://i.imgur.com/upd3Tqh.png)

이런.. Unique constraint가 위반되었다 뜨네요 Contact에서.. 아마 addHospital에서 contact의 기본값을 ""로 넣어주었는데, 이것도 unique한 것으로 취급되어 기존에 입력한 다른 병원이 가진 기본 contact값 ""과 충돌하는 모양입니다. 나중에 수정해주어야겠어요. 우선 unique한 필드인 contact, email에 다른 value들을 넣고 진행합니다.

![Imgur](https://i.imgur.com/Nbavzjv.png)

이번엔 성공했습니다. Hospital을 만드는데 성공했어요.

Resolver들을 만들고 시험하실 때 이런식으로 하면 될겁니다.

---

## 2.4 Computed Field 만들기

`Computed Field`에 대한 설명을 이전에 적어놓았는데 찾기 힘든 위치에 적어놓은 것 같아 다시 여기다 적을게요.

`Computed Field`에 설명하기 전 `Fragments`에 대한 설명부터 하겠습니다.

### 2.4.1 GraphQL - Fragments

설명하기 앞서 저희가 참고하는 오픈소스에서는 `fragment` **기능을 사용하지 않습니다**.

`Fragment`가 수행하는 기능을 `Computed fields`로 대체하였기 때문인데요. 그래도 `Fragment`가 왜 필요한지 아시면 몇몇 코드들을 이해하는데 도움될거같아 설명을 남겨봅니다.

정확하게 `Fragment`는 재사용할수 있는 `query`의 파편이라 생각하시면 됩니다. 이 때문에 복잡한 `query`들을 간단하게 표현하는데 주로 쓰이지만, `query`의 무한 루프로 인해 서버에 과부하가 발생하는 막는 일에도 쓰입니다.

**GraphQL**에서 `user`의 `id`와 사용자이름을 `query`한다 치면은:

```js
query {
  user( id: ~~~ ) {
    id
    username
  }
}
```

이런식으로 하게 되는데요. 다음과 같은 상황을 상정해볼게요.

```js
query {
  user( id: ~~~ ) {
    id
    comments {
      id
      user {
        id
        comment {
          id
          user { ... }
        }
      }
    }
  }
}
```

이런식으로 `query`의 무한루프를 만들게 하는 상황을 GraphQL은 허용하지 않습니다. 실제로 이런식으로 `query`를 해보려 하면 오류가 뜰겁니다.

하지만 user.comment로 찾은 comment가 user를 return하지 않는다거나, user.comment.user가 comment를 return하지 않으면 이런식의 무한루프를 방지할 수 있겠죠. 이걸 가능하게 하는게 fragment입니다.

예시를 하나 들자면:

```js
// COMMENT_FRAGMENT를 지정해줍니다.
export const COMMENT_FRAGMENT = `
    id
    text
    user {
        ${USER_FRAGMENT}
    }
`;
// USER_FRAGMENT를 지정해줍니다.
export const USER_FRAGMENT = `
    id
    username
    avatar
`;

// 포스트에 달린 코멘트를 찾는 query가 있다고 칠게요.
export default {
  Query: {
    seeCommentsOnPost: async (_, args) => {
      const { id } = args;
      const post = await prisma.post({ id });
      return prisma
        .post({ id })
        .comments()
        .$fragment(COMMENT_FRAGMENT);
    }
  }
};
```

이렇게 되면 seeCommentOwner라는 query에서는 comment들의 id, text, 그리고 해당 코멘트를 적은 user의 id와 username들만 받게됩니다. id, text, username 등은 다 string이니 이 경우 무한루프가 발생할 수 없습니다.

이런 `fragment`들을 저희는 따로 사용하지 않고 대신 computed field 기능을 사용합니다. Computed field가 무엇인지 볼게요.

---

### 2.4.2 Computed Field

`./src/api/User/User.js`를 한번 보겠습니다.

```js
export default {
  User: {
    posts: ({ id }) => prisma.user({ id }).posts(),
    following: ({ id }) => prisma.user({ id }).following(),
    followers: ({ id }) => prisma.user({ id }).followers(),
    likes: ({ id }) => prisma.user({ id }).likes(),
    comments: ({ id }) => prisma.user({ id }).comments(),
    rooms: ({ id }) => prisma.user({ id }).rooms(),
    postsCount: ({ id }) =>
      prisma
        .postsConnection({ where: { user: { id } } })
        .aggregate()
        .count(),
```

이렇게 `User`에서 얻을 수 있는 정보들을 함수 형태로 지정해주는 것을 `User`의 computed field라고 합니다.

구조가 왜 저런식인지 햇갈리실텐데요. 원래 computed field의 구조는

```js
export default {
  Like: {
    post: ( parent, arguments, {request}) => prisma.like({ parent.id }).post(),
    user: ( parent ) => prisma.like({ parent.id }).user()
  }
};
```

이런식입니다. 보시면 아까 다룬 resolver의 js 파일과 구조가 유사합니다. 받는 input이 parent, arguments, context로 resolver와 같죠. Resolver의 js파일 구조를 아래 첨부합니다.

```js
export default {
  Mutation: {
    addHospital: async (_, args, { request, isAuthenticated }) => { .... } } }
```

저희가 필요한건 `parent`의 id 부분입니다. 따라서 `parent` 이후 `argument`, `context` 부분은 받지 않고, parent도 그 자체를 받는 대신 parent 안의 id만을 변수로 지정해 받아옵니다. 그러면 코드는 다음과 같습니다.

```js
export default {
  Like: {
    post: ({ id }) => prisma.like({ id }).post(),
    user: ({ id }) => prisma.like({ id }).user()
  }
};
```

물론 `parent`의 `id`만이 아니라 다른 필드들이 필요하면 이런 식으로 써줄수도 있습니다.

```js
export default {
  User: {
    fullName: parent => `${parent.firstName} ${parent.lastName}`
  }
};
```

이렇게 computed fields를 이용해서 `fragment` 사용을 피할 수도 있습니다. 또한 데이터 내 특정 필드의 갯수 등 유용한 정보들 역시 compute해서 불러올 수 있습니다. 직접 `Hospital.js`를 만드는 과정을 통해 알아보겠습니다.

### 2.4.3 Hospital.js Computed field 만들기

하나하나 살펴볼게요.

우선 prisma client를 불러와줍니다.

```js
import { prisma } from "../../../generated/prisma-client";
```

그리고 Hospital의 Computed field 작성을 위한 레이아웃을 잡아주고요.

```js
export default {
  Hospital: {

    }
  }
};
```

그리고 patient, staffs, rooms 등 다른 객체를 return해야 하는 query들을 우선적으로 computed field를 통해 제어해줍니다.

```js
export default {
  Hospital: {
    patients: ({ id }) => prisma.hospital({ id }).patients(),
    staffs: ({ id }) => prisma.hospital({ id }).staffs(),
    rooms: ({ id }) => prisma.hospital({ id }).rooms(),
    admin: ({ id }) => prisma.hospital({ id }).admin(),
    files: ({ id }) => prisma.hospital({ id }).files(),
    }
  }
};
```

이후 크게 두가지 기능을 추가하겠습니다. 하나는 환자와 스태프 숫자를 새는 computed field이고, 나머지 하나는 지금 접속한 `User`가 해당 병원의 `admin`인지 알아보는 기능입니다.

우선 카운트 기능부터 추가해보겠습니다.

```js
    patientsCount: ({ id }) =>
      prisma
        .usersConnection({ where: { patientof_some: {id } } })
        .aggregate()
        .count(),
```

이건 Prisma documentation에서 제공하는 count 기능의 응용판인데요. Prisma client에서 제공하는 함수 `usersConnection`은 특정 조건을 만족하는 `User`들을 `return`합니다.

가령, 여기에서 나온 조건 `usersConnection({ where: { patientof_some: {id } } })`은 `patientof` 필드에 병원 `id`를 갖는, 즉 해당 병원의 환자로 등록되어 있는 `User`들을 보여줄겁니다.

- patientof_some과 같은 조건들은 prisma client에서 자동생성됩니다. \_some, \_every, \_none 과 같은 argument들이 1 to N, 혹은 N to M 형태의 관계에선 자동으로 만들어지는데요. every, some, none은 각각 주어지는 조건이 related node의 전부, 일부, 혹은 none과 맞아떨어지는 경우를 의미한다고 [prisma documentation](https://www.prisma.io/docs/reference/prisma-api/queries-ahwee4zaey)엔 적혀있는데 깊이 이해는 못했습니다. count 할 때 \_some을 써서 할 수 있다 정도만 알고 넘어가면 될 거 같아요 일단은.

* 이렇게 해서 주어지는 결과를 `.aggregate()` 후 `.count()` 하면 저희가 의도한 해당 `Hospital`에 소속된 `patient` 숫자를 알 수 있습니다.

staffsCount 역시 동일한 방식으로 만들어집니다.

```js

    staffsCount: ({ id }) =>
      prisma
      .usersConnection({ where: { staffof_some: { id } } })
        .aggregate()
        .count(),
```

이제 isYours를 추가해볼게요. 병원의 admin이 나인지 아닌지 알아보기 위한 코드입니다.

```js
isYours: async (parent, _, { request }) => {
  const { user } = request;
  const { id: parentId } = parent;
  const ADMIN = await prisma.hospital({ id: parentId }).admin();
  return user.id === ADMIN.id;
};
```

우선 `user`를 `request`로부터 받아오고, `parent`의 `id`, 즉 병원의 `id`를 `parentId`란 변수로 받아옵니다.

이후 `prisma.hospital({ id: parentId }).admin();`을 이용해 병원의 admin인 User 정보를 찾아옵니다. 사실 이거보다 더 간단하게 할 수 있는 방법이 있을텐데 일단은 이렇게 쓰고있어요.

여기서 `prisma`를 통해 `User`를 찾아오는 과정이 즉시 완료되지 않으므로, `isYours`를 비동기 함수로 정의내려주고 (`async`) `ADMIN` 변수로 유저를 찾아 받아오는 동안 기다려줍니다. (`await`)

이후 ADMIN이 return 되면 request를 보낸 user의 Id와 ADMIN의 id를 비교하여 이를 Boolean으로 return합니다.

---

이렇게 해서 Hospital의 computed field 정의를 완료했습니다. 앞으로 필요에 따라 여기에 더 추가할수도, 뺄수도 있겠죠.

완성된 `Hospital.js`:

```js
import { prisma } from "../../../generated/prisma-client";

export default {
  Hospital: {
    patients: ({ id }) => prisma.hospital({ id }).patients(),
    staffs: ({ id }) => prisma.hospital({ id }).staffs(),
    rooms: ({ id }) => prisma.hospital({ id }).rooms(),
    admin: ({ id }) => prisma.hospital({ id }).admin(),
    files: ({ id }) => prisma.hospital({ id }).files(),
    patientsCount: ({ id }) =>
      prisma
        .usersConnection({ where: { patientof_some: { id } } })
        .aggregate()
        .count(),
    staffsCount: ({ id }) =>
      prisma
        .usersConnection({ where: { staffof_some: { id } } })
        .aggregate()
        .count(),
    isYours: async (parent, _, { request }) => {
      // 이 병원의 Admin이 나인지 알아보기 위한 코드. 수정이 필요함
      const { user } = request;
      const { id: parentId } = parent;
      const ADMIN = await prisma.hospital({ id: parentId }).admin();
      return user.id === ADMIN.id;
    }
  }
};
```

이렇듯 Resolver를 만들 때도 Computed field를 만들 때도 Prisma Client를 이용해야 하는데, 지금까지 저희 앱에서 다룬 형태 말고도 다른 형태가 필요한 경우도 있을 수 있습니다. 그럴 경우 [prisma documentation](https://www.prisma.io/docs/reference/prisma-api/queries-ahwee4zaey)을 참고해주세요. 1.14 버전 다큐멘테이션인데 어쩐지 최신 다큐멘테이션에선 Query를 찾을수가 없네요..

### 2.4.4 models.graphql 수정하기

아까 models.graphql 내에 computed field들을 넣어주어야 한다 말씀드렸습니다.

저희가 원래 있는 필드들 (rooms, admin, files, 등등)을 제외하면 총 3개의 필드를 추가했습니다. `patientsCount`, `staffsCount`, `isYours입니다`. 이제 이 세 필드를 `Hospital`의 필드로 `models.graphql`에서 추가해야합니다.

원래 `models.graphql` 내에 `Hospital`은 다음과 같이 정의되어 있었습니다:

```js
type Hospital {
  id: ID!
  avatar: String
  location: String
  bio: String
  files: [File!]!
  posts: [Post!]!
  rooms: [Room!]!
  name: String!
  email: String
  contact: String
  admin: User
  staffs: [User!]!
  patients: [User!]!
}
```

여기다 computed field에서 정의한 새 필드 3개를 추가합니다.

- `patientsCount`, `staffsCount`는 `Int`,
- `isYours`는 `Boolean`일 것입니다.

그러면 이렇게 되겠죠.

```js
type Hospital {
  id: ID!
  avatar: String
  location: String
  bio: String
  files: [File!]!
  posts: [Post!]!
  rooms: [Room!]!
  name: String!
  email: String
  contact: String
  admin: User
  staffs: [User!]!
  patients: [User!]!
  patientsCount: Int!
  staffsCount: Int!
  isYours: Boolean!
}
```

Required 표시 (`!`)를 붙여놓은 이유는 이 필드들은 별다른 input 데이터가 필요없이 계산을 통해 항상 값을 도출할 수 있는 필드들이기 때문입니다. 아마 Required 표시를 하지 않아도 상관없지 않을까 생각합니다.

**정리하자면 models.graphql 내에 정의되어야 하는 필드들은 다음과 같습니다:**

1. datamodel.prisma에서 정의한 필드

2) Computed field로 정의한 필드

---

이제 병원 프로필 페이지를 만들기 위해 필요한 백엔드 요소들은 다 만들었습니다. 이제 프론트엔드로 넘어가서 페이지를 직접 만들어 볼게요.

---

# 3 병원 프로필 컴포넌트 만들기 (프론트엔드)


현재 병원 프로필 컴포넌트는 프론트엔드 폴더 내의 `./src/Routes/HospitalProfile` 폴더 내에 들어있습니다.


컴포넌트를 구성하는데 필요한 코드 양이 많아 별도의 폴더를 구성해서 분리한건데요. 이렇게 하지 않고 파일 하나에 모든 코드를 다 넣어도 전혀 상관없습니다. 실제로 `./Routes/Feed` 같은 피드 보여주는 컴포넌트의 경우 한 파일에 모든게 구성되어 있어요.


컴포넌트 만드는 과정엔 크게 4가지가 있어요.


1. 컴포넌트에 접속 할 수 있는 URL 만들기
2. 컴포넌트에서 사용할 데이터를 불러오는 query 만들기
3. 데이터를 불러오기
4. 불러온 데이터를 이용해 실제로 페이지 구성하기

---

## 3.0 들어가기 전에


Visual Studio Code를 만일 사용하신다면 유용한 팁입니다. (다른 텍스트 에디터에도 유사한 기능이 있을 수 있어요)


프런트엔드 디자인을 할 때 저희가 필연적으로 많은 컴포넌트, 혹은 엘리먼트를 만들게 됩니다. 예를 들어 저희가 로그인을 한 후 Secret을 confirm하는 페이지를 만들 때에도:

```js
<Helmet>
  <title>Confirm Secret | Prismagram</title>
</Helmet>
<form onSubmit={onSubmit}>
<Input placeholder="Paste your secret" required {...secret} />
  <Button text={"Confirm"} />
</form>

```

이렇게 `Helmet`, `form`, `Button` 등 다양한 엘리먼트 혹 컴포넌트들이 사용되는데요. 이것들이 무엇을 하는 컴포넌트들인지, 어떤 파일에서 정의된건지 궁금하실 때 이걸 확인하는 쉬운 방법을 Visual Stuido Code는 제공합니다.


**해당 컴포넌트 이름 위에다 커서를 올리고 F12를 누르면 해당 컴포넌트가 정의된 부분을 보여줍니다.**


![Imgur](https://i.imgur.com/Te2yvDcm.png)


예를 들어, AuthPresenter.js에서 Button 위에 이렇게 커서를 올리고 F12를 누르면


![Imgur](https://i.imgur.com/PYPQKm6m.png)


이렇게 Button 컴포넌트가 정의된 Button.js 파일을 열어줍니다. 프론트엔드 페이지들에서 쓰인 요소들을 분석할 때 유용할거에요.


---

## 3.1 컴포넌트에 접근하는 Route (URL) 만들기

컴포넌트를 불러오는 과정을 보여드리기 위해 파일을 새로 하나 만들어볼게요.

Routes 폴더 안에 `Test.js`를 만들어줍니다. 그리고 그 안에 다음과 같이 써줄게요.

```js
export default () => "시험용입니다";
```

그리고 나서는 이 `Test.js`를 불러오는 url을 만들어주어야 합니다. `./src/Components/Routes.js`로 가실게요.

`Routes.js` 안에는 여러 요소들이 있습니다. 그 중 제일 주목해야 할건 `LoggedInRoutes`라는 함수인데요. 사용자가 로그인 했을시, 어떤 url을 타면 어떤 component를 볼 수 있는지를 정의합니다.

```js
const LoggedInRoutes = () => (
  <Switch>
    <Route exact path="/" component={Feed} />
    <Route path="/explore" component={Explore} />
    <Route path="/search" component={Search} />
    <Route path="/notifications" component={Notifications} />
    <Route path="/user/:username" component={Profile} />
    <Route path="/hospital/:name" component={HospitalProfile} />
    <Redirect from="*" to="/" />
  </Switch>
);
```

여기서 보면 보시다시피 `Feed`, `Explore`, `Profile` 등 다양한 컴포넌트들로 향할 수 있는 url들이 표시되어 있습니다.

예를 들어, `localhost:3000/#/explore`를 한다면 `explore` 컴포넌트로, `.../search`를 하면 `search` 컴포넌트로 안내받는 식이죠. (저 #이 왜 붙어야 하는진 아직 알아보는 중입니다.)

따라서 잠깐 동안만 여기다 `Route`을 하나 더 추가하겠습니다.

```js
import Test from "../Routes/Test";

const LoggedInRoutes = () => (
  <Switch>
    <Route exact path="/" component={Feed} />
    <Route path="/explore" component={Explore} />
    <Route path="/search" component={Search} />
    <Route path="/notifications" component={Notifications} />

    {/*요기!*/}
    <Route path="/test" component={Test} />

    <Route path="/user/:username" component={Profile} />
    <Route path="/hospital/:name" component={HospitalProfile} />
    <Redirect from="*" to="/" />
  </Switch>
);
```

Routes 폴더 안의 Test 컴포넌트를 import한 후, Route을 통해 로그인 이후 /test란 url이 주어지면 Test 컴포넌트를 보여주도록 설정하였습니다. 그러면 이제 프론트엔드로 돌아가 로그인 한 후 url에다 /test를 쳐보겠습니다. (로컬에서 돌릴 시 `localhost:3000/#/test`)

![Imgur](https://i.imgur.com/PqU3XWT.png)

그러면 이렇게 저희가 디자인한 컴포넌트가 페이지 상에 나타납니다!

이렇게 (되게 간단하게) 컴포넌트를 만들고 해당 컴포넌트를 보여주는 URL을 Route을 통해 설정해주는 법을 살펴보았습니다.

컴포넌트로 다른 컴포넌트를 불러올수도 있는데요. Test.js를 잠깐 수정해보겠습니다.

```js
import Notification from "./Notifications";

export default () => {
  return <Notification />;
};
```

Test.js가 들어있는 Routes 폴더에 있는 Notification.js 로부터 Notification 컴포넌트를 불러옵니다. 그리고 불러온 Notification 컴포넌트를 return합니다.

`Notification.js`는 다음과 같이 이루어져 있습니다.

```js
export default () => "This is notifications";
```

저희가 `Test.js`에서 Notification이란 컴포넌트를 return하니 아마 Test 컴포넌트를 다시 한번 (해당 URL로 접속해서) 봐주면 Notification 컴포넌트의 내용이 나타날텐데요. 다시 한번 해당 URL로 접속해보겠습니다.

![Imgur](https://i.imgur.com/v7Rd9zK.png)

오류가 떠있습니다. React를 import하지 않아서 뜨는 오류입니다. 방금 Test.js에서 저희가 return한 `<Notification/>` JSX를 사용해서 만들어진 리액트 엘리먼트입니다.

JSX는 자바스크립트의 확장 문법입니다. 저렇게 리액트 엘리먼트들을 사용할 수 있게 함으로서 UI 디자인을 보다 편하게 해주는데요. JSX가 무엇인지, 또 어떻게 사용하는지에 관한 내용은 필요하다면 [JSX 문서](https://ko.reactjs.org/docs/introducing-jsx.html#___gatsby)를 살펴보시면 될 것 같습니다.

다만 JSX 문서에서 리액트 엘리먼트를 렌더링하는 방식은 다소 복잡합니다. 저희는 `react-router-dom`이라는 라이브러리를 사용하기에 해당 문서에서 설명하는 것보단 보다 간편히 렌더링이 가능합니다. 이 부분에 대한 설명은 [이 링크](./Docs/3.1.JSXLibrary.md)를 참고해주세요.

아무튼 Test.js의 오류는 react를 import해주면 간단히 해결됩니다.

```js
import React from "react";
import Notification from "./Notifications";

export default () => {
  return <Notification />;
};
```

이렇게만 고쳐주면 localhost:3000/#/test url을 따라갈 시 아래와 같은 화면이 뜰겁니다.

![Imgur](https://i.imgur.com/JmKcDnj.png)

이렇게요.

---

지금까지 어떻게 컴포넌트에 접근하는 URL을 만들고, 컴포넌트 안에 다른 컴포넌트를 집어넣어 보여주는 과정을 간단하게 살펴보았습니다.

병원 프로필 페이지도 이때까지 설명한 것과 마찬가지 방법으로 호스팅됩니다. 차이가 있다면, 병원 프로필 페이지 url은 정해져 있지 않고 병원의 이름에 따라 유동적이란 점입니다. 이 점에서 사용자 프로필과 유사합니다.

병원 프로필 페이지로 향하는 Route은 다음과 같이 정의됩니다:

```js
<Route path="/hospital/:name" component={HospitalProfile} />
```

url이 `/hospital/:name`이란 사실을 확인할 수 있는데요. 이는 `/hospital/` 이후에 위치하는 String을 name이란 변수로 받아 HospitalProfile 이란 컴포넌트를 보여주는 방식입니다. 지금부터 좀 더 자세히 살펴보겠습니다.

---

## 3.2 컴포넌트 디자인: 개요

이제 Test.js와 관련된 코드들은 삭제하고 본격적으로 HosptialProfile 컴포넌트를 살펴보도록 할게요.

우선 `./src/Routes/HospitalContainer` 폴더로 가시면

1. index.js
2. HospitalProfileContainer.js
3. HospitalProfilePresenter.js

이 세 파일이 있습니다. 각각 어떤 역할을 맡고있냐 하면...

1. index.js:
   - HospitalContainer를 export합니다.

2) HospitalProfileContainer.js:
   - URL로부터 변수를 받습니다. (이 경우엔 URL에 주어지는 `name`)
   - 병원 프로필을 보여주는데 필요한 데이터를 불러옵니다. 이 경우엔 seeHospital이란 Resolver를 이용합니다. (그냥 Hospital 객체의 name을 넣어주면 해당 Hospital 객체를 return하는 아주 간단한 resolver입니다.)
   - 데이터를 불러오는 중인지 알려주는 Loading과 실제 병원의 데이터인 data를 갖게 되는데, 이 두 정보를 HospitalProfilePresenter에 넘겨줍니다.
   - 위 세가지 행동을 모두 행하는 함수를 export합니다.

3. HospitalProfilePresenter.js
   - 실제 병원 프로필을 꾸미고 보여주는 코드입니다.
   - 각 컴포넌트들을 스타일링합니다.
   - Container에서 받은 데이터들을 기반으로 컴포넌트들을 배치합니다.

각각 이 정도 역할을 맡고 있습니다.

대형 컴포넌트의 구조가 꼭 이렇게 정형화되어있지는 않습니다. 예를 들어 Container에선 query를 정의해주게 되는데 이런 query가 너무 길어지게 되면 다른 파일로 분리할 수도 있겠죠. (`./src/Routes/Auth` 참조)

그러면 이제 Container와 Presenter에 있는 코드들을 설명하도록 하겠습니다. 저도 처음부터 다 만든게 아니고 `./src/Routes/Profile` 에서 파일들을 긁어와 수정하였습니다.

---

## 3.3 컴포넌트 디자인: Container

HospitalProfileContainer.js를 설명해볼게요.

### 3.3.1 Query

우선 이 코드의 역할은 서버로부터 URL에 주어진 `name`과 같은 `name`을 갖는 `Hospital` 객체를 찾아오는 것입니다. 때문에 query를 정의 해 줍니다.

```js
import { gql } from "apollo-boost";

const GET_HOSPITAL = gql`
  query seeHospital($name: String!) {
    seeHospital(name: $name) {
      id
      name
      bio
      files {
        url
        id
      }
      location
      staffs {
        id
        avatar
        fullName
        username
        isSelf
        bio
      }
      admin {
        id
        avatar
        fullName
        username
        isSelf
        bio
      }
      isYours
      staffsCount
      patientsCount
    }
  }
`;
```

이게 아폴로를 이용해 GraphQL query를 짜는 방식입니다.

아폴로에서 `gql` 함수를 불러온 후, gql`` <- 이 사이에 우리가 불러오기를 원하는 GraphQL query나 mutation을 써넣어주면 됩니다. GraphQL Playground에서 resolver를 사용하는 방식과 거의 흡사합니다.

- `gql` 함수는 우리가 정의한 String 형태의 query를 parse해서 query document로 만들어줍니다.

위 경우에는 seeHosptial이란 query를 해주는 resolver를 사용해서 병원의 데이터를 받아오는 query를 만든 모습입니다. 저기 `$` 표시는 왜 쓰는건지 저도 정확히는 모르지만 [아폴로 문서](https://www.apollographql.com/docs/react/data/queries/)에 저런 식으로 되어있습니다.

제 생각에는 나중에 받아오는 변수를 뜻하는 거 같은데요. `query seeHospital($name: String!)` 부분에서 변수가 String이 맞는지 확인하고, `seeHospital(name: $name) {...}` 부분에서 name 필드에 변수로 주어진 name을 넣어 (`$name`) query를 진행하는 것 같습니다만 공식 문서에서 해당 내용을 찾지는 못했습니다. 그냥 제 추측입니다.

아무튼 이렇게 만들어진 query는 나중에 useQuery를 이용해서 사용할 수 있습니다. 지금 해당 내용을 보실게요.

---

### 3.3.2 HospitalProfilePresenter return하기

`HospitalProflieContainer.js`의 마지막 부분은 이렇게 구성되어 있습니다.

```js
export default withRouter(({ match: { params: { name } } }) => {
  const { data, loading } = useQuery(GET_HOSPITAL, {
    variables: { name }
  });

  return (
    <HospitalProfilePresenter loading={loading} data={data} />
  );
});
```

보시면 함수의 input 부분이 상당히 복잡한 모습을 보실 수 있습니다. withRouter 함수의 기능은 [이 링크](https://stackoverflow.com/questions/53539314/what-is-withrouter-for-in-react-router-dom)에 설명되어 있는데요. header처럼 모든 페이지에 존재해 원래라면 사용자를 redirect 할 수 없는 컴포넌트가 사용자를 redirect 할 수 있도록 하기 위해서 쓰인다 합니다.

지금 사용하고 있는 HospitalProfileContainer의 경우 Header처럼 모든 페이지에 존재하지는 않지만, parameter로 주어지는 name에 따라 다른 페이지를 랜더링해야 하기 때문에 withRouter 기능을 쓰지 않았나 생각합니다. 이 부분은 더 공부해보고 나은 설명이 있으면 추가하겠습니다.

아무튼 함수를 하나하나 뜯어보면,

```js
export default withRouter(({ match: { params: { name } } }) => { ... }
```

withRouter를 사용해 URL로부터 input을 받아올 시

```js
{
  match: {

    params: {

        name: "병원이름",
        other: "...",
        info: "..."
        (...)

      } ,

    otherfield:"..." ,
    (...)

    }
}
```

이런 식으로 input이 주어집니다. 하지만 저희가 필요한건 name밖에 없으니, 따라서 몇 겹의 객체들 안에 싸여 있는, 저희가 사용해야하는 변수 `name`을 바로 빼주기 위해 `{ match: { params: { name } } }` 이란 형태로 input을 정의해주었습니다.

```js
export default withRouter( ( input ) => {
  const name = input.match.params.name
  ...
  }
```

이렇게 input을 통째로 받아와서 그 안에서 `name`이란 필드를 찾아 변수를 만들어주는 것과 다르지 않습니다.

다음 부분을 살펴볼게요.

```js
const { data, loading } = useQuery(GET_HOSPITAL, {
  variables: { name }
});
```

앞서 저희가 `GET_HOSPITAL`이란 query를 정의하였습니다. 이 query를 사용해서 병원 데이터를 불러옵니다. useQuery 라는 함수를 사용합니다.


```js
useQuery(사용자_정의_Query, { variables: { variable } });
```


useQuery는 두 input을 받습니다. 첫번째는 사용하고자 하는 query이고, 그 query에 들어가는 variable들을 객체 형식으로 뒤에 넣어줍니다. `GET_HOSPITAL` query의 경우 name을 넣어주니 variable에도 name을 넣어줍니다.


useQuery 함수는 두가지를 return하는데요, 하나는 Query의 결과로 받아온 데이터. 다른 하나는 해당 데이터가 로드되었는지의 여부입니다. 각각을 `data`, `loading`이라는 변수로 받아왔습니다.


그러면 이제 받아온 데이터와 로딩 여부를 바탕으로 본격적으로 페이지를 만들어줄 차례입니다. 앞서 페이지에서 보여지는 element들이 들어있는 곳은 `HospitalProfilePresenter`라고 말씀드렸죠? `HospitalProfilePresenter` 컴포넌트에 `loading`과 `data`라는 `props`를 전달하고, 본격적으로 페이지 디자인을 시작합니다.


`props`는 부모 컴포넌트가 자식 컴포넌트에게 전달하는 값이라 생각하면 될 것 같아요. 도움 될 만한 [문서](https://velopert.com/3629) 첨부합니다.



### 3.3.3 propTypes


HosptialPresenter의 경우 PropTypes를 필요로 하지 않지만, 어떤 컴포넌트의 경우 PropType을 정의해줘야 하는 경우가 있습니다.


`FatText`라는 컴포넌트를 한번 볼게요.


```js
import React from "react";
import PropTypes from "prop-types";
import styled from "styled-components";

const Text = styled.span`
  font-weight: 600;
`;

const FatText = ({ text, className }) => (
  <Text className={className}>{text}</Text>
);

FatText.propTypes = {
  text: PropTypes.string.isRequired
};

export default FatText;
```


FatText의 실사용례는 다음과 같습니다.
```js
<FatText text={ "텍스트"  } />
```


이렇게 `text`란 `prop`을 부모 컴포넌트에서 `FatText` 컴포넌트에게 전달하면, `FatText`는 해당 텍스트를 font-weight이 600인 텍스트로 바꾸어 돌려줍니다. 한마디로 더 진하게 만들어주는데요.


이 경우 FatText는 Text라는 prop을 받기에 propTypes를 정의해주어야 합니다. 코드의 이 부분과 같습니다.


```js
FatText.propTypes = {
  text: PropTypes.string.isRequired
};
```


`FatText` 안에 들어가는 `prop`인 `text`는 `string`이어야만 하고, 필수적으로 주어져야한다는 내용이 정의되어있습니다.


병원 프로필 컴포넌트는 url에서 자동으로 input을 받아오는 `withRouter`을 사용해서 이렇게 `prop`과 `proptypes`를 정의해줄 필요가 없었지만, 혹시 이렇게 `prop`을 다루는 컴포넌트를 만들 땐 `propTypes`의 정의가 필요합니다.


---


## 3.4 컴포넌트 디자인: Presenter


`HospitalProfilePresenter` 문서를 한번 보겠습니다. 문서가 너무 길어서 전부 다 여기다 옮기지는 못하지만 일단 부분부분 살펴보도록 할게요.


### 3.4.1 라이브러리 살펴보기


우선 병원 프로필 페이지에서 import하는 라이브러리를 한번 살펴보겠습니다.


```js
import React, { useState, useEffect } from "react";
import styled from "styled-components";
import { Helmet } from "rl-react-helmet";
import Loader from "../../Components/Loader";
import Avatar from "../../Components/Avatar";
import FatText from "../../Components/FatText";
import FollowButton from "../../Components/FollowButton";
import SquarePost from "../../Components/SquarePost";
import Button from "../../Components/Button";
```

- `useState`: `State`은 컴포넌트에서 관리하는 상태 값으로, 유동적인 데이터를 다룰 때 주로 사용합니다. useState은 state을 쉽게 관리할 수 있도록 도와줍니다.

    - 원래는 State을 정의할때 보다 복잡한 코드를 사용해야 했지만 최신 버젼 리액트는 **Hooks** 란걸 제공해서 보다 쉽게 이런 작업들을 행할 수 있도록 해줍니다. [State Hooks 관련 문서](https://ko.reactjs.org/docs/hooks-reference.html#usestate)

    - `useEffect`도 `useState`과 같이 Hooks에 속하는데요. 병원 프로필 페이지에서는 상단에서 사진의 프로필 페이지를 슬라이드하는데 쓰입니다. 역시 [관련 문서](https://ko.reactjs.org/docs/hooks-reference.html#useeffect)입니다.

- `styled`: 리액트를 사용한 프런트엔드를 만들 때 엘리먼트들의 스타일을 보다 쉽게 지정할 수 있도록 도와줍니다. 기존 HTML - CSS를 사용한 방식에서 한 `<div> ` 엘리먼트에 스타일을 지정하려고 하면,

```html
<div id="testId" class="testClass">
  Hello World!
</div>
```

이렇게 HTML 파일 안의 `div` 엘리먼트 안에 class, 혹은 id를 지정하고, css 파일을 따로 만들어

```css
#testId {
  border: 2px;
}

.test {
  background-color: red;
}
```

이런 식으로 id와 class를 가진 엘리먼트를 어떻게 스타일링할지 따로 지정해주어야 했습니다. 하지만 저희가 사용하는 `styled component`는 이 작업을 보다 간단하게 수행할 수 있습니다. 

예를 들어 `HospitalProfilePresenter` 안에는 `Files`라 이름붙은 div이 있습니다. 이 div을 정의하고 스타일링하는 과정을 styled component는 간단히 수행할 수 있어요.


``` js
const Files = styled.div`
  position: absolute;
  left: 20%;
  top: 0%;
  width: 60%;
  z-index: -100;
`;
```

이렇게 Files를 지정한 css 스타일을 갖는 div 엘리먼트로 지정해주는거죠. 이후 이 Files란 div 엘리먼트를 실제로 페이지 안에 집어넣는 과정도 간단합니다.


```js
        <Files>
          {files &&
            files.map((file, index) => (
              <File
                key={file.id}
                src={file.url}
                showing={index === currentItem}
              />
            ))}
        </Files>
```

이렇게 HTML 태그처럼 (`<Files>  ...  </Files>`) 넣어줄 수 있는거죠.


---

### 3.4.2 Loader


이제 HospitalPriflePresenter 에서 사용하는 기본적인 라이브러리들을 살펴보았으니 실제 페이지 디자인과, 각 디자인에 관여하는 컴포넌트들을 살펴볼게요.


![Imgur](https://i.imgur.com/dGom114l.png)


파일의 첫 부분은 styled component를 사용해서 여러 엘리먼트들을 정의내리는 부분입니다. 이 부분은 생략하도록 하겠습니다. 그 다음 실제로 컴포넌트를 `export`하는 부분을 살펴볼게요.


```js
export default ({ loading, data }) => {
  if (loading === true) {
    //  로딩중이라면 로딩화면!
    return (
      <Wrapper>
        <Loader />
      </Wrapper>
    );
  } else if (!loading && data && data.seeHospital) { ... }
    
```


아까 Container에서 Presenter로 전달한 Props에는 두가지가 있었습니다. Loading과 data. 이 두 Props는 한 객체에 담겨오게 됩니다. 이 객체에서 loading과 data를 받아오는 부분이 상단 코드의 첫줄입니다. 좀 더 이해하기 쉽게 옮겨적으면 아래 코드와 같은 식이 되겠네요.


```js
export default ( props ) => {
  const loading = props.loading;
  const data = props.data;

  if (loading === true) { ... }
```


앞서 `Loading` 이라는 변수는 data가 로드되었는지 유무를 알려주는 Boolean이라 말씀드렸습니다. 아직 데이터가 로딩중이라면 병원 프로필 페이지를 띄워도 보여줄 수 있는 내용도 없고 오류가 뜰테니, `Loading`일 `true`일 경우 `Loader`라는, 로딩화면을 띄우는 컴포넌트를 보여줍니다. 그게 아래 코드입니다:

```js

if (loading === true) {
    //  로딩중이라면 로딩화면!
    return (
      <Wrapper>
        <Loader />
      </Wrapper>
    ); 
  }

```

- Wrapper: 말 그대로 우리가 페이지에서 보여주는 모든 컴포넌트들을 감싸주는 컴포넌트입니다. 상위에 위치해 있죠. 인스타그램에서 우리가 보는 모든 요소들이 가운데에 정렬되어 있는데, 이는 모든 요소들보다 상위에 위치하는 Wrapper가 요소들이 가운데에 정렬되도록 잡아두고 있기에 가능합니다.

- Loader: `./src/Components/Loader.js`에 존재하는 컴포넌트입니다. 단순한 컴포넌트로, 인스타그램 마크가 일정 시간 간격을 두고 깜빡이게 됩니다. Loader 구조에 대해서는 여기 [링크](./Docs/Loader.md))에 자세히 적어놓았습니다.

---
###  3.4.3 데이터 불러오기

이제 다음 코드를 살펴보겠습니다.

```js
else if (!loading && data && data.seeHospital) {
    //  로딩도 완료되고, 데이터도 넘어왔고 한다면 사용자의 프로필을 만들어줍니다.
    const {
      seeHospital: {
        id,
        name,
        bio,
        files,
        location,
        staffs,
        admin,
        isYours,
        staffsCount,
        patientsCount
      }
    } = data;
```


로딩이 완료되었을 경우, `data`란 `prop`에서 우리가 필요한 데이터들을 뽑아줍니다. `data`라는 객체 안에 (seeHospital이란 resolver를 이용해서 받아온 데이터임으로) `seeHospital`이란 객체가 있고 그 객체 안에 `id`, `name` 등 다양한 데이터들이 들어있는데요. 그 데이터들을 받아오는 과정입니다.


지금은 병원 객체를 받아왔으니 `admin`, `location`, `staffs` 등 병원 객체 안의 필드들을 받아왔지만 받아오는 객체에 따라 다른 필드들을 받아올수도 있습니다.

---

### 3.4.4 Slider (1)


코드의 다음 부분은 병원 프로필 페이지 상단에서 돌아가는 슬라이더를 만드는 부분입니다.


```js
    const [currentItem, setCurrentItem] = useState(0);
    const slide = () => {
      const totalFiles = files.length;
      if (currentItem === totalFiles - 1) {
        setTimeout(() => setCurrentItem(0), 3000);
      } else {
        setTimeout(() => setCurrentItem(currentItem + 1), 3000);
      }
    };
    useEffect(() => {
      slide();
    }, [currentItem]);
```


- useState은 `currentItem`이라는 state과, `currentItem`을 지정해줄 수 있는 함수 `setCurrentItem`을 만들어줍니다.
    - useState으로 state을 만들어줄 때, 해당 state의 시작값을 지정해주어야 합니다 여기서는 0을 지정해주었네요.
    - `currentItem`이란 state은 병원 상단에서 사진을 슬라이드시킬 때 어떤 사진을 보일지 지정해줍니다.


저희가 `seeHospital`을 통해 받아오는 정보들 중 `files`가 있습니다. `File`이란 객체들이 들어있는 `array`인데요. `slide` 함수는 이 array의 길이 범위 안에서 `currentItem`을 실행 시점부터 3초 이후에 1을 올려줍니다. 만약 `currentItem`이 파일의 갯수 - 1 이라면 1을 올리는 대신 `currentItem`을 0으로 만들어주죠.


좀 더 자세히 뜯어보면:


```js
    const totalFiles = files.length;
```

파일들이 전부 몇개인지 `files.length`를 통해 받아옵니다. (자바스크립트에서 Array 안에 들어있는 element들의 갯수를 받아오는 방법입니다.)


```js
    if (currentItem === totalFiles - 1) {
      setTimeout(() => setCurrentItem(0), 3000);
    } 
```

이후, `currentItem`이 `totalFiles`보다 하나가 모자라다면, 3000 ms (=3초) 이후 currentItem을 setCurrentItem을 이용해 0으로 맞춰줍니다.


```js
      else {
        setTimeout(() => setCurrentItem(currentItem + 1), 3000);
      }
```

만일 `currentItem`이 `totalFiles` - 1보다 작다면, 3초 간격으로 `setCurrentItem`을 이용해 `currentItem`을 1씩 늘려줍니다.


여기까지 읽으셨으면 `currentItem`을 `Files`란 array 안에 존재하는 파일을 특정하는 인덱스로 활용한다는 사실을 눈치채셨을 것 같습니다. 실제로 병원 프로필 상단의 사진 슬라이드는 `currentItem`을 인덱스로 활용해서 해당 사진을 보여주는 방식으로 만들어져 있습니다. 때문에 3초 간격으로 사진들이 바뀌는 것이죠. (추후에 이 부분은 수정할지도 모릅니다. 직접 수동으로 슬라이드 가능하도록.) 


```js
    useEffect(() => {
      slide();
    }, [currentItem]);
```

여기 정의된 `useEffect`는
1. 처음 페이지가 render되었을 때
2. 컴포넌트가 업데이트되었을 때. 여기서는 currentItem이란 State이 업데이트 되었을 때.


이 떄 실행되는 함수를 생성합니다. 이 경우엔 앞서 이야기한 `slide()` 함수를 실행하는데요. 따라서 1) 처음 페이지가 render 되었을 때, 2) 이후 3초마다 `currentItem`이 업데이트 될 때마다 useEffect가 slide()함수를 실행하며 `currentItem`을 0부터 totalFiles - 1까지 변화시킨다는 것을 확인하실 수 있습니다.

---

### 3.4.5 본격적인 페이지 디자인


드디어 본격적인 페이지 디자인입니다.


HospitalProfileContainer가 return하는 리액트 엘리먼트는 [다음](./Docs/HospitalProfilePresenter.md)과 같습니다. 너무 길어서 문서는 분리했습니다. 


우선 Presenter 안의 요소들이 각각 어떤 기능을 하는지 간단히 살펴볼게요.


- `<Wrapper>` 엘리먼트는 아까 `Loader` 설명할때도 했지만 모든 엘리먼트들을 감싸는 역할을 합니다. 모든 엘리먼트 상위에 위치하며 내용을 가운데로 정렬해줍니다.


- `<Helmet>`: 우리가 브라우저를 켜면 상단 탭에 페이지 제목이 보입니다. 이렇듯 페이지 타이틀이나 meta 태그와 같은 요소들은 react에서 관리되는 요소들이 아니라 좀 복잡한 코드를 입력해야 하는데요. `react-helmet`이란 라이브러리에서 제공하는 `Helmet`은 그럴 필요 없이 리액트 컴포넌트 렌더링하듯이 바로 페이지 타이틀 등을 지정할 수 있도록 해줍니다. 자세한 설명은 [링크의 3-7 부분](https://velopert.com/3425)을 참고해주세요.


실제 사용은 다음과 같이 합니다.


```js
<Helmet>
  <title>{name} | H+ground</title>
</Helmet>
```


이렇게 해 주고 병원 프로필 페이지를 보시면 



이렇게 Helmet 안에 title을 지정한데로 페이지 제목이 표시되는 것을 보실 수 있습니다.


그 아래를 보시면 Files 부분이 있는데 이건 추후에 설명할게요. 앞서 말씀드린 slide를 시키는 부분이란것만 지금은 아시면 될거같아요.


- `<Header>`: 프로필 페이지 상단에 나타나는 부분입니다. 병원 정보와 스태프 숫자 등이 표시되는 부분인데요.

    - `HeaderColumn`: Header는 `HeaderColumn`이라는 `div`으로 구성되어 있습니다. 그리고 이 `HeaderColumn`은 총 2개가 있는데, 그 중 하나에는 사용자 이름과 병원에서 일하는 사람들 수 등이 들어가고 나머지 하나에는 버튼이 들어가있습니다.


      - `UsernameRow` 역시 그냥 `div`입니다. 사용자 이름을 넣을 행과, 병원의 staffsCount, patientsCount 등을 넣을 행을 구분하기 위해서 만들었어요.


      - `UsernameRow`의 스타일링을 살펴보면 ,`display: flex;` , `align-items: center;` 등의 내용이 있는데, 간단히 말해 flex를 이용해 UsernameRow의 width를 HeaderColumn의 너비와 같게 만들어 공간을 확보하고, UsernameRow 안의 모든 내용을 가운데에 정렬했다 보시면 될 거 같아요.


      - 이런 스타일링은 일부는 처음부터 알고 하지만 일부는 일단 엘리먼트들을 넣어놓고 구글 개발자 툴을 이용해 스타일을 부여해가며 제가 원하는 스타일이 나올때까지 맞춰줍니다.


```js
<UsernameRow>
  <Username>{name}</Username>{" "}
</UsernameRow>
```

UsernameRow는 Username을 담고 있지요. 이걸 이용해서 병원에서 받아온 `name`을 표시해줍니다.
  

다른 엘리먼트들도 내용은 비슷합니다.


- Counts: ul (unordered list)로, 밑에 하위의 `Count`라는 list item을 지니고 있습니다. 말이 어려운데, 간단히 말해 [list 엘리먼트](https://www.w3schools.com/html/html_lists.asp)를 만들었다 보시면 될 것 같아요.
  - 이 안에 FatText라는 컴포넌트를 사용해 병원의 의료진 숫자와 환자들 숫자를 표시해줍니다.
  - `<FatText>` 컴포넌트는 텍스트를 props으로 주면 해당 텍스트를 진한 글씨로 렌더링해주는 컴포넌트입니다. (`./src/Components/FatText.js` 참고)


```js
<Counts>
  <Count>
    <FatText text={String(staffsCount)} /> Staffs
  </Count>
  <Count>
    <FatText text={String(patientsCount)} /> Pts
  </Count>
  <Count>
    위치: <FatText text={String(location)} />
  </Count>
</Counts>
```


따라서 이런 식으로 `<Counts>` 라는 ul 엘리먼트 안에 3개의 리스트 엘리먼트 `<Count>`를 넣고, 그 안에 각각 데이터로부터 받아온 staffsCount, patientsCount, location 값을 넣었습니다. 자바스크립트 변수를 넣을땐 저렇게 { } 중괄호 안에 넣어주어야 합니다.


![Imgur](https://i.imgur.com/NVLQj9o.png)


그 결과 이런 메뉴가 완성된거죠.


그런데 이 메뉴 디자인이 너무 심심하다 싶으면 저희가 만져줄 수 있습니다. 크롬 개발자 도구를 한번 이용해볼텐데요. 구글 크롬의 경우 이 메뉴를 `우클릭 - 검사` 를 누르면


![Imgur](https://i.imgur.com/c4Ov6or.png?1)


개발자 메뉴 내에서 해당 요소를 볼 수 있습니다. 여기서 저는 list들 중 하나를 선택해서 텍스트 색깔을 붉은색으로 바꾸어 볼게요


![Imgur](https://i.imgur.com/gi3JRUc.png)


우측 하단에서 제가 선택한 list에 `color:red`를 부여했더니 색깔이 바뀐 모습을 확인하실 수 있습니다. 이와 같이 개발자 메뉴를 이용해서 css 스타일링을 디버깅할 수 있어요. 보다 자세한 내용은 [이 링크](http://comajava.blogspot.com/2013/11/chrome-css.html)를 참고해주세요. 직접 해보시면 이해하기 정말 쉬울겁니다.


나머지 내용은 크게 특별한게 없습니다. 그냥 여러 div 엘리먼트들을 생성해서 아까 받아온 데이터들을 넣어준 작업의 반복이고, 읽어보면 바로 아실거에요.


그런데 그 중 하나 추가적인 설명이 필요한 부분이 `map function`인데, 아까 설명을 미루었던 `<Files>` 태그를 살펴볼게요.


```js
<Files>
  {files &&
    files.map((file, index) => (
      <File
        key={file.id}
        src={file.url}
        showing={index === currentItem}
      />
    ))}
</Files>
```


여기서 `files`는 아까도 말씀드렸듯 `File` 개체들이 들어있는 Array입니다. Array에서 map 함수는 **Array 내 각 요소들에 대해 callback function을 수행합니다.**
[자바스크립트 콜백함수 이해하기](https://yubylab.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EC%BD%9C%EB%B0%B1%ED%95%A8%EC%88%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)


이 경우, `files.map( (file, index) => {...} )`라는 함수는 files 내의 모든 file에 대해 {...} 안에 있는 내용을 수행하게 되죠. 내용을 한번 볼까요?


```js
files.map((file, index) => (
<File
  key={file.id}
  src={file.url}
  showing={index === currentItem}
/>
)
```


files 안의 모든 file에 대해 `<File>`이란 엘리먼트를 만들어줌을 알 수 있습니다. File 엘리먼트에 `file`의 `url`을 `src`라는 이름으로 넘겨주고, index가 currentItem과 match 하는지 여부를 `showing`이란 이름으로 전달하는 것 역시 알 수 있는데요. `File` 엘리먼트를 살펴보겠습니다.


```js
const File = styled.div`
  max-width: 100%;
  width: 100%;
  height: 300px;
  position: absolute;
  top: 0;
  background-image: url(${props => props.src});
  background-size: cover;
  background-position: center;
  opacity: ${props => (props.showing ? 1 : 0)};
  transition: opacity 0.5s linear;
`;
```


styling 부분은 따로 특이할게 없습니다. 주목해야 할 부분은 background-image 부분과 opacity 부분인데요. 


- background-image: 앞서 src로 넘겨주었던 이미지 url을 이용해서 File의 배경 이미지를 설정해주는 부분입니다.


- opacity: 아까 files.map에서 index가 `currentItem` 이란 `state`과 동일한지를 Boolean으로 넘겨주었습니다. 이게 true면 opacity는 1, 아니라면 opacity가 0이 됩니다.
    - 앞서 currentItem은 0에서 파일갯수 - 1까지 3초에 한번 1씩 올라갑니다.
    - 즉 files.map()에 의해 `<File>`은 총 파일 갯수만큼 만들어지지만, 이 중 index가 currentItem과 일치하는 단 하나의 파일만 우리에게 보이게 됩니다. 이게 병원 프로필 상단 이미지 슬라이더가 동작하는 원리입니다.


이정도면 HospitalProfilePresenter에 관한 내용도 대부분 다루었습니다. 내용이 많이 길어졌는데 내용은 길지만 그렇게 복잡하진 않습니다. 


위 내용을 바탕으로 직접 엘리먼트를 만들고 받은 데이터를 엘리먼트 안에 넣어 표시시키고, 그 엘리먼트의 스타일을 크롬 개발자 툴 등을 이용해 조정해가며 원하는 스타일을 만들고 하다 보면 금방 감이 오실겁니다.


혹시 모호한 부분 있다면 말씀주세요.

---

#### **To-do-list**

1. 설치 ~ 실행 후 로그인. 이하 기능들.

- [x] 백엔드 실행법
- [x] 프론트엔드 실행법

2. hospital profile 만든 과정

* 백엔드
- [x] 레이아웃 설명
- [x] datamodel 새로 만들기. Hosptial 데이터모델, 그에 따른 데이터모델 수정
- [x] Resolver 만들기
- [x] Hosptial.js computed field 만들기 + 그에 따른 models.graphql 수정

* 프론트앤드
- [x] Routes에서 hosptial profile로 넘어가는 route 만들기
- [x] Header에서 해당 route로 연결해주는 링크 만들기?
- [X] 컴포넌트 디자인
  - [X] 개요:
  - [X] Container 만들기
  - [X] Presenter 만들기

---


이 아래로는 제가 예전에 써놓았던 문서입니다.


# 1. Apollo

/.Apollo/Client.js 파일을 보시면

```js
export default new ApolloClient({
  uri:
    process.env.NODE_ENV === "development"
      ? "http://localhost:4000"
      : "https://hground-backend.herokuapp.com",
  clientState: {
    defaults,
    resolvers
  },
  headers: {
    Authorization: `Bearer ${localStorage.getItem("token")}`
  }
});
```

이렇게 생긴 부분이 있어요. 이 말은 우리가 개발중일때는 (process.env.NODE_ENV === "development") ["http://localhost:4000"](http://localhost:4000)을 서버 url로 삼아 통신하고, 그렇지 않을 경우에는 ["https://hground-backend.herokuapp.com"](https://hground-backend.herokuapp.com)을 통해 통신한단 소리입니다. (이 자리엔 저희 서버가 들어올거에요. 지금은 제가 임시로 heroku로 만들어놓았습니다.)

#### 1.1 로그인 프로세스

이 예제에서는 로그인이 조금 이상한 방식으로 되어있어요.

계정을 만들고 로그인을 누르면, 해당 계정 이메일로 secret 키가 발송이 됩니다. 이 secret key를 입력하는 방식으로 로그인을 하게됩니다.

#### Feed, Profile

피드랑 프로파일 등 메뉴가 있는걸 확인할 수 있어요. 그런데 Post가 아무것도 안 올라와서 그런지 지금 들어가보면 상당히 휑할거에요. 이 부분은 좀 더 작업해서 업데이트드리겠습니다.

---

아폴로 클라이언트:
Apollo Client를 시작하는것. ApolloClient는 GraphQL API와 앱을 연결합니다.
Apollo는 graphql을 기반으로 한 상태관리 플랫폼이다. 클라이언트에서 graphql을 사용하여 데이터를 가져오는 UI를 만들 때 사용하기 좋다.
특히 React하고 결합이 좋다. => 컴포넌트 자체에 Query를 녹여서 구현하기가 쉬워진다
그리고 App.js와 Apollo Client를 연결해준다.

Dog라는 component에서 GET_DOGS라는 query를 이용해볼게요.

```js
const GET_DOGS = gql`
  {
    dogs {
      id
      breed
    }
  }
`;

const Dogs = ({ onDogSelected }) => (
  <Query query={GET_DOGS}>
    {({ loading, error, data }) => {
      if (loading) return "Loading...";
      if (error) return `Error! ${error.message}`;

      return (
        <select name="dog" onChange={onDogSelected}>
          {data.dogs.map(dog => (
            <option key={dog.id} value={dog.breed}>
              {dog.breed}
            </option>
          ))}
        </select>
      );
    }}
  </Query>
);
```

#### LocalState

원래는 post가 열리고 닫히고 이런걸 다 LocalState에서 조절하는데
일단 지금은 로그인만 조절해봅시다.
웹사이트의 LocalStorage:
크롬에서 F12를 누른다음 localStorage를 쳐보세요. 말 그래도 서버가 아닌 사용자가 프론트엔드를 이용하는데 필요한것들이 이거에요. 저희가 사용하는 기기 (로컬)에 쓰이는 정보들이 여기 저장됩니다.

#### Apollo Chorme Extension

Apollo Client를 보다 편하게 사용할 수 있게 해주는 크롬 확장도구.
GraphQL playground와 유사하게 query들을 만져보거나 확인하거나 할 수 있다.

#### 프론트엔드에서의 GraphQL query

```js
import { gql } from "apollo-boost";
import { useQuery } from "react-apollo-hooks";

// GraphQL query isLoggedIn을 정의해줍니다.
// @client: 설명은 아래에
const QUERY = gql`
  {
    isLoggedIn @client
  }
`;
const {
  data: { isLoggedIn }
} = useQuery(QUERY);
```

여기서 isLoggedIn에 @client는 왜 붙어있느냐. 이걸 붙여놓지 않을 시 Apollo는 우리 서버쪽에 접근해서 isLoggedIn에 접근하려 합니다. 로그인 유무는 서버가 아니라 클라이언트쪽에 저장되므로 @client를 넣어줍니다. (아폴로 클라이언트 내에서만 사용하는 느낌인듯)

query는 userQuery (react-apollo-hooks)를 통해 사용하게 됩니다.
위에 적어놓은 JS 코드를 보면 알겠지만 그냥 저런식으로 사용하면 되요!

# Styling

Theme ~ Themeprovider

Glboalstyles: Global Styles.

- 안에서 props.theme.XXX 와 같은 식으로 theme.js 내 style들을 활용가능

# Components 살펴보기

Hooks: Hooks는 src/Hooks에서 가져옴. 애초에 useInputs.js밖에 없음

## heroku

```
heroku login
heroku git:remote -a hground-backend
git push heroku master
```
