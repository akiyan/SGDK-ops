# 導入と試験

SGDK は `bin/` にビルド済みの jar を同梱する作りなので、フォークを clone すれば直った `xgm2tool.jar` が入っている。

```sh
git clone --depth 1 --branch akiyan https://github.com/akiyan/SGDK.git sgdk
java -jar sgdk/bin/xgm2tool.jar song.xgm song.xgc   # ループが残る
```

## jar を作り直す

Java のソースから作り直すときは JDK 21（javac）を用意する。SGDK には ant や maven の設定がないので、
`tools/xgm2tool/src` と、共通クラスの `tools/commons/src` を一度に javac に通す。

```sh
find sgdk/tools/xgm2tool/src sgdk/tools/commons/src -name '*.java' > sources.txt
javac -nowarn -d classes @sources.txt
jar --create --file xgm2tool.jar --main-class sgdk.xgm2tool.Launcher -C classes .
```

変更前のソースから作った jar は、同梱の `bin/xgm2tool.jar` と同じ出力になる（同じ入力で XGC がバイト一致）。
これを先に確かめてから修正を入れると、ビルド手順の間違いと修正の効果を分けて見られる。

## 試験

| 確かめること | やり方 |
|---|---|
| 他のツールの XGM のループが残る | mml2vgm（`mvcx64`、Format=XGM2）で作った `.xgm` を XGC にして、`loop: N frames` が 0 でないこと |
| VGM からの経路が変わらない | 同じ `.vgm` を修正前後の jar で XGC にして `cmp` |
| 実機で鳴る | SGDK の `XGM2` 資源としてビルドし、曲が最後まで行ってから頭（またはループ点）へ戻ること |
