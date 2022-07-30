# AI-CT
**연구개발특구 AI SPARK 챌린지(인공지능 경진대회)**   
AI 감정 기록 및 상담 서비스 개발 프로젝트 - 팀 AI-CT  
  


# Description

**< 사용한 데이터 셋 >**
https://drive.google.com/drive/folders/1OU2s36s3xl_Q3jAiplFoghK0iylvnYZO?usp=sharing

-   ETRI 나눔 AI 플랫폼 - 음성 감정 인식 데이터셋
-   AI 허브 - 감성 대화 말뭉치
-   ETRI 나눔 AI 플랫폼 - 한국어 멀티 모달 감정 데이터셋 2020

위의 데이터를 활용하여 10가지의 감정과 4가지의 강도로 분류하는 알고리즘 개발

우리는 감정을 제대로 표출해내지 못하는 사람들을 위한 AI 상담 서비스를 기획하였다.

즉, 실제 슬픈감정임에도 불구하고 텍스트로는 그 감정을 담아내지 못하는 사람들을 대상으로 하기 때문에 ‘텍스트 데이터’가 아닌, ‘음성 파일 자체’에서 음성 특성을 추출해 데이터를 활용하도록 한다.

-   현재 대부분 음성관련 데이터 활용 방식을 보면 음성의 텍스트 데이터만을 활용하여 알고리즘을 구성하는 자연어처리(NLP)방식이 많다.
-   인간의 말하기 활동은 혀와 턱, 입술, 후두를 세밀하게 조정하는 복잡한 행위로, 신경 조절에 이상이 있거나 기관 중 하나라도 문제가 생기면 즉각 말투나 목소리가 달라진다. 사고가 느려지면서 빠른 판단과 행동을 가로막기 때문이다.
-   MFCC 알고리즘 및 다양한 알고리즘을 활용하면 음성 데이터를 특징 벡터화 하여 사용할 수 있다.

![https://miro.medium.com/max/633/1*7sKM9aECRmuoqTadCYVw9A.jpeg](https://miro.medium.com/max/633/1*7sKM9aECRmuoqTadCYVw9A.jpeg)

-   음성 데이터 Augmentation
    -   noise
    -   stretching
    -   shifting
    -   pitching

원본 음성 데이터에서 새로운 샘플들을 만들어내는 과정이다. noise injection, shifting time, changing pitch and speed를 적용한다

-   음성 데이터에서 Feature Extraction
    -   Zero Crossing Rate : 특정 프레임이 지속되는 동안 신호의 부호 변화율입니다.
    -   Chroma_stft
        -   Chroma Vector : 12가지 동일한 성질의 음높이 클래스를 나타내는 스펙트럼 에너지의 12요소 표현(반음 간격).
        -   Chroma Deviation : 12개의 크로마 계수의 표준 편차입니다.
    -   MFCC
        -   MFCCs Mel Frequency Cephrusic 계수는 주파수 대역이 선형적이지 않고 멜 척도에 따라 분포하는 두상표현을 형성합니다.
    -   RMS(root mean square) value
    -   MelSpectogram


# Data

### **데이터 개요**

-   사용한 데이터는 ETRI 나눔 AI 플랫폼에서 제공하는 음성 감정 인식 데이터셋, 한국어 멀티 모달 감정 데이터 셋 2020 그리고 AI 허브에서 제공하는 감성대화 말뭉치 데이터를 활용하였습니다.
-   제공된 데이터 셋은 주어진 상황에 참가자들의 발화 내용이 음성 데이터(wav)로 담겨져있습니다.
-   음성 데이터 정보를 csv 형식으로 라벨링 되어있습니다.

### **데이터 전처리**

-   학습 데이터는 'AI-CT' 폴더에 위치하며 데이터 ( Ravdess.zip, CremaD.zip, CremaDinfo.zip, Savee.zip, Tess.zip, KEManno.zip, data.zip ) 을 활용합니다.
-   Combined_df.csv : 6가지 데이터 셋을 통일된 칼럼으로 합친 데이터프레임 파일
-   features.csv : 모델링을 위해 필요한, 모델링에 사용될 Feature 데이터들을 뽑아내는 과정을 담은 파일


**< 데이터를 뽑아내는 과정 >**

-   **Data Augmentation**
    -   "원본 original 음성 data"에서 "noise해서 얻은 data", "stretch 및 pitch를 해서 얻은 data" 를 새로 생성해 Data Augmentation을 진행했다.즉, 데이터는 (원본 데이터, noise해서 얻은 데이터, stretch 및 pitch를 해서 얻은 데이터)로 3배 늘어난다.
-   **Feature Extraction**
    -   1번 Data Augmentation을 거친 후, 모든 데이터들에 대해 ( ZCR, Chroma_stft, MFCC, RMS, MelSpectogram)의 feature를 추출해낸다.

**< 기타 파일 폴더 구조 >**

-   / AI-CT
    -   / Ravdess.zip
        -   /audio_speech_actors_01-24
    -   / CremaD.zip
        -   /AudioWAV
    -   /cremadinfo.csv
    -   / Savee.zip
        -   / AudioData
    -   / Tess.zip
        -   / tess toronto emotional speech set data/TESS Toronto emotional speech set data/
    -   / KEMDy20
        -   / annotation
        -   / wav
-   / data.zip
    -   / male_5000
    -   / female_5000
    -   test_out.json
    -   sentence.xlsx : 음원의 간단한 정보와 객체 감정 정보가 기록

**각 데이터 셋의 자세한 분석을 보기위해 [여기를](https://url.kr/3z8kp2) 클릭해주세요.**

**< Gender / Emotion / Age / Path / Intensive >**

해당 칼럼에는 각각 아래와 같이 세부 사항이 존재합니다.

**<Gender> - 발화자의 성별**

-   Female - 여성
-   Male - 남성
-   None - 없음

**<Emotion> - 음성의 감정 분류**

-   기쁨(Happy)
-   슬픔(Sad)
-   분노(Anger)
-   혐오(Disgust)
-   공포(Fear)
-   놀람(Surprise)
-   중립(Neutral)
-   당황(Embarrassed)
-   불안(Anxiety)
-   상처(Wound)

**<Age> - 발화자의 연령대**

-   Senior (60세 ~ ) - 노년
-   Middle-aged ( ~ 59세) - 중년
-   Youth ( ~ 39세) - 청년
-   Teenager ( ~ 19세) - 청소년

**<Path> - 음성데이터(.wav)의 파일 경로**

-   (음성)데이터 경로

**<Intensive> - 음성의 강도**

-   None - 없음
-   Low - 낮음
-   Middle - 중간
-   High - 높음



# Presentation Slides

![AI-CT 발표자료_page-0004](https://user-images.githubusercontent.com/62376361/166525787-b35ebfb5-6ae0-4465-8004-f1069d77903a.jpg)
![AI-CT 발표자료_page-0005](https://user-images.githubusercontent.com/62376361/166525789-6deb3ee3-775f-406c-afc2-6a3af3a78f06.jpg)
![AI-CT 발표자료_page-0006](https://user-images.githubusercontent.com/62376361/166525793-b41ab284-c75e-4d17-a3e0-b139797ba7d1.jpg)
![AI-CT 발표자료_page-0007](https://user-images.githubusercontent.com/62376361/166525796-528c14f2-5106-4935-a0d6-c21459961c44.jpg)
![AI-CT 발표자료_page-0008](https://user-images.githubusercontent.com/62376361/166525800-7eef7266-2a36-45d9-9c29-0b50a80f8462.jpg)
![AI-CT 발표자료_page-0009](https://user-images.githubusercontent.com/62376361/166525805-2beeb6fa-eb28-4be9-ab90-1b1419368baf.jpg)
![AI-CT 발표자료_page-0010](https://user-images.githubusercontent.com/62376361/166525806-512cac6a-93dd-4b47-9036-73449b4b09cb.jpg)
![AI-CT 발표자료_page-0011](https://user-images.githubusercontent.com/62376361/166525811-8871255c-e90b-40d0-bd67-3d4b0bc1a5f7.jpg)
![AI-CT 발표자료_page-0012](https://user-images.githubusercontent.com/62376361/166525814-69ca53fa-fc1f-4a44-a593-1b39b83ce073.jpg)
![AI-CT 발표자료_page-0013](https://user-images.githubusercontent.com/62376361/166525817-4b8ae2fb-4f51-491a-8d77-6db15996fbb5.jpg)
![AI-CT 발표자료_page-0014](https://user-images.githubusercontent.com/62376361/166525821-b4e8a4da-0616-4f57-9e4b-37039d096ff6.jpg)
![AI-CT 발표자료_page-0015](https://user-images.githubusercontent.com/62376361/166525825-6cd60a8e-e728-48cb-a3a0-47f646e829f9.jpg)
![AI-CT 발표자료_page-0016](https://user-images.githubusercontent.com/62376361/166525828-3dfc5daf-ffa8-4254-b61a-e11196a58a85.jpg)
![AI-CT 발표자료_page-0017](https://user-images.githubusercontent.com/62376361/166525832-62c301a6-388f-4ba9-adc4-9d4ecf2c4aa0.jpg)
![AI-CT 발표자료_page-0018](https://user-images.githubusercontent.com/62376361/166525836-65e1a58e-a896-4b33-8bda-c89f9c830bdf.jpg)
![AI-CT 발표자료_page-0019](https://user-images.githubusercontent.com/62376361/166525838-6b400cc1-fc1d-417d-bff4-ad20dea998d0.jpg)
![AI-CT 발표자료_page-0020](https://user-images.githubusercontent.com/62376361/166525842-3935651d-ac85-444e-a3a6-7cab7016df1e.jpg)
![AI-CT 발표자료_page-0021](https://user-images.githubusercontent.com/62376361/166525845-cadde278-7d3e-4b04-841e-d934a39bc805.jpg)
![AI-CT 발표자료_page-0022](https://user-images.githubusercontent.com/62376361/166525850-35e8e6db-7ba0-4fc4-a2dc-226ee2e896d7.jpg)
![AI-CT 발표자료_page-0023](https://user-images.githubusercontent.com/62376361/166525855-6711c884-ae15-453f-9d6f-f1203f8a2afc.jpg)
![AI-CT 발표자료_page-0024](https://user-images.githubusercontent.com/62376361/166525858-32253b70-78c5-40aa-ba66-9564342b5027.jpg)
![AI-CT 발표자료_page-0025](https://user-images.githubusercontent.com/62376361/166525859-911b61db-b074-4d44-b4f3-f94ac6e2407d.jpg)
![AI-CT 발표자료_page-0026](https://user-images.githubusercontent.com/62376361/166525863-540a7798-d5b7-4f44-a92a-7e4b9d3365c6.jpg)
![AI-CT 발표자료_page-0027](https://user-images.githubusercontent.com/62376361/166525865-00389486-0c0e-4036-bb1b-55212cedae62.jpg)
![AI-CT 발표자료_page-0028](https://user-images.githubusercontent.com/62376361/166525867-1790d08e-1d59-4ccd-9941-4e9c50079a60.jpg)
![AI-CT 발표자료_page-0029](https://user-images.githubusercontent.com/62376361/166525871-fdd24552-f6de-4523-b2ac-7c9c1f2e1511.jpg)
