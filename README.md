# restaurant-review-service

# 서비스 기능
1. 사용자 프로필 및 소셜 기능
2. 맛집 추천 알고리즘
3. 사진 및 동영상 업로드
4. 지도 통합
5. 이벤트 및 할인 정보
6. 키워드 검색 및 필터링
7. 푸시 알림
8. 다국어 지원
9. 온라인 예약 기능
10. 맛집 통계 및 트렌드


## **사용자 Flow (Usecase)**
- 맛집을 등록할 수 있다
- 맛집을 수정할 수 있다
- 맛집을 삭제할 수 있다
- 맛집에 리뷰를 작성할 수 있다
- 맛집에 작성한 리뷰를 삭제할 수 있다
- 맛집에 작성된 리뷰와 평균별점을 확인할 수 있다

### **데이터**
- 맛집
    - 이름 (String)
    - 주소 (String)
    - N개의 메뉴
        - 이름 (String)
        - 가격 (Number)
    - N개의 리뷰
        - 본문 (String)
        - 별점 (Number)

### ERD

![image](https://github.com/hanjhoon/restaurant-review-service/assets/121271030/e5937d3d-f710-4ce7-9269-3fcb592020d7)

### API

- 맛집 리스트 가져오기 API
    
    ```
    GET /restaurants
    
    // response
    [
      {
        "id": Long,
        "name": string,
        "address": string,
        "createdAt": string,
        "updatedAt": string
      },
      ...
    }
    ```
    
- 맛집 정보 가져오기 API
    
    ```
    GET /restaurant/{restaurantId}
    
    // response
    {
      "id": Long,
      "name": string,
      "address": string,
      "createdAt": string,
      "updatedAt": string,
      "menus": [
        {"id": Long, "name": string, "price": int, "createdAt": string, "updatedAt": string},
        {"id": Long, "name": string, "price": int, "createdAt": string, "updatedAt": string},
        ...
      ]
    }
    ```
    
- 맛집 생성 API
    
    ```
    POST /restaurant
    {
      "name": string,
      "address": string,
      "menus": [
        {"name": string, "price": int},
        ...
      ]
    }
    ```
    
- 맛집 수정 API
    
    ```
    PUT /restaurant/{restaurantId}
    {
      "name": string,
      "address": string,
      "menus": [
        {"name": string, "price": int},
        ...
      ]
    }
    ```
    
- 맛집 삭제 API
    
    ```
    DELETE /restaurant/{restaurantId}
    ```
    
- 리뷰 작성 API
    
    ```
    POST /review
    {
      "restaurantId": int,
      "content": string,
      "score": float
    }
    ```
    
- 리뷰 삭제 API
    
    ```
    DELETE /review/{reviewId}
    ```
    
- 맛집에 등록된 리뷰 가져오기 API
```
GET /restaurant/{restaurantId}/reviews

// response
{
  "avgScore": float, // 평균 별점
  "reviews": [
    {"id": int, "content": string, "score": float, "createdAt": string},
    {"id": int, "content": string, "score": float, "createdAt": string},
    {"id": int, "content": string, "score": float, "createdAt": string}
  ],
  "page": {
    "offset": int,
    "limit": int
  }
}
```
