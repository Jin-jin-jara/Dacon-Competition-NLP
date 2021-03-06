# Dacon-Competition-NLP

## Overview

올해 1월부터 7월까지 스미싱 범죄 건수는 17만6220건으로 지난해 같은 기간(14만5093건)에 비해 21.5% 증가했습니다.

특히 최근 교묘하고 지능적인 스미싱 문자 패턴으로 인해 고객들의 피해가 증가하고 있습니다. 이를 방지하기 위해 kb 금융그룹과 KISA는 데이코너들에게 도움을 요청합니다.

주최/주관
- 주최 : KB금융지주, DACON , KISA(한국인터넷진흥원)
- 주관 : DACON

## Problem Statement

데이콘 금융문자 분석 경진대회에서 풀어야하는 문제는 약 26만건의 문자 데이터를 분석하여 고객들이 받은 문자가 스미싱(금융사기)문자인지 은행에서 온 정상적인 문자인지를 구별하는 것입니다. test데이터 세트에 대한 auc score를 평가 기준으로 합니다. 

## Brief introduction to the data

id - 각 문자가 가지고 있는 고유 구분 번호입니다.(train Data와 public_test Data의 id는 중복되지 않습니다.)<br>
year_month - 고객이 문자를 전송 받은 년도와 월을 나타냅니다.<br>
text - 고객이 전송 받은 문자의 내용입니다. 이번 프로젝트의 핵심적인 데이터입니다.<br>
smishing - 해당 문자의 스미싱 여부입니다. (0 - 스미싱 아님(정상 문자), 1 -  스미싱)<br>

text 컬럼의 데이터는 개인정보 보호를 위해, 개인정보로 간주될 수 있는 이름, 전화번호, 은행 이름, 지점명은 X 혹은 *로 필터링 되어있습니다. 

## Model
전통적으로 강력하다고 여겨진 자연어 처리 모델을 사용했습니다. 사용한 모델은 Word2Vec모델과 Attention 기법이 사용된 양방향 LSTM 모델입니다.<br>

1. Word2Vec <br>
단어의 의미를 다차원 공간에 벡터화 하는 표현 방법을 분산 표현이라고 합니다. 분산 표현은 "비슷한 위치에 등장하는 단어들은 비슷한 의미를 가진다"는 가정을 기반으로 합니다. 분산 표현은 저차원에서 단어의 의미를 여러 차원에다 분산하여 표현하고 이런 표현 방법은 단어 간 유사도를 계산할 수 있습니다. 미리 훈련된 임베딩 벡터를 불러오는 방법도 있지만 저희는 갖고 있는 텍스트 데이터를 처음부터 학습시키는 방법을 택했습니다. 자주 함께 나오는 단어들은 trigram으로 최대 3단어까지 함께 묶어주었습니다.

2. Attention을 적용한 양방향 LSTM모델 <br>
고질적인 RNN의 문제점을 개선한 LSTM 모델을 바탕으로 시작했습니다. 후에 양방향 LSTM, 어텐션 기법을 적용한 양방향 LSTM모델을 사용해 모델을 개선시켰습니다. 
