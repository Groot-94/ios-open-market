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
- [구현화면](#구현내용)
- [키워드](#키워드)
- [TroubleShooting](#TroubleShooting)
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
||||
|:---:|:---:|:---:|
|레이아웃 변경 화면|화면 스크롤|리스트 화면 새로고침|
|<img src = "https://i.imgur.com/9OxGWib.gif" width="300" height="600">| <img src = "https://i.imgur.com/nYey8oC.gif" width="300" height="600"> | <img src = "https://i.imgur.com/1TMvjwp.gif" width="300" height="600">|
|그리드 화면 새로고침|새 상품 등록|상품 설명 키보드 내 키보드 내리는 버튼 구현|
| <img src = "https://i.imgur.com/VRFrIcf.gif" width="300" height="600"> |<img src = "https://i.imgur.com/kBW2zhO.gif" width="300" height="600">| <img src = "https://i.imgur.com/HDMGd5o.gif" width="300" height="600"> |
|사진 등록 스크롤뷰 구현|등록 형식을 못맞췄을 때|상품 삭제 구현|
| <img src = "https://i.imgur.com/GJhqacZ.gif" width="300" height="600">| <img src = "https://i.imgur.com/UqO0PZa.gif" width="300" height="600"> |<img src = "https://i.imgur.com/5U1bgBG.gif" width="300" height="600">|
|상품 수정 구현|상품삭제 비밀번호 틀렸을 때|수정할 때 형식 못맞췃을때|
|<img src = "https://i.imgur.com/OJpYfei.gif" width="300" height="600">|<img src = "https://i.imgur.com/WLYIcMC.gif" width="300" height="600">|<img src = "https://i.imgur.com/iLY8who.gif" width="300" height="600">|
## 키워드

<details>
<summary>내용보기</summary>

- JSON Decoder
- URLSession
- MockSession
- Unit Test
- Asynchronous Tests
- Collection View
- Mordern Collection View
- Compositional Layout
- List Configuration
- UISegmentedControl
- UIActivityIndicatorView
- UICollectionViewDiffableDataSource
- NSMutableAttributedString
- asynchronous data fetching
- UIImagePickerController
- UITextView
- UITextViewDelegate
- Keyboard
- UIAlertController
- multipart-form/data
- UICollectionView Pagination
    
</details>

## [TroubleShooting]

<details>
<summary>내용보기</summary>

### 1. Network에서 data를 받아오는 Unit Test를 하면서 테스트가 제대로 되지 않는 문제
- 네트워크는 서버에서 언제 응답이 올지 모르기 때문에 dataTask의 completionHandler는 비동기 실행입니다.
- `XCTAssertEqual`이 실행되는 시점보다 completionHandler의 비동기 실행이 느려서 테스트가 실패하는 문제가 있었습니다.
- 해결하기 위해서 Asynchronous Tests and Expectations 공식문서를 참고했습니다.
    - XCTest가 handle waiting을 하는데 사용하는 개체인 하나 이상의 expectations를 생성합니다.
    - 그런 다음 비동기 코드 실행이 완료되면 XCTest에 대기를 중지하도록 지시합니다.
    - 테스트는 expectations가 fulfill되거나 지정된 시간 초과가 만료될 때까지 기다립니다.
```swift
func test_APIRequest를_받아와서_디코딩이_잘되는지() {
        // given
        let expectation = expectation(description: "비동기 요청을 기다림.")
        var resultName: String?
        let myURLSession = MyURLSession()
        
        myURLSession.dataTask(with: sut!) { (result: Result<ProductsDetailList, Error>) in
            switch result {
            case .success(let success):
                resultName = success.pages[0].name
            case .failure(_):
                break
            }
            expectation.fulfill()
        }
            
        wait(for: [expectation], timeout: 300)
        
        // when
        let result = "데릭"
        
        // then
        XCTAssertEqual(result, resultName)
    }
```
[Asynchronous Tests and Expectations](https://developer.apple.com/documentation/xctest/asynchronous_tests_and_expectations)

### 2. UICollectionView layout 초기화
 - 처음 UICollectionView 인스턴스를 생성해 주었더니 다음과 같은 오류가 났습니다.
```
  UICollectionView must be initialized with a non-nil layout parameter
```
- 오류에서 알 수 있듯이 `layout` 파라미터를 nil로 해주어서 생긴 오류였고, layout을 초기화시켜 주어 해결했습니다.

### 3. lazy var
- `listConfiguration`을 인스턴스로 만들고, `listLayout` 내부의 프로퍼티로 사용하려고 하니 다음과 같은 오류가 발생했습니다.
```
    Cannot use instance member 'listConfiguration' within property initializer; property initializers run before 'self' is available
```
- 인스턴스가 생성되기전 내부 프로퍼티의 파라미터로 사용하려고 하여 다음과 같은 오류 발생했다고 생각이 들었고, lazy var를 사용하여 초기화 시점을 동일하게 만들어서 해결했습니다.

### 4. hashable 채택
- Collection View에서 데이터를 불러왔는데 같은 값을 가지고 있다고 앱 크래쉬가 발생했습니다.
- 데이터를 불러오는 구조체인 `ProductDetail`에 `Hashable`을 채택하는 방법으로 해결했습니다.
- Hashable이란?
    - 정수 Hash 값을 제공하는 타입입니다.
    - 그 값 자체로 유일하게 표현이 가능한 방법을 제공합니다.

### 5. Ambigious UILabel height in autoresizing UITableViewCell 경고창
- StackView에 Label을 순서대로 넣은 상태에서 label들의 text만 정해주면 따로 label들의 constraints 설정없이 레이아웃이 정렬된다고 생각했습니다.
- 하지만, 그림과 같은 경고창을 보여줬습니다.
    <img src = "https://i.imgur.com/Tm4zsMo.png" width="500" height="400">
- 여러가지 방법을 사용해서 경고창을 없애려고 했지만 결국에 찾은 방법은 Stack View의 distribution을 변경해주는 방법이였습니다.
    <img src = "https://i.imgur.com/jPVepIj.png" width="700" height="200">
    <img src = "https://i.imgur.com/oQUPFvV.png" width="700" height="200">

[해당 블로그](http://47.112.232.56/a/stackoverflow/en/629df61c4deb6d4bcd5064d5.html)를 보고 Content Hugging priority를 설정해 보았지만 해결이 되지 않았었습니다🥲

[UIStackView.Distribution.equalCentering - 공식문서](https://developer.apple.com/documentation/uikit/uistackview/distribution/equalcentering)

### 6. UIView with rounded corners and drop shadow / Modern Collection View's grid layout 사용 시 cell에 테두리가 자동으로 설정된다고 생각했으나, 테두리가 나타나지 않음.
- grid view를 구현하면서 cell의 테두리가 나타나지 않아서 Modern Collection View's grid에 대해 찾아봤지만 테두리에 대한 내용을 찾지 못했습니다.
- cell의 draw 함수를 override 해서 layout 프로퍼티를 이용해 테두리를 구현하였습니다.

[참고 사이트](https://stackoverflow.com/questions/4754392/uiview-with-rounded-corners-and-drop-shadow)

### snapshot.deleteAllItems() 을 사용해서 cell의 item을 새로고침 하면서 main thread 관련 경고가 나타났습니다.

<img src = "https://i.imgur.com/uCyLS26.png" width="700" height="200">

- 위 문제를 해결하기 위해서 refresh 메서드를 main thread에 넣는 방법을 사용했지만, 동일하게 경고가 나타났습니다.
```swift
@objc private func refresh() {
        DispatchQueue.main.async {
            self.listCollectionView.deleteSnapshot()
            self.gridCollectionView.deleteSnapshot()
            self.fetchData()
            self.listCollectionView.refreshControl?.endRefreshing()
            self.gridCollectionView.refreshControl?.endRefreshing()
        }
    }
```
- 기존 fetchData 메서드에서 SnapShot을 적용하는 부분이 main thread에서 일어나지 않을 가능성이 존재해서 deleteSnapshot 하는 부분과 Race condition의 가능성에 대한 경고로 판단했습니다.
```swift
DispatchQueue.main.async {
                    self.gridCollectionView.configureSnapshot(productsList: success.pages)
                    self.listCollectionView.configureSnapshot(productsList: success.pages)
                    guard let loadingView = self.loadingView,
                          loadingView.isHidden == false
                    else { return }
                    self.removeSpinner()
                }
```
- configureSnapshot을 main thread에서 실행하는 방법으로 해결했습니다.
### 7. 이미지의 크기를 줄이는 방법을 고민했습니다.
- 이미지의 크기(byte)를 줄이기 위해서 방법을 검색을 했지만, byte를 줄이는 방법보다는 사이즈를 줄이는 방법만 확인 할 수 있었습니다. 
- 여러가지 시도 중 사이즈를 조금씩 줄이면 byte의 크기가 줄어듬을 알 수 있었고, 재귀함수를 사용해서 이미지의 크기가 300 byte를 넘으면 조금씩 줄이는 방식으로 이미지의 크기를 줄였습니다.
    ```swift
    func resize(width: CGFloat) -> UIImage {
            let scale = width / self.size.width
            let newHeight = self.size.height * scale

            let size = CGSize(width: width, height: newHeight)
            let render = UIGraphicsImageRenderer(size: size)
            var renderImage = render.image { context in
                self.draw(in: CGRect(origin: .zero, size: size))
            }

            let imgData = NSData(data: renderImage.pngData()!)
            let imageSize = Double(imgData.count) / Design.devideImageDataCountByThousand

            if imageSize > Design.imageDataCountConstraint {
                renderImage = resize(width: width - Design.renderImageResizeNumber)
            }
            return renderImage
        }
    ```
</details>
    
## [1️⃣ Step1_Wiki](https://github.com/bar-d/ios-open-market/wiki/Step1)
## [2️⃣ Step2_Wiki](https://github.com/bar-d/ios-open-market/wiki/Step2)
## [3️⃣ Step3_Wiki](https://github.com/bar-d/ios-open-market/wiki/Step3)
## 프로젝트_후기
컬렉션뷰와 네트워크 구현이 처음이라 힘들었지만, 팀원과 삽질?을 굉장히 오래 하면서 코드를 만들어가는 재미가 있었습니다.
마감 일자를 지키지 못해 리뷰를 받지는 못했지만, 방학기간에도 진행하고 리드미를 작성하면서 끝까지 함께해주는 좋은 팀원과 함께해서 다행이라는 생각을 하게 되었습니다.
### 프로젝트를 진행하면서 느낀 필요성 몇 가지
1. 코드에 철학을 담자.
2. 코드 컨벤션을 지키자(아름다운 코드를 짜자).
3. 지치지 말자.
4. 트러블 슈팅을 미리 작성하자(프로젝트를 진행하면서 하게 되는 고민도 그때그때 작성해놓자) 
5. 리뷰를 받았을 때 바로 적용하는 게 아니라 나의 철학과 비교하고 고민해보자.
## 참고문서
- [URLSession](https://developer.apple.com/documentation/foundation/urlsession)
    - [Fetching Website Data into Memory](https://developer.apple.com/documentation/foundation/url_loading_system/fetching_website_data_into_memory)
- [UICollectionView](https://developer.apple.com/documentation/uikit/uicollectionview)
    - [Modern cell configuration](https://developer.apple.com/videos/play/wwdc2020/10027/)
    - [Lists in UICollectionView](https://developer.apple.com/videos/play/wwdc2020/10026)
    - [Implementing Modern Collection Views](https://developer.apple.com/documentation/uikit/views_and_controls/collection_views/implementing_modern_collection_views)
- [Data Entry - iOS - Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/patterns/entering-data/)
- [UIAlertController](https://developer.apple.com/documentation/uikit/uialertcontroller)
