# 🔢숫자야구게임⚾

## 소개
랜덤한 숫자 3개를 맞추는 게임 <br>
숫자의 값과 위치가 같으면 스트라이크, 값만 같다면 볼로 사용자는 랜덤한 숫자를 추리
--- 

## 🧑‍🎓팀원
사진 | 닉네임 | 역할
---|:---:|:-------:
![aaron_discord_img](https://user-images.githubusercontent.com/57447946/185568222-2dc1b950-e702-463b-867d-1280f61ba922.jpg) | [`Aaron`](https://github.com/Hashswim) | 설계 및 구현
![dragon_discord_img](https://user-images.githubusercontent.com/57447946/185568196-b3e50482-e4ae-4bf4-9fa9-57e2ac427d5a.jpg) | [`dragon`](https://github.com/DragonYG) | 설계 및 구현
--- 

## 🕟︎타임라인
[커밋 로그](https://github.com/DragonYG/ios-number-baseball/commits/main)
--- 

## ✐순서도
![flow_chart_야구게임_1 drawio](https://user-images.githubusercontent.com/57447946/185417507-0491b63d-20f8-4ba2-a5a9-86d25d6c2e4b.png)
--- 

## 🖥︎실행 화면
 * 메뉴 선택
   - 사용자로부터 메뉴를 입력받음
  <img width="593" alt="메뉴창" src="https://user-images.githubusercontent.com/57447946/185570736-22a521d9-22f8-4e86-86a1-2221cfee69be.png">
  

 * 게임 시작
   - 입력해야하는 형식 출력 및 받은 입력 저장
  <img width="593" alt="게임시작" src="https://user-images.githubusercontent.com/57447946/185571128-3b54ed2b-317b-4b7c-8a9c-2b84fca43e62.png">
  <br>
  
 * 입력 유효성 검사 및 판정
   - 사용자로부터 받은 입력이 1~9사이의 유효한 숫자 3개라면 스트라이크·볼 판정, 남은 횟수 출력
   - 사용자로부터 받은 입력이 문자, 범위 밖의 숫자, 3개가 아닌 숫자라면 재입력 메시지 출력
  <img width="593" alt="사용자 입력처리" src="https://user-images.githubusercontent.com/57447946/185572864-a1c31758-61c2-4512-ae72-a115c06261f6.png">
   <br>

 * 게임 결과 출력
   - 사용자가 3 스트라이크를 달성했을 경우 사용자 승리 메시지 출력 및 메뉴 선택창 이동
  <img width="593" alt="사용자승리" src="https://user-images.githubusercontent.com/57447946/185570734-936a4ef9-827d-4018-9640-e1eae8e10809.png">
  <br>

   - 사용자가 남은 기회를 모두 소진했을 경우 컴퓨터 승리 메시지 출력 및 메뉴 선택창 이동
  <img width="593" alt="컴퓨터승리" src="https://user-images.githubusercontent.com/57447946/185570730-841bc5cf-ad58-45eb-9755-9be0837cbff3.png">
  <br>

 * 게임 종료
   - 게임 종료 메뉴 입력 시 프로그램 종료
  <img width="593" alt="게임종료" src="https://user-images.githubusercontent.com/57447946/185570723-7f0b8821-937b-4cb9-a47f-7b366e1f46ff.png">
  <br>

--- 

## 😧트러블 슈팅
1. 사용자의 입력을 받는 함수와 입력의 유효성을 검토하는 함수를 구분되게 변경
> 변경 사유 : 함수에 들여쓰기 2회초과와 함수형 프로그래밍을 위한 기능 구분
   
* 기존 코드
``` swift
func getUserNumber() -> Array<Int> {
     print("숫자 3개를 띄어쓰기로 구분해주세요.\n중복숫자는 허용하지 않습니다")
     print("입력 : ", terminator: "")
     var userNumbers = [Int]()

     if let userNumber = readLine()?.split(separator: " ") {
         if userNumber.count == 3 {
             if let userNumber1 = Int(userNumber[0]) {
                 if userNumber1 > 0 && userNumber1 < 10 {
                     userNumbers.append(userNumber1)
                 }
             }
             if let userNumber2 = Int(userNumber[1]) {
                 if userNumber2 > 0 && userNumber2 < 10 {
                     userNumbers.append(userNumber2)
                 }
             }
             if let userNumber3 = Int(userNumber[2]) {
                 if userNumber3 > 0 && userNumber3 < 10 {
                     userNumbers.append(userNumber3)
                 }
             }
         }
     }
     if Set(userNumbers).count != 3 {
         userNumbers.removeAll()
     }
     if userNumbers.count != 3 {
         print("입력이 잘못되었습니다.")
     }

     return userNumbers
     let userInput = readLine()?.split(separator: " ")

     return userInput
 }
 ```

 * 변경 구성 
``` swift
func getUserNumber() -> Array<Int> {
    while true {
        print("숫자 3개를 띄어쓰기로 구분해주세요.\n중복숫자는 허용하지 않습니다.")
        print("입력 : ", terminator: "")
        let input = readLine()

        if let userNumber = checkNumber(input) {
            return userNumber
        }
        print("입력이 잘못되었습니다.")
    }
}

func checkNumber(_ userInput: String?) -> Array<Int>? {
    guard let userInput = userInput else { return nil }

    let userInputArr = userInput.split(separator: " ")
    if userInputArr.count != 3 { return nil }

    let userNumber = userInputArr.compactMap{ Int($0) }.filter { $0 > 0 && $0 < 10 }
    if Set(userNumber).count != 3 { return nil }

    return userNumber
}
```
   - 고차함수를 활용해 직관적인 코드로 수정
      - 형변환을 Set으로 해줌으로써 중복되는 값을 제거 (Set에는 중복된 값이 들어갈 수 없음)
      - .compactMap 를 사용하여 정수값만 입력되게 변경
      - .filter 를 사용하여 입력 가능한 정수값을 설정
   - guard let & if let 을 사용하여 Optional 처리
   - :star: 유효성에 맞는 값만 남을 때까지 필터하는 방식 -> 유효성에 맞지 않는 값만 리턴시키는 방식으로 변경

2. 스트라이크 & 볼을 판정하는 함수 구현
* 구현 코드
``` swift
func compareStikeBall(_ randomNumber: Array<Int>, _ userNumber: Array<Int>) -> Bool {
    var strike = 0
    var ball = 0

    userNumber.forEach {
        if randomNumber.contains($0) {
            ball += 1
        }
    }
    strike = zip(randomNumber, userNumber).compactMap {
        $0.0 == $0.1 ? true : nil
    }.count
    ball -= strike

    print("\(strike) 스트라이크, \(ball) 볼")
    return strike == 3 ? true : false
}
```
   - 고차함수를 활용해 직관적인 코드 적용
      - .forEach : 배열 안에 있는 모든 값을 순차적으로 확인
      - .contains : 배열 안에 해당 값이 포함되었는지 확인
      - .zip : 좌측에 기입된 배열과 우측에 기입된 배열의 같은 순번에 위치한 값을 확인하여 동일위치라면 True값 출력, 다르다면 nil 출력
      - .count : 배열에 포함된 값이 몇개인지 출력
   - [조건 ? 맞을경우 : 틀릴경우]로 if문 대체 가능
   - 매개변수 앞에 _(언더바)를 설정해둘 경우 매개변수명을 적지않고 원하는 값만 넣어줄 수 있음

3. [Swift API Design Guideline](https://www.swift.org/documentation/api-design-guidelines/)에 따른 변수명 설정 및 코드 컨벤션 수정 
   - 직관적이고 효율적인 코드 설계에 어려움을 느꼈지만 리뷰어의 피드백을 통해 함수명을 동사, 변수명을 명사로 변경 하는 등의 컨벤션 수정
   - Ex) menu() -> selectMenu()

## 📚참고 링크
- [Swift API Design Guideline](https://www.swift.org/documentation/api-design-guidelines/)
- [Swift Language Guide - Optional, nil, Optional Binding](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)
- [Swift Language Guide - Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html)
- [Apple Develop Documentation - Optional](https://developer.apple.com/documentation/swift/optional)
