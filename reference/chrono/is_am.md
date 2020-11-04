# is_am
* chrono[meta header]
* std::chrono[meta namespace]
* function[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::chrono {
  constexpr bool is_am(const hours& h) noexcept;
}
```

## 概要
時間が午前かを判定する。


## 戻り値
```cpp
return 0h <= h && h <= 11h;
```
* 0h[link duration/op_h.md]
* 11h[link duration/op_h.md]


## 例
```cpp example
#include <cassert>
#include <chrono>

namespace chrono = std::chrono;

int main()
{
  chrono::hh_mm_ss time{chrono::hours{15} + chrono::minutes{30} + chrono::seconds{10}};
  assert(chrono::is_am(time.hours()) == false);
  assert(chrono::is_pm(time.hours()) == true);
}
```
* chrono::is_am[color ff0000]
* chrono::hh_mm_ss[link hh_mm_ss.md.nolink]
* time.hours()[link hh_mm_ss/hours.md.nolink]
* chrono::is_pm[link is_pm.md]

### 出力
```
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): 10.0
- [GCC](/implementation.md#gcc): 11.1
- [Visual C++](/implementation.md#visual_cpp): (2019 Update 3時点で実装なし)