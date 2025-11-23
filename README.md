# Bigdata Recommendation System

Point
- 전처리
    - 데이터 EDA 하면서 인덱스 처리, 널 처리 시행 및 발표 과정에서 언급
    - 병렬처리 등 고려해 유사도 계산시 걸린 시간도 함께 발표 언급
    - 개선 안된 부분도 함께 공유
    - Dot Product 를 통한 유사도 계산이 최종 목표
- Goal
    - Item - Based CF 를 Dot Production 을 통해 추천 시스템 구현

- 유의사항
    - 제작 연도가 없는 영화에 대한 처리
        - 리메이크 및 재개봉 등에 의한 연도 차이 및 연도 미등록 데이터에 대한 처리를 어떻게 할 것인가?
    - User Based CF 시 User Rating Matrix 는 Sparse 함
        - NaN 값 처리를 어떻게 할 것인가?
            - 단순히 0 으로 처리, 혹은 평균 처리 등
    - Model Eval
        - 각 유저에 대한 Rating 을 Pred
        - NaN 인 유저들에 대해서는 Pred 를 사용하는게 추천 시스템의 목적
        - Model Eval 은 특정 영화를 본 사용자에 대한 Pred 값과, 실제로 사용자의 평가 점수 간의 오차
    - Item Based CF  에 대한 설명
        - 특정 User 가 **시청한 비슷한 영화를 추천해준다.**
        - 유사도 점수를 어떻게 계산할 것인가?
            - One Hot 기반 cos 유사도 : 영화를 봤는가 안 봤는가
            - Frequency 기반 : 어떤 사람이 그 영화를 몇번 보았는가
            - 평점 기반 cos 유사도 : 몇점을 주었는가?
            - 장르 기반 유사도 : 평점 + 영화의 장르에 대한 유사도

11/24 (월) 회의 내용
- Null 값에 어떤 값을 처리할 것인가?
- 병렬처리에 대한 질문 (GPU?)
