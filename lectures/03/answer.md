# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：
- `--trace` で見えたツール呼び出し（ツール名と引数）：
- 1つの質問での LLM 呼び出し回数（`requests`）：
- 追加したツールと、docstring に書いた説明：

## 宿題

- 取り組んだレベル：基礎 
- やったこと：
agent.pyのINSTRUCTIONSを以下のように変更
用語や講座に固有のことを答える前に、必ず search_glossary で用語集を確認する。
→必要だと判断した場合のみ search_glossary で用語集を確認する。
docstringを以下のように変更
 指定した回の講義内容から確認問題を1問作成する。
「第2回の確認問題を出して」のように、
指定した回の理解度を確認する問題を出題するときに使う。
lecture には講義の回数を整数で指定する（例: 2）。
→クイズ


- 結果：
元の回答
--- trace ---
[tool call]   make_quiz({'lecture': 2})
[tool return] make_quiz -> {"question": "「LoRA」の意味は？", "answer": "事前学習済みの重みは固定したまま、重みの更新分を2つの小さな行列の積（低ランク行列）で表し、その小さな行列だけを学習するPEFT手法。学習するパラメータが少なく、…
[usage] RunUsage(cost=Decimal('0.0004561'), details={'text_prompt_tokens': 912}, input_text_tokens=912, input_tokens=912, output_tokens=73, requests=2, tool_calls=1)
INSTRUCTIONS変更回答
--- trace ---
[tool call]   make_quiz({'lecture': 2})
[tool return] make_quiz -> {"question": "「過学習」の意味は？", "answer": "学習データにだけ過度に適合し、未知の入力に対する性能が落ちる状態。学習に使わない検証データで性能を測って気づく。"}…
[usage] RunUsage(cost=Decimal('0.0003687'), details={'text_prompt_tokens': 854}, input_text_tokens=854, input_tokens=854, output_tokens=45, requests=2, tool_calls=1)

--- trace ---
[tool call]   make_quiz({'lecture': 2})
[tool return] make_quiz -> {"question": "「事前学習」の意味は？", "answer": "大量の汎用テキストで、次のトークンを予測するようにモデルを学習させる最初の段階。言語の知識や一般的な常識の多くはここで身につく。"}…
[usage] RunUsage(cost=Decimal('0.0005041'), details={'text_prompt_tokens': 797}, input_text_tokens=797, input_tokens=797, output_tokens=106, requests=2, tool_calls=1)
- 気づき・疑問：
それぞれ変更し実行したが、解答や回数にへんかはなかった。