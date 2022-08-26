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
1. 사용자의 입력이 유효한지 판단 하는 함수 설계
 * 코드 구성 
``` swift
    func checkNumber(_ userInput: String?) -> Array<Int>? {
        guard let userInput = userInput else { return nil }

        let userInputArr = userInput.split(separator: " ")
        if userInputArr.count != 3 { return nil }

        let userNumber = userInputArr.compactMap{ Int($0) }.filter { $0 > 0 && $0 < 10 }
        if Set(userNumber).count != 3 { return nil }

        return userNumber
    }
```
   - 숫자 범위를 판단하는 부분을 다시 확인하면 구현 로직 변경
   - 고차함수를 활용해 직관적인 코드로 수정

2. [Swift API Design Guideline](https://www.swift.org/documentation/api-design-guidelines/)에 따른 변수명 설정 및 코드 컨벤션 수정 
   - 직관적이고 효율적인 코드 설계에 어려움을 느꼈지만 리뷰어의 피드백을 통해 함수명을 동사, 변수명을 명사로 변경 하는 등의 컨벤션 수정
   - Ex) menu() -> selectMenu()

## 📚참고 링크
- [Swift API Design Guideline](https://www.swift.org/documentation/api-design-guidelines/)
- [Swift Language Guide - Optional, nil, Optional Binding](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)
- [Swift Language Guide - Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html)
