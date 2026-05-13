# mu-ui-lib

`mu-ui-lib` は、`mmemo` と `sail` で共通利用する Svelte コンポーネントや小さな UI ヘルパーを置くためのライブラリです。

## 置くもの

- 共通ボタン
- 共通カード
- モーダル
- フォーム部品
- アイコンやラベルの共通表示

## 使い方

このパッケージは、まずは workspace 内からソース参照する前提で置いています。
必要になったら、Svelte パッケージとして `exports` やビルド成果物を追加していけます。

## 共通部品

### ボタン

- `MuPrimaryButton`
  - 新規作成、保存、確定など、画面の主操作に使います
- `MuSecondaryButton`
  - 戻る、キャンセル、閉じるなど、補助操作に使います
- `MuDangerButton`
  - 削除など、取り消しにくい破壊的操作に使います

### 日付フィールド

- `MuDateField`
  - 日付の表示と編集を共通化したフィールドです
  - `editable={true}` で `<input type="date">`、`false` で日付ラベル表示になります

```svelte
<MuDateField bind:value={dateValue} editable={isNew} />
```
