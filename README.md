<br />
<p align="center">
  <a href="https://github.com/Gaepodong/Your-True-Review">
    <img src="https://fontmeme.com/permalink/200910/109ba0996778b6d9b99ce3ec7deee89e.png" alt="Logo" width="200" height="80">
  </a>

  <h2 align="center">Your-True-Review</h2>
  <h3 align="center">By Team Gaepodong</h3>

  <p align="center">
    감정분석 및 텍스트랭크를 이용한 영화 대표 리뷰 추출과 평점 부여 서비스
    <br />
    <a href="http://13.124.8.184:5000/movies/list/"><strong>Explore the Website »</strong></a>
    <br />
    <a href="https://www.youtube.com/watch?v=2W03KY3I_a4"><strong>Watch Youtube »</strong></a>
    <br />
    <a href="/감정분석 및 텍스트랭크를 이용한 영화 대표 리뷰 추출과 평점 부여 서비스.pdf"><strong>Read Paper »</strong></a>
    <br />
  </p>
</p>

## Table of Contents

- [About The Project](#about-the-project)
- [Built With](#built-with)
- [Getting Started](#getting-started)
- [Contact](#contact)

    
## About The Project

<p align="center">
    <img src="/image/webpage.png" alt="Logo" width="" height="500">
</p>

 __감정 분석 기법을 이용한 영화 평점 자동 부여 및 TextRank를 이용한 대표 리뷰 추출 시스템__    
  본 프로젝트는 영화 리뷰 댓글 데이터를 수집하여 댓글이 나타내는 긍/부정에 따라 평점을 매기고, 각 영화를 대표할 수 있는 리뷰를 보여주는 웹 서비스입니다.

## Built With
|Tools| Description |
|:-:|---|
|python| Crawling, Modeling, Web |
|flask| The web framework used |
|bootstrap| The web framework used |

### Server
|Server|Platform|
|:-:|---|
|Web|AWS EC2 Instance|
|API|Goorm IDE|

### USAGE API

```bash
curl -X POST http://13.124.54.4:51830/predict \
-d "text"="WANT_TO_ANALYZE_SENTENCE" 
```

API Return
- type: Dict
- output: {"emotion_percent": (float) ,"movie_rating": (int) ,"pos_or_neg": (0:negative or 1:positive)}

### Directories
```
.
├── API
│   └── app.py
├── LICENSE
├── README.md
├── data
│   ├── model
│   ├── output
│   └── wordcloud
├── get_model.py
├── image
├── macro.py
├── rawdata
├── textrank.py
└── web
    ├── config.py
    ├── init_db.sh
    ├── migrations
    ├── true_review
    ├── requirements.txt
    └── true_review.db

21 directories, 20 files
```

### Crawling Workflow
![image](/image/crawling_workflow.png)

### Model Workflow
![image](/image/model_workflow.png)

### Movie-BERT Workflow

#### 1. Model Architecture
<p>
    <img src="/image/movie_bert_arch.jpg" width="400">
</p>

#### 2. Task 1. Positive Negative Classification
<p>
    <img src="/image/movie_bert_cls.jpg" width="400">
</p>

#### 3. Task 2. Review Rating Regression
<p>
    <img src="/image/movie_bert_pred.jpg" width="400">
</p>


### Web Workflow
![image](/image/web_workflow.png)

## Getting Started

### Prerequisites

- python3
- python3-pip
- python venv
- mxnet-cu101
- glonnlp
- sentencepiece==0.1.85
- transformers==2.1.1
- torch==1.3.1
- konlpy (mecab)

### Installing

1. Clone the repository
```bash
git clone https://github.com/Gaepodong/Your-True-Review.git
```
2. Make Virtualenv and Activate
```bash
pip install virtualenv && virtualenv [NAME] && source .[NAME]/bin/activate
```
3. Set the environment variables
```bash
export FLASK_APP="true_review" FLASK_ENV="development" API_SERVER="http://13.124.240.211:55637/predict"
```
4. Change the directory and Install the requirements.
```bash
cd Your-True-Review/web && pip install -r requirements.txt
```
5. Run the Server
```bash
flask run
```
6. Enter the Sevice page
```
http://localhost:5000/update
```

### Abstract Key Sentences & Generate Wordcloud

1. Set device
```python
# get_model.py line:16

# if you use GPU, 
device = torch.device("cuda:0")
# if you use CPU,
device = torch.device("cpu")
```

2. [Download Model](https://drive.google.com/file/d/1kA1Yw1vahLPqrzgyLcy4J4XNXHxQXUxG/view?usp=sharing) and change "Model Path" 

```python 
# get_model.py line:102

# if you are using GPU,
self.to_model.load_state_dict(torch.load('MODEL_PATH'))
# if you are using CPU,
self.to_model.load_state_dict(torch.load('MODEL_PATH', map_location=device))
```

3. If you want to generate Korean wordcloud, Download the font to support encoding Korean and change "Font Path"
```python
# macro.py line:45.

font_path = 'FONT_PATH',
```
4. Run - Output will be stored in /data/
```bash
python macro.py
```

![image](/image/demonstration.gif)

## Contact

- yohlee - [@l-yohai](https://github.com/l-yohai)  
- sanam - [@simian114](https://github.com/simian114)  
- kylee - [@KyungKyuLee](https://github.com/KyungKyuLee)  
- jungwlee - [@LeejwUniverse](https://github.com/LeejwUniverse)  
- iwoo - [@humblEgo](https://github.com/humblEgo)  

## License

  - [Bootstrap](https://github.com/Gaepodong/Your-True-Review/blob/master/LICENSE/bootstrap)
  - [KoBERT](https://github.com/Gaepodong/Your-True-Review/blob/master/LICENSE/KoBERT)
