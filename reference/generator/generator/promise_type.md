# generator::promise_type
* generator[meta header]
* class template[meta id-type]
* std[meta namespace]
* cpp23[meta cpp]

```cpp
namespace std {
  template<class Ref, class V, class Allocator>
  class generator<Ref, V, Allocator>::promise_type {
    ...
  };
}
```
* generator[link ../generator.md]


## 概要
ジェネレータコルーチン動作を制御する[Promise型](/lang/cpp20/coroutines.md)。


## メンバ関数
### コルーチン

| 名前            | 説明           | 対応バージョン |
|-----------------|----------------|----------------|
| `get_return_object` | [`generator`](../generator.md)戻り値の取得 | C++23 |
| `initial_suspend` | 初期サスペンドポイント動作の制御 | C++23 |
| `final_suspend` | 最終サスペンドポイント動作の制御 | C++23 |
| `yield_value` | co_yield式動作の制御 | C++23 |
| `await_transform` | co_await式動作の制御 | C++23 |
| `return_void` | コルーチンreturn動作の制御 | C++23 |
| `unhandled_exception` | 未処理例外の制御 | C++23 |
| `operator new` | カスタムnew演算子 | C++23 |
| `operator delete` | カスタムdelete演算子 | C++23 |


## バージョン
### 言語
- C++23

### 処理系
- [Clang](/implementation.md#clang):
- [GCC](/implementation.md#gcc):
- [ICC](/implementation.md#icc):
- [Visual C++](/implementation.md#visual_cpp):

## 関連項目
- [`std::ranges::elements_of`](/reference/ranges/elements_of.md)

## 参照
- [P2502R2 `std::generator`: Synchronous Coroutine Generator for Ranges](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2022/p2502r2.pdf)