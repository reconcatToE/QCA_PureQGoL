# QCA_PureQGoL Challenge
PureQuantumGoL : A pure quantum game of Life exclusively driven by quantum computation, with no classical elements.

# 2025/05/02
量子セルオートマトンはどう考えても将来の最重要分野になるのがわかりきっているし、それが完全に見えているのに
自分の数学力が全く足りてないのがきつい
本職が気付いて参入してくれば2度と追いつけないところまですぐに行ってしまう
とにかく低く屈んで基礎をやり始めたがいつまでかかるやら、、、


# 2025/4/27
・次世代セルのOFF/ONをXゲート方式で計算するのは、複数ルールへヒットした際の挙動からして論理的に不可能。  
・2次元ライフゲームが2次元格子上に存在すること、とりわけ、  
  モデルに触る前の段階でルールにヒットするパターンの総数を事前に決定できることを利用すると、  
  前よりはライフゲームとして破綻していないモデルを作れたけれども、  
  古典計算が入ってしまうのでpureではなくなる、、、  
      (しかも、以前の研究からも判明した通り、ONセルの確率振幅が急速に減少していく。    
       例えばムーア近傍で3セルがONの総パターン数は56。  
       現世代の|1>が1パターンある場合、次世代では確率振幅が1/56になってしまう。    
       goldilocks/edge of chaosからは程遠い動きとなる。)   
・難しいっていうか正直言って無理かも？とは思っているんだけど、  
  今はこれが勉強する動機となっているので、好奇心がある限りは継続する。  
  とりあえずここまででこれからのことは次考える。コード作るのも億劫なので今回は数式だけ、、、  
・次は「量子ビットを使って論理的な空間を格子で作ったうえで、   
  量子ウォークの確率振幅を流しながらGoLっぽい相互作用計算を乗せる」  
  というのを試してみてもいいかもしれない。    
  本当は素の量子ビットを1セルで扱いたいという理由があったんだけど、、、  

[ imperfect model: classical computation  Included ] 2025.04.27 
### 1. セルの状態 / Cell State
- 各セルは **ON**（`|1⟩`）または **OFF**（`|0⟩`）の内部状態をとる。  
  Each cell is either **ON** (`|1⟩`) or **OFF** (`|0⟩`).
  
- セル `(i,j)` の周囲（ムーア近傍）に **ON** 状態のセルが `k` 個の場合、対応する射影演算子 `P_k^{(i,j)}`を下記に定義：  
  If there are `k` **ON** cells in the Moore neighborhood, the projection operator `P_k^{(i,j)}` is defined as:

$$
P_k^{(i,j)} = |k\rangle \langle k|
$$

### 2. ユニタリ演算子 / Unitary Operator
セル `(i,j)` の内部状態状態に従って、回転ゲート \( R_x \) を適用：  
The unitary operator \( U_{i,j} \) applies a rotation gate \( R_x \) corresponding to the internal state of cell `(i,j)` based on pattern `k`.
- 回転角 `θ`（量子ゲート回転用の回転角）は、ルールに基づく**可能な全パターン数** `M_k`: で割る。  
The rotation angle `θ` (used for quantum gate rotation) is divided by the total number of **possible patterns** `M_k`: based on the rule.

$$
U_{i,j} = \prod_k \left( P_k^{(i,j)} \otimes R\left(\frac{\pi}{M_k}\right) \right)
$$
  
### 3. 全体の進化 / Global Evolution Operator

全体の進化演算子：  
The global evolution operator applies the unitary operators across all cells:

$$
U(t \to t+1) = \bigotimes_{(i,j)} \prod_k \left( P_k^{(i,j)} \otimes R\left(\frac{\pi}{M_k}\right) \right)
$$


# 2025/4/12
約半年かけて何度かチャレンジしているがどれもうまくいってない。
ミニマル3量子ビットで検証しているものの、今のところは論理的に詰んでしまっているように見える。
そもそもJ.H.Conwayオリジナルの古典GoLと同一ルールにこだわる必要はなく、
QCA上でgoldilocks/edge of chaos的な新ルールを探索する方がよいのかもしれない。
