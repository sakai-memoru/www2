# 1905-GDTA-Goal-Directed-Task-Analysis.md

## overveiew


## contents

### ** Goal Directed Task Analysis

#### * definition
- ユーザ要求を獲得するための手法
- ユーザの状況認知 (SA : Situation Awareness)に着目
    + ある環境下での現状認識(preception)や現状理解(comprehension)とそれによる予測(projection)からなる変化に対する一連の認知活動


#### * model

- ユーザのGoal（目標、目的）
- Goal達成のためのSub Task
- Sub Taskの達成のための判断基準(criteria)
- Sub Taskの達成の終了を判断する条件としてのFacts

https://www.researchgate.net/publication/292981760_Integrating_Human_Capabilities_into_Biosurveillance_Systems_A_Study_of_Biosurveillance_and_Situation_Awareness


[![Image from Gyazo](https://i.gyazo.com/057f48b197d74f1474664833d7b89130.png)](https://gyazo.com/057f48b197d74f1474664833d7b89130)

[![Image from Gyazo](https://i.gyazo.com/f67d9b2ec76c904a25750434ba17a758.png)](https://gyazo.com/f67d9b2ec76c904a25750434ba17a758)

[![Image from Gyazo](https://i.gyazo.com/3a47dbd6270f1136b8f1ae3c58d74588.png)](https://gyazo.com/3a47dbd6270f1136b8f1ae3c58d74588)

https://www.hm.tokoha-u.ac.jp/~nagasaki/note/2018/40/index.html

[![Image from Gyazo](https://i.gyazo.com/2f3ceb0c2c18cf71d39e23623b82fecd.png)](https://gyazo.com/2f3ceb0c2c18cf71d39e23623b82fecd)



### ** GDTAによるModel Design

- ヒトは、事実認識（現状認識:Facts）－解釈（現状理解:interpret）ー予測（predict)のサイクルに従い、行動(Action)を起こす意思決定(decision-making)をする。
- 現状の事実認識には、五感のsensorを使う。事実を知覚する際に、emotion(feeling)が発生する。
- どうModelingするか？
    - Emotion(Feeling:positive/negative)も判断の対象とする。
    - Factsを、十分に収集することを心がける
    - Interpret（Thinking）にあるbiasに気づく
    - predictは、行動時の選択肢の中で、確率的に、goalを達成しうる確率が高い行動の選択のこと

- User centered Disign
    - ユーザの状態は状況により変化する＝＞Decisionに向けてのSA (Situation Awareness：状況認知)が変わる＝＞Decisionが変わる
        - 「状態」　　＝＞ positive / negative
            - 身体的能力、身体的状態
            - 持ち物を含む身体的状態
            - 取り巻く環境（天候、混雑具合）
        - 「優先事項」＝＞ H-M-L

### ** User Centered Design との関係

- Action : 対象phaseにおける一般的なAction
- Opponent : 対象相手（外側にあるactorと捉えられる）
- Thinking : 状況(知覚した事実)に対するinterpret
- Feeling : 事実を知覚した時のemotion
- Insight : Thinking-Feelingを客観的に見ることにより得られる抽象的、論理的Thinking