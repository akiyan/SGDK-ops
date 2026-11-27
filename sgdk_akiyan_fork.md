# akiyan/SGDK の変更情報

| 項目 | 値 |
|---|---|
| 上流 | [Stephane-D/SGDK](https://github.com/Stephane-D/SGDK) |
| 上流基準 | `ef9292c`（`v2.11`） |
| 既定ブランチ | `akiyan` |
| 独自コミット | `a6ea53d` xgm2tool: keep the loop point of an XGM written by another tool |

## xgm2tool：他のツールが書いた XGM のループ点を残す

`xgm2tool` は VGM を読んだときだけ、コマンド列に**ループ開始印**（`LoopStartCommand`）を入れる。
XGC の書き出し、曲の長さ、XD3 タグは、すべてこの印からループを読む。

XGM ファイルはループを「最後のコマンド（`$FF dddddd`）のアドレス」として持つ。上流にはそれを印に戻す処理が
ないので、**他のツールが書いた XGM2 を読み込むとループが消え**、XGC にすると 1 回鳴って止まる曲になる。

未圧縮の XGM を読んだ後に、そのアドレスが指すコマンドへ印を付けるようにした（`XGM.restoreLoopStarts()`）。
圧縮ずみの XGM は上流にもともと「ループ点は復元できない」と注記があり、そちらは変えていない。

```java
// XGM.java（抜粋）
if (!packed)
{
    restoreLoopStarts();
    updateTimes();
}
```

FM と PSG の両方を見る。アドレスが `-1`（`0xFFFFFF`）のときはループなしとして何もしない。

- 変更したファイル：`tools/xgm2tool/src/sgdk/xgm2tool/format/XGM.java`（+59 行）、`bin/xgm2tool.jar`（再ビルド）
- 影響：VGM から変換する既定の経路は 1 バイトも変わらない（[検証](releases/2026-11-27.md)）
