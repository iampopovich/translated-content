---
title: break-after
slug: Web/CSS/break-after
l10n:
  sourceCommit: 429d45679a29f386af0ddfcf2a64498843c3e1e5
---

{{CSSRef}}

**`break-after`** は [CSS](/ja/docs/Web/CSS) のプロパティで、生成されたボックスの後で、ページ、段、領域をどのように区切るかを設定します。ボックスが生成されない場合は、このプロパティは無視されます。

{{InteractiveExample("CSS デモ: break-after")}}

```css interactive-example-choice
break-after: auto;
```

```css interactive-example-choice
break-after: page;
```

```html-nolint interactive-example
<section id="default-example">
  <div>
    <p>
      このプロパティの効果は、文書が印刷される時、または印刷のプレビューが表示された時に確認できます。
    </p>
    <button id="print-btn">印刷プレビューを表示</button>
    <div class="box-container">
      <div class="box">プロパティの前のコンテンツ</div>
      <div class="box" id="example-element">'break-after' の付いたコンテンツ</div>
      <div class="box">プロパティの後のコンテンツ</div>
    </div>
  </div>
</section>
```

```css interactive-example
.box {
  border: solid #5b6dcd 5px;
  background-color: #5b6dcd;
  margin: 10px 0;
  padding: 5px;
}

#example-element {
  border: solid 5px #ffc129;
  background-color: #ffc129;
  color: black;
}

.hide-element {
  display: none;
}
```

```js interactive-example
const btn = document.getElementById("print-btn");
const editorContainer = document.getElementsByClassName(
  "css-editor-container",
)[0];
const exampleHTMLElement = document.getElementById("default-example");

const printableSection = document.createElement("div");
printableSection.setAttribute("id", "printable-section");
printableSection.classList.add("hide-element");
document.body.appendChild(printableSection);

btn.addEventListener("click", () => {
  const exampleContent = exampleHTMLElement.innerHTML;

  editorContainer.classList.add("hide-element");
  printableSection.innerHTML = exampleContent;
  printableSection.classList.remove("hide-element");

  window.print();

  printableSection.classList.add("hide-element");
  printableSection.innerHTML = "";
  editorContainer.classList.remove("hide-element");
});
```

## 構文

```css
/* 一般の区切り値 */
break-after: auto;
break-after: avoid;
break-after: always;
break-after: all;

/* 改ページ値 */
break-after: avoid-page;
break-after: page;
break-after: left;
break-after: right;
break-after: recto;
break-after: verso;

/* 段区切り値 */
break-after: avoid-column;
break-after: column;

/* 領域区切り値 */
break-after: avoid-region;
break-after: region;

/* グローバル値 */
break-after: inherit;
break-after: initial;
break-after: revert;
break-after: revert-layer;
break-after: unset;
```

区切り位置になる可能性のある場所 (言い換えれば、要素の境界) は、3 つのプロパティに影響されます。前の要素の `break-after` の値、次の要素の {{cssxref("break-before")}} の値、包含要素の {{cssxref("break-inside")}} の値です。

分割が行われるかどうかを判断するためには、以下の規則が適用されます。

1. 考慮される 3 つの値の中の何れかに*区切りを強制する値* (`always`, `left`, `right`, `page`, `column`, `region` の何れか) がある場合、それが優先されます。そのような区切りが複数ある場合は、フローの中で最も後に現れる要素のものが使用されます (つまり、 `break-before` の値は `break-after` の値より優先し、それは更に `break-inside` よりも優先します)。
2. 考慮される 3 つの値の中に*区切りを防止する値* (`avoid`, `avoid-page`, `avoid-region`, `avoid-column` の何れか) が含まれていた場合は、その場所で区切りは適用されません。

強制的な区切りが適用されると、必要に応じてソフトな区切りが追加される場合がありますが、 `avoid` に関する値に解決される要素の境界には追加されません。

### 値

#### 一般の区切り値

- `auto`
  - : 該当するボックスの直後に何らかの (ページ、段、領域の) 区切りを挿入することを許可しますが、強制はしません。
- `avoid`
  - : 該当するボックスの直後に何らかの (ページ、段、領域の) 区切りを挿入することを禁止します。
- `always`
  - : 該当するボックスの直後で強制的に改ページを行います。この区切りの種類は断片化のコンテキストを直接含むものです。段組みコンテナーの中であれば強制的な段区切りとなり、ページ付きメディアの (ただし段組みコンテナーの中ではない) 場合はページ区切りになります。
- `all`
  - : 該当するボックスの直後で強制的に改ページを行います。すべての分断しうるコンテキストを通して区切ります。よって、段組みコンテナーの中での区切りは、ページコンテナーの中であれば強制的に段組みとページを区切ります。

#### 改ページ値

- `avoid-page`
  - : 該当するボックスの直後の改ページを禁止します。
- `page`
  - : 該当するボックスの直後で改ページを行います。
- `left`
  - : 該当するボックスの直後で 1 つまたは 2 つの改ページを行い、次のページが左ページになるようにします。横書きの本では、本の背の左側に置かれているページ、両面印刷では裏側のページです。
- `right`
  - : 該当するボックスの直後で 1 つまたは 2 つの改ページを行い、次のページが右ページになるようにします。横書きの本では、本の背の右側に置かれているページ、両面印刷では表側のページです。
- `recto`
  - : 該当するボックスの直後で一つまたは二つの改ページを行い、次のページが奇数ページになるようにします。 (奇数ページは左から右に開く場合は右ページになり、右から左に開く場合は左ページになります。)
- `verso`
  - : 該当するボックスの直後で一つまたは二つの改ページを行い、次のページが偶数ページになるようにします。 (奇数ページは左から右に開く場合は左ページになり、右から左に開く場合は右ページになります。)

#### 段区切り値

- `avoid-column`
  - : 該当するボックスの直後の段区切りを禁止します。
- `column`
  - : 該当するボックスの直後で段区切りを行います。

#### 領域区切り値

- `avoid-region`
  - : 該当するボックスの直後の領域区切りを禁止します。
- `region`
  - : 該当するボックスの直後で領域区切りを行います。

## 改ページの別名

互換性のため、古い {{cssxref("page-break-after")}} はブラウザーから `break-after` の別名として扱われます。これにより、 `page-break-after` を使用しているサイトが引き続き設計通りに動作することを保証します。値のサブセットは次のような別名になります。

| page-break-after | break-after |
| ---------------- | ----------- |
| `auto`           | `auto`      |
| `left`           | `left`      |
| `right`          | `right`     |
| `avoid`          | `avoid`     |
| `always`         | `page`      |

> [!NOTE]
> ブラウザーにおいては `always` の値は `page-break-*` において、段区切りではなくページ区切りとして実装されています。したがって、 Level 4 の仕様書では `always` の値ではなく `page` の別名となっています。

## 公式定義

{{cssinfo}}

## 形式文法

{{csssyntax}}

## 例

### きれいに段に分割

次の例では、すべての段にまたがる `<h1>` (`column-span: all` を使用して実現) と、一連の `<h2>` と段落を `column-width: 200px` を使用して段組みレイアウトしたコンテナーを用意しています。

既定では、小見出しと段落は、見出しの位置が統一されていないため、かなり乱雑にレイアウトされていました。しかし、 `break-after: column` を `<p>` 要素に使うことで、それぞれの要素の後に強制的に改行するようにしたので、各段の先頭に `<h2>` がきちんと配置されます。

#### HTML

```html
<article>
  <h1>大見出し</h1>

  <h2>小見出し</h2>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla vitae
    fringilla mauris. Quisque commodo eget nisi sed pretium. Mauris luctus nec
    lacus in ultricies. Mauris vitae hendrerit arcu, ac scelerisque lacus.
    Aliquam lobortis in lacus sit amet posuere. Fusce iaculis urna id neque
    dapibus, eu lacinia lectus dictum.
  </p>

  <h2>小見出し</h2>

  <p>
    Praesent condimentum dui dui, sit amet rutrum diam tincidunt eu. Cras
    suscipit porta leo sit amet rutrum. Sed vehicula ornare tincidunt. Curabitur
    a ipsum ac diam mattis volutpat ac ut elit. Nullam luctus justo non
    vestibulum gravida. Morbi metus libero, pharetra non porttitor a, molestie
    nec nisi.
  </p>

  <h2>小見出し</h2>

  <p>
    Vivamus eleifend metus vitae neque placerat, eget interdum elit mattis.
    Donec eu vulputate nibh. Ut turpis leo, malesuada quis nisl nec, volutpat
    egestas tellus.
  </p>

  <h2>小見出し</h2>

  <p>
    In finibus viverra enim vel suscipit. Quisque consequat velit eu orci
    malesuada, ut interdum tortor molestie. Proin sed pellentesque augue. Nam
    risus justo, faucibus non porta a, congue vel massa. Cras luctus lacus nisl,
    sed tincidunt velit pharetra ac. Duis suscipit faucibus dui sed ultricies.
  </p>
</article>
```

#### CSS

```css
html {
  font-family: helvetica, arial, sans-serif;
}

h1 {
  font-size: 3rem;
  letter-spacing: 2px;
  column-span: all;
}

h2 {
  font-size: 1.2rem;
  color: red;
  letter-spacing: 1px;
}

p {
  line-height: 1.5;
  break-after: column;
}

article {
  column-width: 200px;
  gap: 20px;
}
```

### 結果

{{EmbedLiveSample('Breaking_into_neat_columns', '100%', 600)}}

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [学習: 段組みレイアウト](/ja/docs/Learn_web_development/Core/CSS_layout/Multiple-column_Layout)
- [Breaking Boxes With CSS Fragmentation](https://www.smashingmagazine.com/2019/02/css-fragmentation/)
