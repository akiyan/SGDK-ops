# SGDK-ops

`Stephane-D/SGDK` を直接フォークした `akiyan/SGDK` の変更情報、導入手順、検証記録を管理する。
実装と試験、機能や不具合の Issue は本体に置く。 [SGDK 本体](https://github.com/akiyan/SGDK/tree/akiyan) · [Issue](https://github.com/akiyan/SGDK/issues)

既定ブランチの `akiyan` は、固定した上流コミットに独自差分を 1 コミット載せる。
初回は SGDK 2.11 を基準に、**他のツールが書いた XGM ファイルのループ点が失われる**不具合を直した。
[変更情報](sgdk_akiyan_fork.md) · [上流 2.11](https://github.com/Stephane-D/SGDK/releases/tag/v2.11)

AI の自動操作や高速な反復の効率がよくなる変更、および他のツールとつなぐときに必要な修正を、特定のタイトルに
依存しない汎用の形で加える。

- [導入と試験](docs/setup.md)
- [最初の修正の検証記録](releases/2026-11-27.md)

ここに置く文書は MIT ライセンス。本体のライセンスは上流（MIT）に従う。 [文書のライセンス](LICENSE)
