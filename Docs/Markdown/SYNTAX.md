# Markdown 構文リファレンス

## 見出し

**h1 見出し**
```markdown
# 見出し1
```

**h2 見出し**
```markdown
## 見出し2
```

**h3 見出し**
```markdown
### 見出し3
```

**h4 見出し**
```markdown
#### 見出し4
```

**h5 見出し**
```markdown
##### 見出し5
```

**h6 見出し**
```markdown
###### 見出し6
```

## 強調・装飾

**太字**
```markdown
**太字のテキスト**
```

**斜体**
```markdown
*斜体のテキスト*
```

**太字と斜体**
```markdown
***太字かつ斜体のテキスト***
```

**取り消し線**
```markdown
~~取り消し線~~
```

**下線（HTML）**
```markdown
<u>下線付きテキスト</u>
```

## リスト

**順序なしリスト（-）**
```markdown
- 項目1
- 項目2
- 項目3
```

**順序なしリスト（*）**
```markdown
* 項目1
* 項目2
* 項目3
```

**順序付きリスト**
```markdown
1. 項目1
2. 項目2
3. 項目3
```

**ネストされたリスト**
```markdown
- 項目1
  - サブ項目1
  - サブ項目2
- 項目2
```

**チェックボックス**
```markdown
- [ ] 未完了タスク
- [x] 完了済みタスク
```

## リンク

**インラインリンク**
```markdown
[リンクテキスト](https://example.com)
```

**タイトル付きリンク**
```markdown
[リンクテキスト](https://example.com "タイトル")
```

**参照リンク**
```markdown
[リンクテキスト][ref]

[ref]: https://example.com
```

**自動リンク**
```markdown
<https://example.com>
```

**メールアドレス**
```markdown
<email@example.com>
```

## 画像

**基本的な画像**
```markdown
![代替テキスト](image.jpg)
```

**タイトル付き画像**
```markdown
![代替テキスト](image.jpg "画像タイトル")
```

**参照スタイルの画像**
```markdown
![代替テキスト][img-ref]

[img-ref]: image.jpg
```

**リンク付き画像**
```markdown
[![代替テキスト](image.jpg)](https://example.com)
```

**HTML画像（サイズ指定）**
```markdown
<img src="image.jpg" width="300" height="200" alt="代替テキスト">
```

## コードブロック

**インラインコード**
```markdown
`inline code`
```

**コードブロック（バッククォート）**
````markdown
```
code block
```
````

**言語指定付きコードブロック**
````markdown
```javascript
const hello = 'world';
```
````

**インデントによるコードブロック**
```markdown
    code block with indent
```

## 引用

**基本的な引用**
```markdown
> 引用テキスト
```

**複数行の引用**
```markdown
> 引用行1
> 引用行2
```

**ネストされた引用**
```markdown
> 引用レベル1
>> 引用レベル2
```

**引用内のMarkdown**
```markdown
> **太字**や*斜体*も使用可能
```

## テーブル

**基本的なテーブル**
```markdown
| ヘッダー1 | ヘッダー2 | ヘッダー3 |
| --- | --- | --- |
| データ1 | データ2 | データ3 |
| データ4 | データ5 | データ6 |
```

**左寄せ・中央・右寄せ**
```markdown
| 左寄せ | 中央 | 右寄せ |
| :--- | :---: | ---: |
| データ1 | データ2 | データ3 |
```

**シンプルな記法**
```markdown
ヘッダー1 | ヘッダー2
--- | ---
データ1 | データ2
```

## 水平線

**ハイフン3つ**
```markdown
---
```

**アスタリスク3つ**
```markdown
***
```

**アンダースコア3つ**
```markdown
___
```

## HTML埋め込み

**divタグ**
```markdown
<div align="center">
  中央寄せのコンテンツ
</div>
```

**色付きテキスト**
```markdown
<span style="color: red;">赤いテキスト</span>
```

**折りたたみ**
```markdown
<details>
<summary>クリックして展開</summary>

折りたたまれた内容

</details>
```

## 改行

**2つのスペース + Enter**
```markdown
行末に2つのスペース  
次の行
```

**brタグ**
```markdown
行1<br>行2
```

**空行**
```markdown
段落1

段落2
```

## エスケープ

**バックスラッシュでエスケープ**
```markdown
\* エスケープされたアスタリスク
\# エスケープされたハッシュ
\[ エスケープされた角括弧
```

## 脚注（拡張構文）

**脚注の定義**
```markdown
本文中の参照[^1]

[^1]: 脚注の内容
```

**複数行の脚注**
```markdown
本文中の参照[^note]

[^note]: 脚注の内容
    複数行も可能
```

## 数式（拡張構文）

**インライン数式**
```markdown
$E = mc^2$
```

**ブロック数式**
```markdown
$$
\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
$$
```

## 絵文字（GitHub拡張）

**絵文字コード**
```markdown
:smile:
:heart:
:rocket:
```

## アンカーリンク

**見出しへのリンク**
```markdown
[セクションへ移動](#見出し)
```

**HTML ID指定**
```markdown
<a id="custom-id"></a>
## 見出し

[カスタムIDへ移動](#custom-id)
```

## コメント

**HTML コメント**
```markdown
<!-- これはコメントです -->
```

## よく使う組み合わせ

**コードブロック内にバッククォート表示**
````markdown
````markdown
```
code
```
````
````

**画像とテキストを横並び**
```markdown
<img src="image.jpg" align="left" width="200">

テキストが画像の右側に表示されます。
```

**中央寄せの画像**
```markdown
<p align="center">
  <img src="image.jpg" alt="画像">
</p>
```

**バッジ（Shields.io）**
```markdown
![Badge](https://img.shields.io/badge/label-message-color)
```
