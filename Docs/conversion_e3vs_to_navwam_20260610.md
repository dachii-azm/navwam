# E3VS-Bench → NavWAM プロジェクトページ変換 (2026-06-10)

## 依頼内容の要約
`navwam_proj`（中身は別手法 E3VS-Bench のプロジェクトページ）を、NavWAM 論文
（`fix/NavigationWorldActionModel_Paper`）用のプロジェクトページに作り替える。
編集可能なのは `navwam_proj` 配下のみ。論文 PDF は変換元として読み取りのみ参照。

## 確定方針
- 著者: Daichi Azuma, Taiki Miyanishi, Koya Sakamoto, Shuhei Kurita, Yaonan Zhu,
  Petr Khrapchenkov, Motoaki Kawanabe, Yusuke Iwasawa, Yutaka Matsuo
  （所属の上付き番号割り当ては著者本人が後で実施 → TODO コメントで明示）
- Qualitative: 実機 rollout 動画を後日追加（placeholder スロット4枠）
- Paper / Code リンク: 未定 → `#` placeholder
- 図: PDF→PNG 変換は Claude が実施。数値結果は HTML テーブル、定性は図 PNG

## 変更・追加したファイル
- `index.html` … 全面書き換え（E3VS 内容を NavWAM の構成に置換）
- `README.md` … NavWAM 用に更新（構成・TODO・ローカルプレビュー手順）
- `static/figures/navwam/*.png` … 論文 PDF から変換・トリミングして新規作成
- `static/videos/navwam/README.txt` … 動画投入先の案内
- 削除: E3VS の `static/figures/*.png`（7枚）, `static/videos/output_ep*.mp4`（6本）

## 図アセットの生成
変換ツール: `pdftocairo -png -r 200 -singlefile`（poppler）。
PIL で必要領域に縦トリミング + 周囲余白の自動除去（下書きレイヤー除去のため）。

| 出力PNG | 変換元PDF | 用途 |
|---|---|---|
| teaser.png | fig/teaser_navwam.pdf | Teaser（NWM vs NWAM コンセプト）|
| architecture.png | fig/overview6.pdf | Method（9フレーム latent canvas）|
| realworld_foresight.png | fig/realworld_ftr.pdf | Preserving Visual Foresight |
| qualitative_realworld.png | fig/realworld5.pdf | 実機 rollout 軌跡 |
| robot_platform.png | supplementary/fig/diablo2.pdf | Diablo ロボット |
| value.png | supplementary/fig/value.pdf | goal-progress value |

（gostan7.pdf は realworld_ftr とほぼ重複だったため未使用）

## ページ構成（セクション）
1. Hero（タイトル・著者9名・Paper/Code placeholder）
2. Teaser（TL;DR + teaser.png）
3. Overview（論文 abstract）
4. Method（architecture.png + latent canvas / 3 mode 解説）
5. World Models as Policies（go stanford ATE/RPE テーブル）
6. Preserving Visual Foresight（subject consistency テーブル + foresight 図）
7. Learning Useful Futures for Control（head ablation + 直接ポリシー比較 SIT テーブル）
8. Closed-loop Real-Robot Deployment（実機 SR テーブル + 軌跡図 + 機体/value 図）
9. Qualitative Results（動画カルーセル placeholder）
10. BibTeX（azuma2026navwam）/ Footer（テンプレクレジット維持）

## 掲載した主要数値（論文の tab/*.tex より）
- go stanford: Cosmos+CEM 0.455/0.109, NWM 0.453/0.107, NavWAM 0.324/0.099, w/FT **0.192/0.070**
- Head ablation (ATE h4/h8): Img-only 0.326/0.569 → +Act+St 0.107/0.287 → +Val **0.076/0.192**
- 直接ポリシー(SIT): OmniVLA 0.086/0.162, NavWAM **0.077/0.144**（SR 46.3/15.9）
- Subject consistency: NWM 0.524, NavWAM **0.668**, w/FT 0.635
- 実機 SR: NWM 16.7%, OmniVLA 58.3%, NavWAM **79.2%**（19/24）

## 動作確認
- E3VS 残存語彙の全件スキャン → クリーン（ヒットは著者URL `k0uya` と通常語 "benchmark" の誤検出のみ）
- ローカル参照アセット存在チェック → 全 OK（rollout mp4 4本のみ意図的 placeholder）
- HTML タグ整合（section/div/table/tr）→ OK（テンプレ由来の section 即閉じバグも修正）
- `python3 -m http.server` で index.html / 画像が HTTP 200 で配信されることを確認

## 残TODO（公開前に著者対応）
- 著者の所属上付き番号の割り当て（`<!-- TODO(author) -->`）
- Paper / Code の実 URL、BibTeX の arXiv id
- `static/videos/navwam/rollout1〜4.mp4` の投入
- favicon の差し替え（任意）
