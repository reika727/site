# linalg
* linalg[meta header]
* cpp26[meta cpp]

`<linalg>`ヘッダでは、線形代数(linear algebra)に関する基礎的な演算アルゴリズムを提供する。
本ヘッダが提供するエンティティは、すべて名前空間`std::linalg`に属する。

1次元データであるベクトル(vector)や2次元データである行列(matrix)に対して、線形代数分野のデファクトスタンダードとされる BLAS(Basic Linear Algebra Subprograms) 互換のアルゴリズム群、いくつかの LAPACK(Linear Algebra PACKage) 互換のアルゴリズムが提供される。
BLAS互換アルゴリズムは、演算対象データの次元数や計算オーダーに応じて3段階に区分される。

- Level 1 BLAS : ベクトルーベクトルの演算
- Level 2 BLAS : 行列ーベクトルの演算
- Level 3 BLAS : 行列ー行列の演算

例えば、2個の一般行列の積を求める`std::linalg::matrix_product`はLevel 3 BLASルーチン`xGEMM`に対応する。
（実際のBLASルーチン名は、浮動小数点数型の単精度`S`／倍精度`D`とそれぞれの複素数版`C`,`Z`として、プレフィックス`x`部は文字4種類のいずれか。）

また、多次元配列ビュー[`std::mdpan`](mdspan/mdspan.md)と組み合わせて利用する拡張機能が提供される。


## 共通要件
`<linalg>`ヘッダが提供する演算アルゴリズムは、スカラ値およびベクトル／行列の要素型として線形代数値型(linear algebra value types)を取り扱う。

線形代数値型はBLASが取り扱う`float`, `double`, `std::complex<float>`, `std::complex<double>`をはじめ、[`semiregular`](concepts/semiregular.md)のモデルであれば良い。
また、線形代数値型の値初期化は加法元（算術型であれば値`0`）であること。

プログラム定義型を利用する場合、演算アルゴリズムはカスタマイゼーションポイントとして`abs`, `real`, `imag`, `conj`を非修飾名で呼び出す。


## `std::mdspan`向け機能拡張

| 名前 | 説明 | 対応バージョン |
|------|------|----------------|
| [`layout_blas_packed`](linalg/layout_blas_packed.md) | 行列要素のBLAS互換パックレイアウトに対応する[レイアウトマッピングポリシー](mdspan/LayoutMappingPolicy.md) (class template) | C++26 |
| [`scaled_accessor`](linalg/scaled_accessor.md.nolink) | `scaled`関数用の[アクセサポリシー](mdspan/AccessorPolicy.md) (class template) | C++26 |
| [`scaled`](linalg/scaled.md.nolink) | 要素値をスカラ倍した読み取り専用`std::mdspan`を作る (function template) | C++26 |
| [`conjugated_accessor`](linalg/conjugated_accessor.md.nolink) | `conjugated`関数用の[アクセサポリシー](mdspan/AccessorPolicy.md) (class template) | C++26 |
| [`conjugated`](linalg/conjugated.md.nolink) | 読み取り専用の複素共役ビュー`std::mdspan`を作る (function template) | C++26 |
| [`layout_transpose`](linalg/layout_transpose.md) | `transposed`関数用の[レイアウトマッピングポリシー](mdspan/LayoutMappingPolicy.md) (class template) | C++26 |
| [`transposed`](linalg/transposed.md) | 2次元`std::mdspan`の行列転置ビューを作る (function template) | C++26 |
| [`conjugate_transposed`](linalg/conjugate_transposed.md.nolink) | 読み取り専用の複素共役転置ビュー`std::mdspan`を作る (function template) | C++26 |


## BLAS 1アルゴリズム

| 名前 | 説明 | 対応バージョン |
|------|------|----------------|
| `setup_givens_rotation_result` | `setup_givens_rotation`の結果型 (class template) | C++26 |
| `setup_givens_rotation` | xLARTG: ギブンス回転をセットアップする (function template) | C++26 |
| `apply_givens_rotation` | xROT: ベクトルにギブンス回転を適用する (function template) | C++26 |
| `swap_elements` | xSWAP: 2つのベクトル／行列の要素を交換する (function template) | C++26 |
| `scale` | xSCAL: ベクトル／行列の要素にスカラ値を乗算する (function template) | C++26 |
| `copy` | xCOPY: ベクトル／行列の要素をコピーする (function template) | C++26 |
| `add` | xAXPY: 2つのベクトル／行列の要素を加算する (function template) | C++26 |
| `dot` | xDOT, xDOTU: 2つのベクトルのドット積を求める (function template) | C++26 |
| `dotc` | xDOTC: 2つのベクトルの複素共役ドット積を求める (function template) | C++26 |
| `sum_of_squares_result` | `vector_sum_of_squares`の結果型 (class template) | C++26 |
| `vector_sum_of_squares` | xLASSQ: ベクトル要素の平方和を求める (function template) | C++26 |
| `vector_two_norm` | xNRM2: ベクトルのユークリッドノルム(Euclidean norm)を求める (function template) | C++26 |
| `vector_abs_sum` | xASUM: ベクトル要素の絶対値和を求める (function template) | C++26 |
| `vector_idx_abs_max` | xIAMAX: ベクトル要素のうち最大絶対値インデクスを返す (function template) | C++26 |
| `matrix_frob_norm` | 行列のフロベニウスノルム(Frobenius norm)を求める (function template) | C++26 |
| `matrix_one_norm` | 行列の1ノルム(One norm)を求める (function template) | C++26 |
| `matrix_inf_norm` | 行列の無限大ノルム(Infinity norm)を求める (function template) | C++26 |


## BLAS 2アルゴリズム

| 名前 | 説明 | 対応バージョン |
|------|------|----------------|
| `matrix_vector_product` | xGEMV: 一般行列とベクトルの積を求める (function template) | C++26 |
| `symmetric_matrix_vector_product` | xSYMV: 対称行列とベクトルの積を求める (function template) | C++26 |
| `hermitian_matrix_vector_product` | xHEMV: ハミルトニアン行列とベクトルの積を求める (function template) | C++26 |
| `triangular_matrix_vector_product` | xTRMV: 三角行列とベクトルの積を求める (function template) | C++26 |
| `triangular_matrix_vector_solve` | xTRSV: 三角行列を係数とする行列方程式を解く (function template) | C++26 |
| `matrix_rank_1_update` | xGER, xGERU: 行列のRank-1更新 (function template) | C++26 |
| `matrix_rank_1_update_c` | xGERC: 複素行列のRank-1更新 (function template) | C++26 |
| `symmetric_matrix_rank_1_update` | xSYR: 対称行列のRank-1更新 (function template) | C++26 |
| `hermitian_matrix_rank_1_update` | xHER: ハミルトニアン行列のRank-1更新 (function template) | C++26 |
| `symmetric_matrix_rank_2_update` | xSYR2: 対称行列のRank-2更新 (function template) | C++26 |
| `hermitian_matrix_rank_2_update` | xHER2: ハミルトニアン行列のRank-2更新 (function template) | C++26 |


## BLAS 3アルゴリズム

| 名前 | 説明 | 対応バージョン |
|------|------|----------------|
| `matrix_product` | xGEMM: 2つの一般行列の積を求める (function template) | C++26 |
| `symmetric_matrix_product` | xSYMM: 対称行列と行列の積を求める (function template) | C++26 |
| `hermitian_matrix_product` | xHEMM: ハミルトニアン行列と行列の積を求める (function template) | C++26 |
| `triangular_matrix_product` | xTRMM: 三角行列と行列の積を求める (function template) | C++26 |
| `triangular_matrix_left_product` | xTRMM: In-placeに三角行列と行列の積を求める (function template) | C++26 |
| `triangular_matrix_right_product` | xTRMM: In-placeに三角行列と行列の積を求める (function template) | C++26 |
| `symmetric_matrix_rank_k_update` | xSYRK: 対称行列のRank-k更新 (function template) | C++26 |
| `hermitian_matrix_rank_k_update` | xHERK: ハミルトニアン行列のRank-k更新 (function template) | C++26 |
| `symmetric_matrix_rank_2k_update` | xSYR2K: 対称行列のRank-2k更新 (function template) | C++26 |
| `hermitian_matrix_rank_2k_update` | xHER2K: ハミルトニアン行列のRank-2k更新 (function template) | C++26 |
| `triangular_matrix_matrix_left_solve` | xTRSM: 三角行列の連立一次方程式を解く (function template) | C++26 |
| `triangular_matrix_matrix_right_solve` | xTRSM: 三角行列の連立一次方程式を解く (function template) | C++26 |


## タグ型

| 名前 | 説明 | 対応バージョン |
|------|------|----------------|
| [`column_major_t`](linalg/column_major_t.md) | 列優先(column-major)順序を表現するためのタグ型 (class) | C++26 |
| [`column_major`](linalg/column_major_t.md)   | 列優先(column-major)順序を表現するためのタグ値 (variable) | C++26 |
| [`row_major_t`](linalg/row_major_t.md) | 行優先(row-major)順序を表現するためのタグ型 (class) | C++26 |
| [`row_major`](linalg/row_major_t.md)   | 行優先(row-major)順序を表現するためのタグ値 (variable) | C++26 |
| [`upper_triangle_t`](linalg/upper_triangle_t.md.nolink) | 上三角行列を表現するためのタグ型 (class) | C++26 |
| [`upper_triangle`](linalg/upper_triangle_t.md.nolink)   | 上三角行列を表現するためのタグ値 (variable) | C++26 |
| [`lower_triangle_t`](linalg/lower_triangle_t.md.nolink) | 下三角行列を表現するためのタグ型 (class) | C++26 |
| [`lower_triangle`](linalg/lower_triangle_t.md.nolink)   | 下三角行列を表現するためのタグ値 (variable) | C++26 |
| `implicit_unit_diagonal_t` | implicit unit diagonalを表現するためのタグ型 (class) | C++26 |
| `implicit_unit_diagonal`   | implicit unit diagonalを表現するためのタグ値 (variable) | C++26 |
| `explicit_diagonal_t` | explicit diagonalを表現するためのタグ型 (class) | C++26 |
| `explicit_diagonal`   | explicit diagonalを表現するためのタグ値 (variable) | C++26 |


## バージョン
### 言語
- C++26


## 関連項目
- [`<mdspan>`](mdspan.md)


## 参照
- [P1673R13 A free function linear algebra interface based on the BLAS](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2023/p1673r13.html)
- [P1674R2: Evolving a Standard C++ Linear Algebra Library from the BLAS](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2022/p1674r2.html)
- [std::linalg: Linear Algebra Coming to Standard C++](https://github.com/CppCon/CppCon2023/blob/main/Presentations/stdlinalg_linear_algebra_coming_to_standard_cpp.pdf), CppCon 2023
- [BLAS (Basic Linear Algebra Subprograms)](https://www.netlib.org/blas/)
