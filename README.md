# DACON


## ๐ย ์ ์ฃผ๋ ๋๋ก ๊ตํต๋ ์์ธก AI ๊ฒฝ์ง๋ํ

### ****๐ย ํ๋ก์ ํธ ์งํ๊ธฐ๊ฐ****

2022.10.26 ~ 22.11.14

### ****๐ย ํ๋ก์ ํธ ๋ด์ฉ****

์ ์ฃผ๋์ ๊ตํต ์ ๋ณด๋ก๋ถํฐ ๋๋ก ๊ตํต๋ ํ๊ท ์์ธก

### ****๐ชย ์ญํ ****

- ์ฌ๋ฏผํฌ : EDA, ๋ชจ๋ธ๋ง(LightGBM)
- ์ ํ์ : EDA , ๋ชจ๋ธ๋ง(CatBoost)
- ์ด์ฌ์ฝ : ํ์๋ณ์ ์ถ์ถ(์๋์ ๋์ง์), ๋ชจ๋ธ๋ง(LightGBM)
- ์ ์์ฑ : ๋ชจ๋ธ๋ง(LightGBM, GradientBoosting, Xgboost, LSTM with Attention)

### ****๐๏ธย ๋ฐ์ดํฐ์****

- train : 4,701,217๊ฐ
- test : 291,241๊ฐ
- columns 
 
   <img src="https://user-images.githubusercontent.com/104626180/202997045-7a679a11-f40b-4213-8a0d-f0c8bc2e3416.png" width="700" height="420">
- ์ธ๋ถ ๋ฐ์ดํฐ์ : [์ ์ฃผ์ ์ผ์ผ ๋จ์ ๊ตฌ๊ฐ๋ณ ํ๊ท  ํตํ ์๋ ์ ๋ณด](http://www.jejuits.go.kr/open_api/open_apiView.do) (API key ์ ์ฒญ ํ ์ฌ์ฉ)

### ****โ๏ธย Preprocess****

- EDA
    - correlation matrix(์ ์ฒด)
        - ์๊ด๊ณ์๊ฐ ๋์ ๋ณ์๋ค์ด ๋ง์ง ์์(0.2 ์ด์์ธ ๋ณ์ 4๊ฐ ์กด์ฌ)
            
            ![แแกแผแแชแซแแจแแฎ](https://user-images.githubusercontent.com/104626180/202994809-7f7c1d7c-1741-410d-b978-b884e1bfd110.png)
            
    - correlation matrix(์์นํ)
    
    ![แแฎแแตแแงแผ](https://user-images.githubusercontent.com/104626180/202994928-a50fbffa-385f-4650-bcd6-6063fe2bff81.png)
    
    - PointBiSerial correlation (๋ช๋ชฉํ)
        
        ![แแงแผแแฉแจแแงแผ1](https://user-images.githubusercontent.com/104626180/202995102-e979bf31-3d48-4f3e-b292-b6fb14c0a44f.png)
        
        ![แแงแผแแฉแจแแงแผ2](https://user-images.githubusercontent.com/104626180/202995144-2f83c146-2cdb-46d5-a8a5-439cd15596ef.png)
        
    - ์ถ์ด๊ทธ๋ํ
        - base_date = 2022๋ 7์ ๊ธฐ์ค ๊ตํต๋ ์ฆ๊ฐ
            
            
            ![base_date1](https://user-images.githubusercontent.com/104626180/202995257-d46402bf-55a3-4b49-9852-68d58141648c.png)
            
            ![base_date2](https://user-images.githubusercontent.com/104626180/202995306-0aa691be-f2d1-4679-bceb-57d3a85ac244.png)

            
    - base_hour = 00์-05์,18์-24์ ๊ตํต๋ ๊ฐ์, 05์-18์ ๊ตํต๋ ์ฆ๊ฐ (์ฐจ์ด๊ฐ ํผ)
        
        ![base_hour](https://user-images.githubusercontent.com/104626180/202995378-790ab728-c3e3-4df3-b68f-279ce438d055.png)
        
    - day_of_week = ๊ธ์์ผ ๊ตํต๋ ์ฆ๊ฐ, ์ฃผ๋ง ๊ตํต๋ ๊ฐ์ (ํฐ์ฐจ์ด ์์)
        
        ![base_week](https://user-images.githubusercontent.com/104626180/202995461-3d67bbed-d5e9-4076-9bdf-c8d37a518230.png)
        
- ํ์๋ณ์
    - distance(km ๊ธฐ์ค)
        - haversine๊ณผ ์์์ , ๋์ฐฉ์ ์ ์๋ ๊ฒฝ๋๋ฅผ ์ด์ฉํด์ ๊ฑฐ๋ฆฌ๋ฅผ ๊ตฌํด์ค
    - ๊ธ์์ผ ์ฌ๋ถ(isfriday ์ปฌ๋ผ)
        - ๊ธ์์ผ์ผ ๊ฒฝ์ฐ True, ์๋๋ฉด False
    - ์์ผ๋ณ ๊ฐ์ค์น(day_weight ์ปฌ๋ผ)
        - ํ,์,๋ชฉ : 1
        - ์,๊ธ : 2
        - ํ , ์ผ : 3
    - ์๋์ ๋์ง์(OOO_mean_speed ์ปฌ๋ผ)
        - hour, day, road, lane, max_speed, road_rating, road_type ๋ณ๋ก ํ๊ท ์๋๋ฅผ ๊ตฌํจ
    - 7์ ์๋์ ๋์ง์(OOO_mean_july_speed ์ปฌ๋ผ)
        - 2022๋ 7์ ๊ธฐ์ค ๊ตํต๋ ์ฆ๊ฐ โ 7์์ ์๋์ ๋์ง์ ์ถ๊ฐ
        - lane, max_speed, road_rating, road_type ๋ณ๋ก ํ๊ท ์๋๋ฅผ ๊ตฌํจ
    - 19๋๋ ์๋ณ ํตํ์๋
 - polynomial features ์ฌ์ฉ

### ๐ย ****Modeling****

- dataset
    - 7์ ๋ฐ์ดํฐ(distance + ์๋์ ๋์ง์ ์ถ๊ฐ)
        - 7์ ๋ฐ์ดํฐ๋ก๋ง ํ์ตํ์ ๋ ์ฑ๋ฅ์ด ์ ์ผ ์๋์์
    - 7์ ๋ฐ์ดํฐ(distance + ์๋์ ๋์ง์ + isfriday ์ถ๊ฐ)
    - 7์ 16์ผ ์ดํ ๋ฐ์ดํฐ(distance + ์ ๋์ง์ ์ถ๊ฐ)
        - 7์ 16์ผ ์ดํ ๋ค๋ฅธ ์ถ์ด๋ฅผ ๋ณด์ฌ์ ๋๋ ๋ด
        
        <img width="1074" alt="modeling" src="https://user-images.githubusercontent.com/104626180/202995601-4f2df3d9-1662-48d2-8cae-aac02f1f4a01.png">
        
    - 21๋ 9์ ~ 22๋ 6์ ๋ฐ์ดํฐ (distance + ์๋์ ๋์ง์ + 7์ ์๋์ ๋์ง์ ์ถ๊ฐ)
    - 7์ ๋ฐ์ดํฐ(distance + ์๋์ ๋์ง์ + 7์ ์๋์ ๋์ง์ ์ถ๊ฐ)
    - 22๋ 1์ ~ 7์ ๋ฐ์ดํฐ(distance + ์๋์ ๋์ง์ + 7์ ์๋์ ๋์ง์ + ์๋ณ ํ๊ท ์๋ ์ถ๊ฐ)
    - 22๋ 4์ ~ 7์ ๋ฐ์ดํฐ(distance + ์๋์ ๋์ง์ + 7์ ์๋์ ๋์ง์ + ์๋ณ ํ๊ท ์๋ ์ถ๊ฐ)
- models
    - LightGBM, CatBoost, XGBoost, GradientBoosing
    - optuna๋ฅผ ์ฌ์ฉํด์ ์ต์ ์ ํ์ดํผํ๋ผ๋ฏธํฐ๋ฅผ ์ฐพ์
- ensemble
    - ๊ฐ๊ฐ์ ๋ชจ๋ธ์์ ๋์จ ๊ฒฐ๊ณผ๊ฐ์ mean, median์ ์ด์ฉํด์ ensemble
    
    <img width="1020" alt="last" src="https://user-images.githubusercontent.com/104626180/202995684-d8a092ba-2ab4-40a0-a859-32438c97fc21.png">
    

### ****๐ย ๊ฒฐ๊ณผ****

- private score :  3.09375
- public score : 3.09759
    - 9๋ฑ /  712๋ฑ
