[English](./README.md) [Korean](./README_ko.md)
# 機械学習システム デザインパターン
機械学習システムを本番稼働させるために必要な学習、推論、運用のアーキテクチャ・デザイン・パターン集です。

## 目的
このドキュメントの目的は機械学習システムを本番稼働させるためのシステム・デザイン・パターンを説明することです。<br>
このドキュメントは機械学習のモデル開発でパフォーマンスを向上させる方法（正解率やRMSE）を説明するものではありませんが、パターンによってはその手法に言及することもあります。
<br>

## 前提
このドキュメントで書かれる機械学習システムパターンのほとんどは、パブリック・クラウドおよびKubernetesを使って稼働させることを前提に記述されています。特定のプログラミング言語に依存しない内容にするよう努めますが、機械学習で使われる最もポピュラーな言語がPythonであるため、ほとんどのデザイン・パターンはPythonで構築可能なものとなっています。
<br>

## 読み物として
読みやすいフォーマットはこちらをご参照ください。<br>
[GitHub Pages](https://mercari.github.io/ml-system-design-pattern/README_ja.html)

## 実装例
一部の実装例を以下で公開しました。
https://github.com/shibuiwilliam/ml-system-in-actions

## Patterns
### [Serving patterns](./Serving-patterns/README_ja.md)
本番サービスで推論サーバを稼働させ運用するパターン。
- [Web Single Pattern](./Serving-patterns/Web-single-pattern/design_ja.md)


- [Synchronous Pattern](./Serving-patterns/Synchronous-pattern/design_ja.md)


- [ASynchronous Pattern](./Serving-patterns/Asynchronous-pattern/design_ja.md)


- [Batch pattern](./Serving-patterns/Batch-pattern/design_ja.md)


- [Prep-pred pattern](./Serving-patterns/Prep-pred-pattern/design_ja.md)


- [Microservice vertical pattern](./Serving-patterns/Microservice-vertical-pattern/design_ja.md)


- [Microservice Horizontal Pattern](./Serving-patterns/Microservice-horizontal-pattern/design_ja.md)


- [Prediction Cache Pattern](./Serving-patterns/Prediction-cache-pattern/design_ja.md)


- [Data Cache Pattern](./Serving-patterns/Data-cache-pattern/design_ja.md)


- [Prediction Circuit Break Pattern](./Serving-patterns/Prediction-circuit-break-pattern/design_ja.md)


- [Multiple stage prediction pattern](./Serving-patterns/Multiple-stage-prediction-pattern/design_ja.md)

- [Serving template pattern](./Serving-patterns/Serving-template-pattern/design_ja.md)

- Edge prediction pattern: To do


- [Antipatterns](./Serving-patterns/Anti-patterns/README_ja.md)

  - [Online Bigsize Anti-Pattern](./Serving-patterns/Anti-patterns/Online-bigsize-pattern/design_ja.md)

  - [All-In-One Anti-Pattern](./Serving-patterns/Anti-patterns/All-in-one-pattern/design_ja.md)

### [QA patterns](./QA-patterns/README_ja.md)
機械学習のモデルおよび推論器を評価するためのパターン。
- [Shadow AB-testing pattern](./QA-patterns/Shadow-ab-test-pattern/design_ja.md)


- [Online AB Test Pattern](./QA-patterns/Online-ab-test-pattern/design_ja.md)


- [Loading test pattern](./QA-patterns/Loading-test-pattern/design_ja.md)


- [Antipatterns](./QA-patterns/Anti-patterns/README_ja.md)

  - [Offline-only pattern](./QA-patterns/Anti-patterns/Offline-only-pattern/design_ja.md)

### [Training patterns](./Training-patterns/README_ja.md)
学習パイプラインを構成するパターン。
- [Batch Training Pattern](./Training-patterns/Batch-training-pattern/design_ja.md)


- [Pipeline Training Pattern](./Training-patterns/Pipeline-training-pattern/design_ja.md)


- [Parameter and Architecture Search Pattern](./Training-patterns/Parameter-and-architecture-search-pattern/design_ja.md)


- [Antipatterns](./Training-patterns/Anti-patterns/README_ja.md)

  - [Only-Me Anti-Pattern](./Training-patterns/Anti-patterns/Only-me-pattern/design_ja.md)

  - [Training Code in Serving Anti-Pattern](./Training-patterns/Anti-patterns/Training-code-in-serving-pattern/design_ja.md)

  - [Too Many Pipes Anti-Pattern](./Training-patterns/Anti-patterns/Too-many-pipes-pattern/design_ja.md)


### [Operation patterns](./Operation-patterns/README_ja.md)
推論器を管理、運用するためのパターン。
- [Model-In-Image Pattern](./Operation-patterns/Model-in-image-pattern/design_ja.md)


- [Model-Load Pattern](./Operation-patterns/Model-load-pattern/design_ja.md)


- [Data model versioning pattern](./Operation-patterns/Data-model-versioning-pattern/design_ja.md)


- [Prediction Log Pattern](./Operation-patterns/Prediction-log-pattern/design_ja.md)


- [Prediction Monitoring Pattern](./Operation-patterns/Prediction-monitoring-pattern/design_ja.md)


- [Parameter-Based Serving Pattern](./Operation-patterns/Parameter-based-serving-pattern/design_ja.md)


- [Condition-based-serving pattern](./Operation-patterns/Condition-based-serving-pattern/design_ja.md)


- [Antipatterns](./Operation-patterns/Anti-patterns/README_ja.md)

  - [No Logging Pattern](./Operation-patterns/Anti-patterns/No-logging-pattern/design_ja.md)

  - [Nobody knows pattern](./Operation-patterns/Anti-patterns/Nobody-knows-pattern/design_ja.md)

### [Lifecycle patterns](./Lifecycle-patterns/README_ja.md)
複数のパターンを組み合わせて機械学習システム全体を構成するパターン。
- [Train-Then-Serve Pattern](./Lifecycle-patterns/Train-then-serve-pattern/design_ja.md)


- [Training-To-Serving Pattern](./Lifecycle-patterns/Training-to-serving-pattern/design_ja.md)


- [Antipatterns](./Lifecycle-patterns/Anti-patterns/README_ja.md)

  - Todo

---

## Committers

 * Yusuke Shibui ([@shibuiwilliam](https://github.com/shibuiwilliam))
 * Sung Yun Byeon ([@zzsza](https://github.com/zzsza))
 * Jiyeon Seo ([@jiyeonseo](https://github.com/jiyeonseo))
 * Daeyoon Jin ([@zetbouaka](https://github.com/zetbouaka))

## Contribution

新たにパターンを追加する場合は[template_design.md](./template_design.md)を使用して執筆し、Issueを作成した後にPRを送ってください。<br>
新たにアンチパターンを追加する場合は[template_antipattern.md](./template_antipattern.md)を使用して執筆し、Issueを作成した後にPRを送ってください。<br>
修正や変更、疑問を呈する場合はIssueを作成してください。<br>

Please read the CLA carefully before submitting your contribution to Mercari.
Under any circumstances, by submitting your contribution, you are deemed to accept and agree to be bound by the terms and conditions of the CLA.

https://www.mercari.com/cla/

## License

Copyright 2020 Mercari, Inc.

Licensed under the [MIT License](LICENSE).
