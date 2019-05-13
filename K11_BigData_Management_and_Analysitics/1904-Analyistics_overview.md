# 1904-Analyistics_overview.md

## overview
- 
    + 

## key words

- 頻出パターンマイニング：frequency data mining

    - 膨大なデータに潜む規則性（rule)を自動的に抽出できる。（相関ルールの抽出）
    - 頻出パターンを列挙する手法
        - Apriori
            - 「長さkの非頻出item set」を含む「長さk+1のitem set」は常に非頻出である。Itemの出現頻度をもとに、アイテムセットを作る。
        - FP-Tree

- 相関ルール　： association rule

    - {A, B, C, \*} を満たすtransactionの中の{\*}の部分での頻出するItemをパターンとして抽出する

        [![Image from Gyazo](https://i.gyazo.com/11e3a6e4b582a5980bbcfd43e2bcaa49.png)](https://gyazo.com/11e3a6e4b582a5980bbcfd43e2bcaa49)

## contents

### ** データ分析事例

- (30p) 予習動画／復習動画／判別学習導入により、以下を実現できた。
    - 成績下位層の大幅削減
    - 成績中位層の高位層への移行
- (30p) 班別学習時の効果的な班構成
    - 現在、「当該科目の得意・不得意」「グループをまとめるリーダ的な役割が好きか嫌いか」「グループ学習が好きか嫌いか」のアンケートベースで多様な学生が１グループ（４～５名）になるように配慮しているものの、グループにより、うまくグループ学習ができるグループとそうでないグループがある。
- (30p) データ分析をもとにPDCAを回すことが重要

### ** Pattern Mining

- 解析対象

    - 購買履歴、行動履歴、Web Click Logs, Online PR, ゲノム、カルテ、事故データ・・・

- 課題＝＞break-throughが必要

    - 計算量爆発
    - 膨大な抽出パターン数
    - 抽出結果の理解困難性

- Apriori : 1994年にR. Agrawalら

    - 支持度(support)と確信度(confidence)に基づきruleを選択
    - Aprioriの問題は何か
        - 購買履歴のセット（TBD)やItem数が巨大になった場合

- FP-Tree : 2000年にJ. Hanら

    1. １回TDBにアクセスして、FP-TreeというHyper Treeを構築
    2.  頻出パターン抽出は、TDBにアクセスせずに、FP-Treeを再帰的にたどることで実現
    3.  FP-Treeが主記憶に入れば、高速化が期待できる。

    - FP-Treeの問題は何か

- 結果を正しく判断する

    - support
    - confidence
    - lift value

### ** Big DataによるruleのDomain空間の写像

- 学習：ヒトが経験から、自然に知識を身につけるという「学習」と同様の機能を、計算機が、データ（Facts）をもとに、Algorithmにより実現する。
    - 「知識」とは、何らかのruleとして記述できるもの
    - Aという知覚した事実に対して、何らかのrule（関数による写像）にっより、Cという結論を得る。この「関数による写像」をruleという。
    - ルールとは、図形空間的に考えると、「境目」(boundary)を決めること。
    - ルールとは、関数的に考えると、functionの重みパラメータを調整することで、ルールづけられる。
    - ルールとは、組み合わせ論的に考えると、組み合わせのassociation 分析、組み合わせ最適化といえる。

### ** BigDataの活用

![img](https://gyazo.com/e76f774619566a4554173bf252cf5220.png)
<https://gyazo.com/e76f774619566a4554173bf252cf5220>

![img](https://gyazo.com/a94ad86363943fbd0c30bbd62bfbc778.png)
<https://gyazo.com/a94ad86363943fbd0c30bbd62bfbc778>