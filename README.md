# VST-NJ8に基づく高校生向けオンライン版語彙サイズテスト（GDGT）

**GDGT** は，VST-NJ8（Hamada et al., 2021）に基づいて作成された，高校生向けのオンライン版語彙サイズテストです。Google スプレッドシートと Google Apps Script を利用することで，独自サーバーを用意せずに，ブラウザ上でテストを実施し，回答結果を Google スプレッドシートに自動保存できます。

<br><br>

## 主な特徴

- VST-NJ8 のレベル 3〜5 から選定した 60 項目を使用
- 4 択形式，1 項⽬解答時間 5 秒，全体で約 5 分程で実施可能
- 受験直後に正答数・正答率・推定語彙サイズを表示
- 回答結果を教員の Google スプレッドシートに自動保存
- Google Apps Script により，サーバー不要で運用可能
- PC・スマートフォンのブラウザで実施可能

## 
> **コピー用スプレッドシート**  
> https://docs.google.com/spreadsheets/d/1JQWdXC0oF0zcegbxAZybgV0QBn7-CnxuafXa-AtytCg/edit?usp=sharing

<br><br>

## リリースバージョン
v.1.0.0

<br><br>

## 利用手順

詳しい利用手順は [USAGE.md](USAGE.md) を参照してください。

<br><br>

## 公開Googleスプレッドシート内に含まれる主な構成ファイルおよびライセンス

本プロジェクト（公開されているGoogle Spread Sheet）には、異なるライセンスが適用されるコードおよびデータが含まれています。
各ファイルの出典、変更内容、および適用ライセンスの詳細については、[LICENSE.md](LICENSE.md)をご確認ください。

| 構成ファイル | 内容 | ライセンス |
|---|---|---|
| `code.gs` | Google Apps Script 側の処理 | MIT License |
| `menu.gs` |スプレッドシートへのメニュー「GDGT管理」追加 | MIT License |
| `index.html` | 受験画面・JavaScript 処理（IRT推定処理を含む） | MIT License |
| `beep_base64.txt` | ビープ音をBase64エンコードしたデータ | MIT License |
| `data.txt` | VST-NJ8 レベル 3〜5 の 60 項目に基づくテスト項目データ | CC BY-NC-SA 4.0 |
| `vst_nj8_parameters.json` | VST-NJ8 に基づくパラメータおよび等化係数 | CC BY-NC-SA 4.0 |
| `ItemEstimate.txt` | JSPS 科研費 24K00084 において高校生に実施した語彙テスト結果に基づく項目パラメータ | CC BY-NC-SA 4.0 |


## クレジット

* `data.txt`に含まれるテスト項目および`vst_nj8_parameters.json`に含まれるVST-NJ8のパラメータは、濱田研究室のウェブサイトで公開されている`VST_OpenData_Scoring.xlsx`のデータに基づいています。
  https://hamada-lab.jp/

* VST-NJ8の開発研究：

> Hamada, A., Iso, T., Kojima, M., Aizawa, K., Hoshino, Y., Sato, K., Sato, R., Chujo, J., & Yamauchi, Y. (2021). Development of a vocabulary size test for Japanese EFL learners using the New JACET List of 8,000 Basic Words. *JACET Journal, 65*, 23–45. https://doi.org/10.32234/jacetjournal.65.0_23

* `ItemEstimate.txt`に含まれる項目パラメータは、JSPS科研費24K00084の助成を受けた研究プロジェクトにおいて実施した語彙テストの結果に基づいています。

<br><br>

## 論文等での引用

- 論文等で本アプリを引用する際には、以下を参考にしてください。
1) 古泉隆・杉浦正利・村尾玲美・阿部大輔・古泉隆・江口朗子・阿部真理子・鈴木駿吾 (2026年8月19日). 『VST-NJ8に基づく高校生向けオンライン版語彙サイズテストの開発』［学会発表］ 外国語教育メディア学会 (LET) 第65回 (2026) 年次研究大会.
2) 古泉隆 (2026). 『VST-NJ8に基づく高校生向けオンライン版語彙サイズテスト（GDGT）』 (v1.x.x) [ソフトウェア]. GitHub repository: https://github.com/tkz-linglab/gdgt

<br><br>

## 注意事項・免責事項

- 本アプリを利用するには，利用者自身の Google アカウントでスプレッドシートをコピーし，Apps Script をデプロイする必要があります。
- デプロイ時に Google の認証・警告画面が表示される場合があります。これは，コピーした Apps Script が利用者自身の Google スプレッドシートに回答結果を書き込むためです。
- 回答データは，利用者（教員等）のGoogleアカウントにコピーしたスプレッドシートに保存されます。個人情報の取り扱いについては，各所属機関の方針に従ってください。
- このオンラインテストは教育目的での利用を想定しています。本テストおよびテスト項目を含むデータの商用利用は，CC BY-NC-SA 4.0 の条件により認められません。
- 本アプリの利用により生じたいかなる損害・不利益について，開発者は責任を負いません。各実施環境で事前に動作確認を行うことを推奨します。
- Googleスプレッドシートを利用しているため、Google側のサービス稼働状況によっては、処理の遅延やアクセス障害等が発生する可能性があります。
- 本アプリの仕様および内容は、今後変更する場合があります。

<br><br>

## 技術的補足

### Google Apps Script

本アプリは、Googleスプレッドシートに紐づくGoogle Apps Scriptプロジェクトとして実装されています。

### IRT推定および等化

`ItemEstimate.txt`に含まれる項目パラメータは、高校生の回答データをRパッケージ`ltm`の2パラメータ・ロジスティックモデル（2PL）で分析して推定したものです。

`vst_nj8_parameters.json`に含まれる等化係数は、高校生データから推定した項目パラメータとVST-NJ8のパラメータに基づき、Rパッケージ`plink`のMean/Sigma法を用いて算出したものです。

アプリにおける能力値θは、経験ベイズ型推定により、事後分布が最も高くなるθ（MAP推定値）として求めています。この処理はJavaScriptで実装し、実装結果の整合性を確認する際には、Rパッケージ`ltm`の`factor.scores(method = "EB")`による推定値を参考にしています。

<br><br>

### 問い合わせフォーム
https://forms.cloud.microsoft/r/AU4FjcUmmn


