# 高度なプロンプトの作成

[![高度なプロンプトの作成](../../images/05-lesson-banner.png?WT.mc_id=academic-105485-yoterada)](https://youtu.be/32GBH6BTWZQ?WT.mc_id=academic-105485-yoterada)

前の章で学んだことをいくつかおさらいしましょう。

> プロンプト _エンジニアリング_ は、より有用な指示やコンテキストを提供することで、**より適切な回答の提供に向けてモデルを導く**プロセスです。

また、プロンプトを書くには、関連するコンテキストを提供することで、プロンプトを作成する際 2つのステップがあり、2番目の部分は _最適化_、つまりプロンプトを徐々に改善する手法です。

ここまでで、プロンプトの書き方についての基本的な理解はできましたが、さらに深く掘り下げる必要があります。この章では、さまざまなプロンプトを試し、あるプロンプトが別のプロンプトよりも優れている理由を理解します。任意の LLM に適用できる、いくつかの基本的な手法に従いプロンプトを作成する方法を学習します。

## はじめに

この章では、次のトピックについて説明します。

- プロンプトにさまざまな手法を適用することで、プロンプト・エンジニアリングの知識を深めます
- 出力を変化させるようプロンプトを構成します

- プロンプトには、さまざまな手法を適用することで、プロンプト・エンジニアリングの知識の幅を広げます
- 出力を変化させるようなプロンプトを作成します。

## 学習目標

このレッスンを完了すると、次のことができるようになります。

- プロンプトの結果を改善するプロンプト・エンジニアリング手法を利用できる。
- 多様な、あるいは決定的なプロンプトを実行できる。

## プロンプト・エンジニアリング

プロンプト・エンジニアリングは、期待する結果を生み出すためのプロンプトを作成するプロセスです。プロンプト・エンジニアリングには、単にテキスト・プロンプトを書くだけではありません。プロンプト・エンジニアリングはエンジニアリング分野ではなく、期待する結果を得るために適用できる一連のテクニックです。

### プロンプトの例

次の基本的なプロンプトを見てみましょう。

> 地理に関する質問を10問作成してください

このプロンプトの中では、実際には一連のさまざまなプロンプトのテクニックを適用しています。

詳しく見ていきましょう。

- **コンテキスト :** 「地理」に関する質問であることを指定しています。
- **出力を制限 :** 作成される質問の数は 10 個以下になります

### 単純なプロンプトの制限

期待する結果が得られる場合と得られない場合があります。地理は幅広いテーマであり、以下の理由により期待する結果が得られない場合があります。

- **大きな話題 :** 国、首都、川などのような話題は大きく、どのような結果が返されるか予想できません。
- **フォーマット :** 質問を特定の方法で書式設定したい場合はどうすればよいでしょうか。

ご覧のとおり、プロンプトを作成する際には考慮すべきことがたくさんあります。

ここまでは、簡単なプロンプトの例を見てきましたが、生成 AI は、さまざまな役割や業界の人々を支援するために、より多くのことができます。次に、いくつかの基本的なテクニックを確認してみましょう。

### プロンプトのテクニック

まずプロンプトは、大規模言語モデル (LLM) の登場で、_新たに出てきた技術_ で、これはモデルに組み込まれている機能ではなく、モデルを使用する際に使用するものだと理解する必要があります。

LLM のプロンプトで利用できる、いくつかの基本的なテクニックがあります。それらを確認してみましょう。

- **Few shot prompting** プロンプトの最も基本的な形式で、いくつかの例を含む一つのプロンプトです。
- **Chain-of-thought** このプロンプトは、問題を段階に分解し LLM に問い合わせします。
- **Generated knowledge** プロンプトの応答を改善するため、事実や知識をプロンプトに追加で提供します。
- **Least to most** Chain-of-thought(思考の連鎖)と同様に、この手法は問題を一連のステップに分解し、それらのステップを順番に実行するように指示します。
- **Self-refine** この手法は、LLM の出力に対する評価と、それに対する改善要求を行います。
- **Maieutic prompting** これは、LLM の回答が正しいことを確認し、回答の各部分を説明するように求めます。これは自己改善の一種です。

### Few-shot prompting

このプロンプトはとても簡単で、一つのプロンプトといくつかの例から構成します。
この手法は、LLM について学び始めたときに最初に使用する手法です。次に例を示します。

- プロンプト: 「代数とは何ですか？」  
- 回答: 「代数は、数学の一分野で、数学記号とそれらの記号を操作するためのルールを研究します。」

### Chain-of-thought

Chain-of-thought (思考の連鎖)は非常に興味深く、LLM を一連の段階に分けて回答を導く手法です。LLM が、何をどうやって行うかを理解するように指導する手法です。次の例を考えてみてください。Chain-of-thought を用いた場合と用いない場合の両方の例をご覧ください。

    - プロンプト: 「アリスはリンゴを 5 個持っていて、3 個を捨て、2 個をボブに渡し、ボブは 1 個を返します。アリスはリンゴを何個持っていますか？」  
    - 回答: 5  

LLMは5と答えますが、これは間違いです。正しい答えはリンゴ 1 個で、計算式は(5 -3 -2 + 1 = 1)です。  

では、どうやって LLM がこれを正しく行うように教えることができるでしょうか？  

Chain-of-thought を試してみましょう。Chain-of-thought を適用するためには：  

1. LLM に類似の例を示す。  
2. 計算式と、それを正しく計算する方法を示す。  
3. 元のプロンプトを提供する。  

という手順を踏みです。以下にその方法を示します。  

    - プロンプト: 「リサはリンゴを7個持っていて、1個を捨て、4個をバートに渡し、バートは1個を返します。計算は次の通り：  
      7 - 1 = 6
      6 - 4 = 2
      2 + 1 = 3
    アリスはリンゴを 5 個持っていて、3 個を捨て、2 個をボブに渡し、ボブは 1 個を返します。アリスはリンゴを何個持っていますか？」
    - 回答: 1

別の例と、計算式を用いて、少し長いプロンプトを作成し、元のプロンプトを提供することで、正しい答え 1 に到達する方法に注目してください。  

ご覧の通り、Chain-of-thought (思考の連鎖) は非常に強力な手法です。

### Generated knowledge

プロンプトを作成する際、多くの場合、自社のデータを活用します。プロンプトの一部は会社からの情報で、残りの部分は具体的な問い合わせ内容にします。

例えば、保険業界であれば、プロンプトは以下のようになるでしょう。

```text
{{company}}: {{company_name}}  
{{products}}:   
{{products_list}}  
以下の予算と要件を考慮した上で、保険を提案してください:  
予算: {{budget}}  
要件: {{requirements}}  
```

上記は、テンプレートを使用してプロンプトをどのように作成するかを示しています。テンプレートには、`{{variable}}`という形式で表現する変数はいくつかあり、これらは会社の API から取得した実際の値に置き換えます。  

以下は、変数を自社の情報に置き換えた後のプロンプトの例です。  

```text
保険会社: ACME保険  
保険商品（月額料金）:   
- 自動車保険, 安価, 500ドル  
- 自動車保険, 高価, 1100ドル   
- 家財保険, 安価, 600ドル  
- 家財保険, 高価, 1200ドル  
- 生命保険, 安価, 100ドル  
   
以下の予算と要件を考慮した上で、保険を提案してください:  
予算: $1000  
要件: 自動車保険, 家財保険  
```

このプロンプトをLLM（Language Model）で実行すると、以下のような回答が得られます。

```output
生命保険も含めて  
   
予算と要件を考慮した上で、ACME保険から以下の保険パッケージを提案します:   
- 自動車保険, 安価, 500ドル   
- 家財保険, 安価, 600ドル   
- 生命保険, 安価, 100ドル   
合計費用: $1,200ドル  
```

この結果では、生命保険も提案されていますが、これは本来求めていない結果です。これは、プロンプトが何を許可するかをより明確にするために、プロンプトを最適化する必要があることを示しています。試行錯誤を繰り返した結果、以下のようなプロンプトにたどり着きました。

```text
保険会社: ACME保険  
保険商品（月額料金）:   
- 種類: 自動車保険, 安価, 費用: 500ドル  
- 種類: 自動車保険, 高価, 費用: 1100ドル   
- 種類: 家財保険, 安価, 費用: 600ドル  
- 種類: 家財保険, 高価, 費用: 1200ドル  
- 種類: 生命保険, 安価, 費用: 100ドル  
   
以下の予算と要件を考慮した上で、保険を提案してください:  
予算: $1000 選択を以下の種類に限定: 自動車保険, 家財保険  
```  

「種類」と「費用」を追加し、「限定」というキーワードを使用することで、LLM が何を求めているかを理解するのに役立ちます。

これにより、以下のような応答が得られます。

```output
予算と要件を考慮した上で、月額500ドルの自動車保険（安価）を提案します。  
```

この例から、Generated knowledge という手法を使用しても、多くの場合、望む結果を得るためにはプロンプトの最適化が必要であることがわかります。

### Least-to-most

「Least-to-most (最小から最大) プロンプト」のアイデアは、大きな問題を小さな問題に分割することです。これにより、LLM（Language Model）が大きな問題をどのように「解決」するかをガイドするのに役立ちます。良い例としては、データサイエンスがあります。LLM に以下のように問題を分割するように依頼することができます。  

> プロンプト: 5つのステップで、データサイエンスを実行する方法は何ですか？  

AI アシスタントは以下のように回答します。  

1. データを収集する  
2. データをクリーニングする  
3. データを分析する  
4. データをプロットする  
5. データを提示する

### Self-refine, critique the results

生成 AI や LLM を使用する際、その出力をそのまま信じてはいけません。必ず確認が必要です。なぜなら、LLM は何が正しいかではなく、次に出てくる可能性が最も高いものを提示しているだけだからです。そのため、LLM に自己評価を求め、それによって自己改善するという手法が有効です。

この手法は以下の手順で行います：  

1. 最初に LLM に問題解決を求める  
2. LLM が回答する  
3. その回答を評価し、AI に改善を求める  
4. LLM が再度回答し、今度は評価を考慮して自身が考えた解決策を提案する  

このプロセスは何度でも繰り返すことができます。

以下にこの手法を使用した例を示します：

> プロンプト: "製品と顧客を持つ　Python Web API　を作成してください"

AIの回答:

```python
import flask
app = Flask(__name__)
    
@app.route('/products')
def products():
    return 'Products'

@app.route('/customers')
def customers():
    return 'Customers'
```

> プロンプト: "上記のコードの改善点を3つ提案してください"

AIの回答:

```text
もちろんです、コードを改善するための3つの提案をします：

正しいモジュールをインポートする：最初の行は flask ではなく Flask をインポートするべきです。正しいインポート文は from flask import Flask となります。

メイン関数を追加する：ファイルを実行した際、アプリケーションを実行できるように、if __name__ == '__main__': ブロックをファイルの最後に追加します。

f-strings を使用する：ルート関数の return 文をフォーマットするために f-strings を使用します。例えば、'Products' を返す代わりに、f'This is the {request.path} page' を返すように変更できます。
```


```python
from flask import Flask, request
    
app = Flask(__name__)
    
@app.route('/products')
def products():
    return f'This is the {request.path} page'

@app.route('/customers')
def customers():
    return f'This is the {request.path} page'

if __name__ == '__main__':
    app.run()
```

上記の AI の回答を見ると、最初の回答を再評価することで、最初に提案されたコードが改善されていることがわかります。

### Maieutic prompting

Maieutic プロンプトは、self-refine (自己改善) と似た手法ですが、こちらは LLM に自身で説明を求めるものです。目指すのは、LLM の出力における不整合を減らし、正確な答えを得ることです。そのための手順は以下のようになります。  

1. LLM に質問に答えるよう求める
2. 答えの各部分について、LLM に詳しく説明させる
3. 不整合がある場合、その部分は排除する  

これら全ての内容を検討し、回答に満足するまで 2 と 3 の手順を繰り返します。

以下に、例を示します。

> プロンプト: パンデミックを緩和するための危機対策を5つの段階でどのように作成すればよいか教えてください。

LLMの回答:

```text
1. リスクを特定する
2. 利害関係者を特定する
3. リソースを特定する
4. 行動を特定する
5. コミュニケーションチャネルを特定する
```

5 つが特定されましたが、これが正しいかどうかを確認するために、LLM に各内容を詳しく説明させてみましょう。

> プロンプト: 最初のステップを詳しく説明してください。具体的には、パンデミックにおけるリスクは何ですか？
 
    ```text  
    リスクは以下の通りです：  
      
    - 生命の喪失
    - ビジネスの喪失
    - 評判の喪失
    - 顧客の喪失
    - 従業員の喪失
    ```  

ここで、LLM が正しいかどうかを確認するため、最初のリスクについて詳しく説明させ、それが上記の答えと一致することを確認します。

> プロンプト: パンデミックにおいて、最も大きなリスクは何でしょうか？また、その理由は何ですか？

```text  
最も大きなリスクは生命の喪失で、それは最も重要な守るべきものです。  
```

> パンデミックにおけるリスクの中で、最も大きな2つのリスクは何だと思いますか？

```text
最も大きな2つのリスクは、生命の喪失とビジネスの喪失です。
```

ここで、LLM　は一貫性を保ち、「生命」と「ビジネス」を最大の2つのリスクとして挙げています。これにより、次のステップに進むことができ、かなりの自信を持つことができます。ただし、LLM　を盲目的に信頼するのではなく、常にその出力を検証することが重要です。

## Vary your output

LLM は本質的に非確実な性質を持っているため、同じプロンプトを実行しても結果は毎回異なります。例えば、以下のプロンプトを試してみてください。

> "Python Web API のコードを生成してください"

```text  
# 必要なモジュールをインポートする  
import flask
from flask import request, jsonify

# Flaskアプリを作成する
app = flask.Flask(__name__)

# APIのルートを作成する
@app.route('/api', methods=['GET'])
def api():
    # リクエストからデータを取得する
    data = request.args

    # データを処理する
    result = process_data(data)

    # 結果をJSONとして返す
    return jsonify(result)

# データを処理する関数
def process_data(data):
    # データを何かしら処理する
    result = data + 1

    # 結果を返す
    return result

# アプリを実行する
if __name__ == '__main__':
    app.run()
```

同じプロンプトを再度実行すると、少し異なる結果が出力されます。

```text
# 必要なパッケージをインポートする
import flask
from flask import request, jsonify

# Flaskアプリケーションを作成する
app = flask.Flask(__name__)
app.config["DEBUG"] = True

# 本のリストを作成する
books = [
    {'id': 0,
     'title': 'A Fire Upon the Deep',
     'author': 'Vernor Vinge',
     'first_sentence': 'The coldsleep itself was dreamless.',
     'year_published': '1992'},
    {'id': 1,
     'title': 'The Ones Who Walk Away From Omelas',
     'author': 'Ursula K. Le Guin',
     'first_sentence': 'With a clamor of bells that set the swallows soaring, the Festival of Summer came to the city Omelas, bright-towered by the sea.',
     'published': '1973'},
    {'id': 2,
     'title': 'Dhalgren',
     'author': 'Samuel R. Delany',
     'first_sentence': 'to wound the autumnal city.',
     'published': '1975'}
]

# APIのエンドポイントを作成する
@app.route('/', methods=['GET'])
def home():
    return '''<h1>Books API</h1>
<p>A prototype API for retrieving books.</p>'''

# すべての本を返すエンドポイントを作成する
@app.route('/api/v1/resources/books/all', methods=['GET'])
def api_all():
    return jsonify(books)

# 単一の本を返すエンドポイントを作成する
@app.route('/api/v1/resources/books', methods=['GET'])
def api_id():
    # IDがURLの一部として提供されたか確認する
    # IDが提供された場合は、それを変数に割り当てる
    # IDが提供されていない場合は、エラーを表示する
    if 'id' in request.args:
        id = int(request.args['id'])
    else:
        return "Error: No id field provided. Please specify an id."

    # 結果のための空のリストを作成する
    results = []

    # データをループして、リクエストされたIDに一致する結果を探す
    # IDは一意ですが、他のフィールドは多数の結果を返す可能性があります
    for book in books:
        if book['id'] == id:
            results.append(book)

    # Flaskのjsonify関数を使用して、Pythonの辞書のリストをJSON形式に変換する
    return jsonify(results)

app.run()
```

> では、このような出力のバリエーションは問題なのでしょうか？

それは、皆様が何を実現したいかによります。特定の確実な応答を求めている場合、それは問題となります。しかし、「地理に関する任意の 3 つの質問を生成する」のように、出力のバリエーションに対して柔軟であれば問題ではありません。

### 温度を使用して出力を変化させる

出力をより予測可能、つまりより決定論的(確実)に制限したいと考えた場合、どのようにすればよいでしょうか？

Temperature (温度) パラメータは 0 から 1 までの値を持っており、0が最も確定的で、1 が最も多様性があることを示します。デフォルト値は0.7です。温度を0.1に設定し、同じプロンプトを 2 回実行してみると以下のような結果が得られます。

> "Python Web API のコード を作成してください"

    ```python
    #import necessary libraries
    import flask
    from flask import request, jsonify
    
    #create an instance of the Flask class
    app = flask.Flask(__name__)
    
    #create an endpoint for the API
    @app.route('/api/v1/endpoint', methods=['GET'])
    def api_endpoint():
        #get the request data
        data = request.get_json()
    
        #process the data
        result = process_data(data)
    
        #return the result
        return jsonify(result)
    
    #function to process the data
    def process_data(data):
        #process the data
        result = {'result': 'success'}
    
        #return the result
        return result
    
    #run the Flask app
    if __name__ == '__main__':
        app.run()
    
    ```

プロンプトを再度実行すると、次の結果が得られます。  

    ```python
    #import necessary libraries
    import flask
    from flask import request, jsonify
    
    #create a Flask app
    app = flask.Flask(__name__)
    
    #create a route for the API
    @app.route('/api', methods=['GET'])
    def api_call():
        #get the data from the request
        data = request.get_json()
        
        #process the data
        result = process_data(data)
        
        #return the result
        return jsonify(result)
    
    #define the process_data function
    def process_data(data):
        #do something with the data
        result = data + 1
        
        #return the result
        return result
    
    #run the app
    if __name__ == '__main__':
        app.run()
    
    ```

これら 2 つの出力結果はわずかな違いしかありません。今度は逆に、温度を0.9に設定してみましょう。

    ```python
    # Import necessary libraries
    import flask
    from flask import request, jsonify
    
    # Create a Flask app
    app = flask.Flask(__name__)
    
    # Create a route for the API
    @app.route('/api', methods=['GET'])
    def api_call():
        # Get the data from the request
        data = request.args
    
        # Process the data
        result = process_data(data)
    
        # Return the result
        return jsonify(result)
    
    # Function to process the data
    def process_data(data):
        # Do something with the data
        result = data + 1
    
        # Return the result
        return result
    
    # Run the app
    if __name__ == '__main__':
        app.run()
    
    ```

温度パラメータの値として 0.9 で 2 回目の実行:

    ```python
    import flask
    from flask import request, jsonify
    
    # create the Flask app
    app = flask.Flask(__name__)
    app.config['DEBUG'] = True
    
    # create some test data
    books = [
        {'id': 0, 'title': 'A Fire Upon The Deep', 'author': 'Vernor Vinge', 'first_sentence': 'The coldsleep itself was dreamless.', 'year_published': '1992'},
        {'id': 1, 'title': 'The Ones Who Walk Away From Omelas', 'author': 'Ursula K. Le Guin', 'first_sentence': 'With a clamor of bells that set the swallows soaring, the Festival of Summer came to the city Omelas, bright-towered by the sea.', 'published': '1973'},
        {'id': 2, 'title': 'Dhalgren', 'author': 'Samuel R. Delany', 'first_sentence': 'to wound the autumnal city.', 'published': '1975'}
    ]
    
    # create an endpoint
    @app.route('/', methods=['GET'])
    def home():
        return '''<h1>Welcome to our book API!</h1>'''
    
    @app.route('/api/v1/resources/books
    
    ```

ご覧いただいたように、結果は非常に多様になることがわかります。

> なお、出力を変化させるために変更できるパラメータは他にもあります。例えば、top-k, top-p, repetition penalty, length penalty, diversity penalty などですが、これらはこのレッスンでは取り扱いません。

## おすすめの方法

皆様が目的の結果を得るためには、様々な方法を試すことができます。プロンプトを利用する頻度が増えるほど、ご自身専用のスタイルを身に付けられるでしょう。

これまでに紹介したテクニックに加えて、LLM を活用する際におすすめの方法がいくつかあります。

以下に、そのおすすめの方法をいくつか紹介します。

- **コンテキストを明確にする** コンテキストは重要で、ドメインやトピックなど、具体的に指定するほど良い結果が得られます。  
- **出力を制限する** 特定の項目数や特定の長さを求める場合は、それを明示的に指定しましょう。
- **「何を」、「どうするか」を明確にする** 例えば、「Python の Web API を作成し、商品と顧客を設定し、それを 3 つのファイルに分けてください」といった、具体的な指示を出すようにしてください
- **テンプレートを活用する** 自社データをプロンプトに反映させたい場合が多いと思います。その際に、テンプレートを活用しましょう。テンプレートには、実際のデータに置き換えられる変数を設定できます。
- **正確に記述する** スペル・ミスがあっても LLM は正しい回答を提供してくれるかもしれませんが、スペルが正確であれば、より良い回答が得られます。

## 課題

Flask を使用して単純な API を構築する方法を示す Python のコードを次に示します。

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/')
def hello():
    name = request.args.get('name', 'World')
    return f'Hello, {name}!'

if __name__ == '__main__':
    app.run()
```

上記のコードを、GitHub Copilot や ChatGPT などの AI アシスタントを使用し、「self-refine (自己調整)」の手法を適用してコードを改善してください。

## 解決

コードに対して適切なプロンプトを追加し、課題の解決を試みてください。

> [!TIP]
> プロンプトに改善を求める際、改善点の数を制限すると効果的です。また、アーキテクチャ、パフォーマンス、セキュリティなど、特定の観点から改善を求めることも可能です。

[Solution](../../solution.py?WT.mc_id=academic-105485-yoterada)

## 知識チェック

なぜ、chain-of-thought (思考の連鎖) プロンプトを使用するのでしょうか?正解を 1 つ選択してください。

1. LLM に問題の解決方法を教える。
1. LLM にコード内のエラーを見つけるように教える
1. LLM にさまざまな解決策を考えるように指示する

答え：1：chain-of-thought (思考の連鎖) プロンプトは、LLM に回答を導き出すための一連の処理段階と、類似問題とその解決方法を提供することで、問題を解決する方法を示すことです。

## 🚀 Challenge

課題では、self-refine (自己改善) の手法を使用しました。皆様が実際に実装したプログラムを取り上げて、それに対してどのように改善したいか考えてみてください。そして、その改善案を self-refine (自己改善手法)の手法を使って実際に適用してみましょう。結果は良くなりましたか？悪くなりましたか？どう思われますか?

## お疲れ様でした!学習を続ける

このレッスン修了後、[生成 AI 学習コレクション](https://aka.ms/genai-collection?WT.mc_id=academic-105485-yoterada) をチェックして、Generative AI の知識をレベルアップさせましょう。

レッスン 6 では、プロンプト エンジニアリングの知識を応用して[テキスト生成アプリケーションの構築](../../../06-text-generation-apps/translations/ja-jp/README.md?WT.mc_id=academic-105485-yoterada)を行います。
