## 整然データの定義

幸福な家族はどれも似ているが、不幸な家族は不幸のあり方がそれぞれ異なっている。――レフ・トルストイ

家族と同じく、整然データセットはどれも似ているが、雑然データセットは雑然のあり方がそれぞれ異なっている。整然データセットは、データセットの構造（物理レイアウト）を意味と結びつける標準化された手法を提供する。この節では、データセットの構造と意味を記述するための標準的な用語をいくつか準備した上で、それらの定義を用いて整然データを定義する。

### データ構造

ほとんどの統計データセットは、*行* (row) と*列* (column)からなる長方形の表である。列はほとんどすべての場合にラベルが付され、行は時々ラベルが付される。表1は、架空の実験に関するデータを、野生の状態で一般的に見られる形式で示したものである。表には、2つの列と3つの行とがあり、行と列の両方にラベルが付されている。

|                     |  treatmenta |  treatmentb |
|:-------------|-----------:|-----------:|
| John Smith              |          ―|           2|
| Jane Doe              |          16|          11|
| Mary Johnson |           3|           1|

表1：典型的な発表用データセット。

同じ潜在的データを構造化する方法は、多くのものがある。表2は、表1と同じデータを示すが、行と列とが転置されている。データは同じであるが、レイアウトが異なっている。行や列といった用語は、2つの表が同じデータを表す理由を記述するのにまったく十分でない。外観に加えて、表に示された値の潜在的意味を記述する方法が必要になる。

|            |  John Smith |  Jane Doe |  Mary Johnson |
|:-----------|-----------:|---------:|-------------:|
| treatmenta |           ―|        16|             3|
| treatmentb |           2|        11|             1|

表2：表1と同じデータだが、構造化の方法が異なっている。

### データの意味

データセットとは*値* (value) を集めたものである。値は、通常、数（量的なものの場合）または文字列（質的なものの場合）のいずれかになる。値は、2つの方法でまとめられる。どの値は、*変数* (variable) と*観測* (observation) に属する。変数には、さまざまなユニットに対して、同じ潜在属性（高さ、温度、継続時間など）を測定するすべての値が含まれる。観測には、さまざまな属性に対して、同じユニット（1人、1日、1レースなど）で測定されたすべての値が含まれる。

表3は、値・変数・観測をより明確にするために、表1を再編成したものである。データセットには、3つの変数と6つの観測を表す18個の値が含まれている。変数は次のとおりである。

1. 「人」：取りうる値を3つ（John Smith、Mary Johnson、Jane Doe）持つ。
2. 「処置」：取りうる値を2つ（a, b）持つ。
3. 「結果」：欠損値をどう捉えるかによって変わるが、取りうる値を5つまたは6つ（―, 16, 3, 2, 11, 1）持つ。

実験計画は、観測の構造について、より詳しいことを教えてくれる。この実験では、「人」と「処置」のすべての組み合わせが測定されており、完全に交差した計画であった。また、実験計画は、欠損値を安全に捨て去ることができるかどうかについても決定する。この実験では、欠損値は、なされるべきだったがなされなかった観測を表しているので、それを保持しておくことは重要である。なすことができない測定（例えば、妊娠したオスの数）を表す構造的欠損値は、安全に捨て去ることができる。

| name         | trt |  result|
|:-------------|:----|-------:|
| John Smith   | a   |       —|
| Jane Doe     | a   |      16|
| Mary Johnson | a   |       3|
| John Smith   | b   |       2|
| Jane Doe     | b   |      11|
| Mary Johnson | b   |       1|

表3：表1と同じデータだが、変数が列に、観測が行になっている。

通常、所与のデータセットに対して何が変数で何が観測かを把握するのは容易である。しかし、変数や観測について、一般的な定義を正確に行うことは驚くほど困難である。例えば、表1の列が「高さ」と「重量」であったとしたら、それらを変数と呼ぶことは納得がいくだろう。列が「高さ」と「幅」であったとしたら、「高さ」と「幅」を「次元」変数の値と考える可能性があるので、あまり明確ではなくなるだろう。列が「自宅の電話」と「職場の電話」であったとしたら、これらを2つの変数として扱うことができるものの、不正検知の環境では、複数の人が1つの電話番号を使用していることが不正を示唆する可能性があるため、「電話番号」と「電話番号の種別」という変数が欲しくなるかもしれない。一般的な経験則としては、行と行の間よりも、変数と変数の間の関数的関係を記述する方が容易である（例：zはxとyの線形結合である、「密度」は「重量」と「体積」の比である）。また、行のグループと行のグループとの間よりは、観測のグループと観測のグループの間の比較の方が容易である（例：グループaの平均とグループbの平均の比較）。

所与の分析に対して、複数のレベルの観測が存在しうる。例えば、新アレルギー薬の試験では、3種類の観測があるだろう。すなわち、人ごとに収集される人口統計上のデータ（「年齢」・「性別」・「人種」）、日ごとにかつ人ごとに収集される医療上のデータ（「くしゃみの数」・「目の赤み」）、日ごとに収集される気象データ（「温度」・「花粉数」）である。

### 整然データ
整然データは、データセットの意味をその構造に写し取る標準的手法である。 データセットが雑然か整然かは、行・列・表が、観測・変数・タイプとどれだけ一致しているかによって決まる。*整然データ* (tidy data) には以下の性質がある。

1. 個々の変数が1つの列をなす。
2. 個々の観察が1つの行をなす。
3. 個々の観察ユニットのタイプが表をなす

これは Codd の第3正規形 (Codd 1990) であるが、統計の言語に合わせた制約がある。そして、リレーショナルデータベースでよく使われる多くの接続されたデータセットではなく、単一のデータセットに重点が置かれている。*雑然データ* (messy data) は、整然データ以外のデータの配列方法を指す。

表3は、表1の整然化されたバージョンである。各行は、1人の「患者」に対する1回の「処置」の「結果」である観察を表し、各列は変数である。

整然データは、データセットを構造化する標準的手法を提供するため、分析者や計算機が必要な変数を抽出することを容易にする。表3を表1と比較してみよう。表1では、異なる変数を抽出するのに、異なる戦略を使用する必要がある。これにより、分析が遅くなり、エラーがもたらされる。ある変数に属するすべての値に関わるデータ分析操作（すべての集計関数）の数を考慮すれば、単純かつ標準的手法でこれらの値を抽出することが重要であることが分かるだろう。 整然データは、R (R Core Team 2014) のようなベクトル化されているプログラミング言語に特に適している。なぜかと言えば、そのレイアウトによって、同じ観測からの異なる変数の値が常にペアになることが保証されているためである。

変数と観測の順序は分析に影響しないが、順序を適切にすれば、生の値を読み取ることが容易になる。変数を編成する方法の1つとして、分析における変数の役割によって考えるというものがある。つまり、データ収集計画によって固定された値であるか、それとも、実験の過程で測定される値であるかと考えるのだ。固定変数は、実験計画を記述し、事前に分かっているものである。計算機科学者はしばしばそれらを固定変数の次元と呼び、統計学者は通常それらを確率変数の添字で示す。被測定変数は、我々が研究で実際に測定するものである。固定変数が最初に来るべきで、被測定変数がそれに続き、関連する変数が連続するように各々の変数を並べる。そして、行は最初の変数によって並べられ、2番目以降の（固定）変数との結びつきはなくなる。これは、本論文で表の形で示したものがすべて従っている方式である。
