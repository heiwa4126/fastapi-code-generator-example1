# fastapi-code-generator-example1

[koxudaxi/fastapi-code-generator](https://github.com/koxudaxi/fastapi-code-generator)
を使ってみる練習。(2023-07)

## やったこと

ChatAPI に
「簡単な headless blog を FastAPI で作ろうと思います。必要と思われる API を OpenAPI2 の YAML 形式で書き出してもらえますか?」
と頼んで出来たのが、[openapi2.0.yaml](openapi2.0.yaml)。

これを fastapi-codegen にかけると

> AttributeError: 'NoneType' object has no attribute 'is_array'

と言われてエラーになるので、
[SwaggerEditor](https://editor-next.swagger.io/) の
`edit -> Convert to OpenAPI 3.0.x`
で
OpenAPI2 から 3 に
変換して、[openapi.yaml](openapi.yaml) を作った。

で、これに対して:

```bash
fastapi-codegen --input openapi.yaml --output mock --model-file interface.py
```

とやると mock/ 以下にコードができるので、これを別のディレクトリにコピーして
(`fastapi-code-generator`と`fastapi[all]`が pydantic のバージョンがかちあって
同時に pip できない)、編集していく。

## 要点

- fastapi-code-generator は OpenAPI3 でないとダメみたい (2023-07 現在)
  - 最初から ChatAPI に「OpenAPI3 で作って」といえば良かったんだな。
  - ただ OpenAPI3、2 よりわかりにくいよね?
- なんだか `fastapi-code-generator` と `fastapi[all]` が同時に pip できない。pydantic のバージョンがかちあう。 (2023-07 現在)
- 将来 API が変更されたときにはどうするかを考えとかないと...

## 他メモ

mock/ の下は .gitignore にするべきですか? (考え中)
