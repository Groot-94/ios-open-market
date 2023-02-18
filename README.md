# 오픈 마켓 README.md
## 프로젝트 저장소
> 프로젝트 기간: 2022-07-11 ~ 2022-08-05</br>
> 팀원: [바드](https://github.com/bar-d), [그루트](https://github.com/Groot-94)</br>
리뷰어: [@Charlie](https://github.com/kcharliek)</br>
그라운드롤: [GroundRule - Wiki](https://github.com/bar-d/ios-open-market/wiki/Ground-Rules)
## 📑 목차
- [개발자 소개](#개발자-소개)
- [프로젝트 소개](#프로젝트-소개)
- [UML](#UML)
- [구현화면](#구현화면)
- [TroubleShooting](#TroubleShooting_Wiki)
- [1️⃣ Step1](#1️⃣-Step1_Wiki)
- [2️⃣ Step2](#2️⃣-Step2_Wiki)
- [3️⃣ Step3](#3️⃣-Step3_Wiki)
- [프로젝트 후기](#프로젝트_후기)
- [참고문서](#참고문서)
## 개발자 소개
|바드|그루트|
|:---:|:---:|
| <img src = "https://i.imgur.com/k9hX1UH.png" width="250" height="250">| <img src = "https://i.imgur.com/onBeySC.jpg" width="250" height="250"> |
|[바드](https://github.com/bar-d)|[그루트](https://github.com/Groot-94)|
## 프로젝트 소개
-  URL Session을 활용한 서버와의 통신을 통해 전달받은 JSON 데이터와 매핑할 모델을 활용
-  Modern CollectionView를 이용해 List, Grid 방식으로 마켓의 물품을 표시하도록 구현
## UML
### [ClassDiagram]
![](https://i.imgur.com/Uqx3FVq.jpg)
## 구현화면
|||
|:---:|:---:|
|레이아웃 변경 화면|화면 스크롤|
| <img src = "https://i.imgur.com/9OxGWib.gif" width="300" height="600">| <img src = "https://i.imgur.com/nYey8oC.gif" width="300" height="600"> |
|리스트 화면 새로고침|그리드 화면 새로고침|
| <img src = "https://i.imgur.com/1TMvjwp.gif" width="300" height="600">| <img src = "https://i.imgur.com/VRFrIcf.gif" width="300" height="600"> |
|새 상품 등록|상품 설명 키보드 내 키보드 내리는 버튼 구현|
| <img src = "https://i.imgur.com/kBW2zhO.gif" width="300" height="600">| <img src = "https://i.imgur.com/HDMGd5o.gif" width="300" height="600"> |
|사진 등록 스크롤뷰 구현|등록 형식을 못맞췄을 때|
| <img src = "https://i.imgur.com/GJhqacZ.gif" width="300" height="600">| <img src = "https://i.imgur.com/UqO0PZa.gif" width="300" height="600"> |
|상품 삭제 구현|상품 수정 구현|
|<img src = "https://i.imgur.com/5U1bgBG.gif" width="300" height="600">|<img src = "https://i.imgur.com/OJpYfei.gif" width="300" height="600">|
|상품삭제 비밀번호 틀렸을 때|수정할 때 형식 못맞췃을때|
|<img src = "https://i.imgur.com/WLYIcMC.gif" width="300" height="600">|<img src = "https://i.imgur.com/iLY8who.gif" width="300" height="600">|
## [TroubleShooting_Wiki](https://github.com/bar-d/ios-open-market/wiki/TroubleShooting)
## [1️⃣ Step1_Wiki](https://github.com/bar-d/ios-open-market/wiki/Step1)
## [2️⃣ Step2_Wiki](https://github.com/bar-d/ios-open-market/wiki/Step2)
## [3️⃣ Step3_Wiki](https://github.com/bar-d/ios-open-market/wiki/Step3)
## 참고문서
- [URLSession](https://developer.apple.com/documentation/foundation/urlsession)
    - [Fetching Website Data into Memory](https://developer.apple.com/documentation/foundation/url_loading_system/fetching_website_data_into_memory)
- [UICollectionView](https://developer.apple.com/documentation/uikit/uicollectionview)
    - [Modern cell configuration](https://developer.apple.com/videos/play/wwdc2020/10027/)
    - [Lists in UICollectionView](https://developer.apple.com/videos/play/wwdc2020/10026)
    - [Implementing Modern Collection Views](https://developer.apple.com/documentation/uikit/views_and_controls/collection_views/implementing_modern_collection_views)
- [Data Entry - iOS - Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/patterns/entering-data/)
- [UIAlertController](https://developer.apple.com/documentation/uikit/uialertcontroller)
## 프로젝트_후기
컬렉션뷰와 네트워크 구현이 처음이라 힘들었지만, 팀원과 삽질?을 굉장히 오래 하면서 코드를 만들어가는 재미가 있었습니다.
마감 일자를 지키지 못해 리뷰를 받지는 못했지만, 방학기간에도 진행하고 리드미를 작성하면서 끝까지 함께해주는 좋은 팀원과 함께해서 다행이라는 생각을 하게 되었습니다.
### 프로젝트를 진행하면서 느낀 필요성 몇 가지
1. 코드에 철학을 담자.
2. 코드 컨벤션을 지키자(아름다운 코드를 짜자).
3. 지치지 말자.
4. 트러블 슈팅을 미리 작성하자(프로젝트를 진행하면서 하게 되는 고민도 그때그때 작성해놓자) 
5. 리뷰를 받았을 때 바로 적용하는 게 아니라 나의 철학과 비교하고 고민해보자.
