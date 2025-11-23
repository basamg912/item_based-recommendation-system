# 🎬 Bigdata Recommendation System – Preprocessing (Rating + Genre Hybrid Embedding)

본 프로젝트에서는 Item-Based Collaborative Filtering을 Dot Product 방식으로 구현하는 것을 목표로 한다.  
이를 위해 **영화 평점 데이터와 장르 정보를 결합한 hybrid item embedding** 전처리를 수행하여,  
기본 rating-only 방식보다 더 안정적이고 의미 있는 item similarity를 얻는 것을 목표로 전처리를 진행하였다.

---

## ⭐ 1. 전처리 개요

MovieLens 데이터는 기본적으로 **평점 정보가 sparse**하며,  
평점만 가지고 item 간 유사도를 계산하면 정보량이 부족해 추천 품질이 낮을 수 있다.

이를 보완하기 위해  
**평점 데이터 + 장르 One-hot 인코딩 벡터**를 결합하여  
각 영화의 특징을 더 풍부하게 표현하는 hybrid item embedding을 구성하였다.

이 방식을 통해  
- 장르 기반의 콘텐츠 정보  
- 사용자 평점 패턴  
두 요소가 함께 반영된 item similarity 계산이 가능해진다.

---

## ⭐ 2. 전처리 과정

### 🔹 Step 1. Rating Matrix 생성
- `movieId × userId` 형태의 pivot table 생성  
- 결측치는 0 또는 user 평균 등으로 채워 여러 방식 비교 예정  

---

### 🔹 Step 2. Genre One-hot 인코딩
- `movies.csv`의 `genres` 컬럼을 `'|'` 기준으로 분리  
- `MultiLabelBinarizer()`를 활용하여 One-hot 인코딩 수행  

---

### 🔹 Step 3. Rating + Genre 결합 (Hybrid Item Embedding)

두 벡터를 movieId 기준으로 정렬 후 concat:

```
[item_rating_vector | item_genre_vector]
```

---

### 🔹 Step 4. Similarity 계산 실험
- rating-only embedding vs hybrid embedding 비교  
- Dot Product / Cosine Similarity 기반 item-item similarity 계산  
- 추천 top-N 결과 변화 확인  

---

### 🔹 Step 5. 추천 품질 비교 실험
- rating-only 기반 추천 top-10  
- rating+genre 기반 추천 top-10  
- 장르 반영 여부에 따른 추천 결과의 자연스러움 평가  

---

## ⭐ 3. Hybrid Embedding의 장점

- 장르 정보가 item 고유 특성을 보완  
- sparse한 rating matrix의 취약점을 dense genre vector가 보완  
- 특정 유저의 extreme rating에 의해 유사도가 흔들리는 문제 감소  
- item-based dot product에서 더 일관된 similarity 분포 생성  

---

## ⭐ 4. 코드 예시 (Colab/Notebook)

```python
import pandas as pd
from sklearn.preprocessing import MultiLabelBinarizer

movies = pd.read_csv("movies.csv")
ratings = pd.read_csv("ratings.csv")

movies['genres'] = movies['genres'].apply(lambda x: x.split('|'))
mlb = MultiLabelBinarizer()
genre_ohe = pd.DataFrame(
    mlb.fit_transform(movies['genres']),
    columns=mlb.classes_,
    index=movies['movieId']
)

rating_mat = ratings.pivot_table(
    index='movieId',
    columns='userId',
    values='rating'
).fillna(0)

rating_mat = rating_mat.sort_index()
genre_ohe = genre_ohe.sort_index()

item_embedding = pd.concat([rating_mat, genre_ohe], axis=1)

print(item_embedding.shape)
item_embedding.head()
```

---

## ⭐ 5. 향후 실험 계획

- rating-only vs hybrid embedding similarity 분포 비교  
- 추천 top-N 결과 비교  
- genre feature 사용 시 추천의 자연스러움 평가  

---

