---
data:
  _extendedDependsOn:
  - icon: ':x:'
    path: convolution/ntt.hpp
    title: convolution/ntt.hpp
  - icon: ':x:'
    path: data_structure/static_modint.hpp
    title: data_structure/static_modint.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/convolution_mod
    links:
    - https://judge.yosupo.jp/problem/convolution_mod
  bundledCode: "#line 1 \"test/verify/yosupo_convolution.test.cpp\"\n#define PROBLEM\
    \ \"https://judge.yosupo.jp/problem/convolution_mod\"\n\n#include <bits/stdc++.h>\n\
    using namespace std;\n\n#line 1 \"data_structure/static_modint.hpp\"\ntemplate<int\
    \ m=998244353> struct StaticModint {\n    using mint = StaticModint;\n    int\
    \ _v;\n\n    constexpr StaticModint() : _v(0) {}\n    template<class T>\n    constexpr\
    \ StaticModint(T v) : _v((v % m + m) % m) {}\n\n    constexpr int Val() const\
    \ { return _v; }\n\n    constexpr mint& operator ++ () { return *this += 1; }\n\
    \    constexpr mint& operator -- () { return *this -= 1; }\n    constexpr mint\
    \ operator ++ (int) { mint res = *this; ++*this; return res; }\n    constexpr\
    \ mint operator -- (int) { mint res = *this; --*this; return res; }\n\n    constexpr\
    \ mint& operator += (const mint& r) {\n        if(_v >= m - r._v) _v -= m;\n \
    \       _v += r._v; return *this;\n    }\n    constexpr mint& operator -= (const\
    \ mint& r) {\n        if(_v < r._v) _v += m;\n        _v -= r._v; return *this;\n\
    \    }\n    constexpr mint& operator *= (const mint& r) {\n        unsigned long\
    \ long z = _v;\n        z *= r._v;\n        _v = (unsigned int)(z % m); return\
    \ *this;\n    }\n    constexpr mint& operator /= (const mint& r) {\n        return\
    \ *this *= r.inv(); \n    }\n\n    constexpr mint Pow(long long n) const {\n \
    \       mint x = *this, r = 1; \n        while(n) {\n            if(n & 1) r *=\
    \ x;\n            x *= x;\n            n >>= 1;\n        }\n        return r;\n\
    \    }\n    constexpr mint Inv() const {\n        return Pow(m - 2);\n    }\n\n\
    \    constexpr mint operator + () const { return *this; }\n    constexpr mint\
    \ operator - () const { return mint() - *this; }\n\n    constexpr mint operator\
    \ + (const mint& r) const { return mint(*this) += r; }\n    constexpr mint operator\
    \ - (const mint& r) const { return mint(*this) -= r; }\n    constexpr mint operator\
    \ * (const mint& r) const { return mint(*this) *= r; }\n    constexpr mint operator\
    \ / (const mint& r) const { return mint(*this) /= r; }\n    \n    constexpr bool\
    \ operator == (const mint& r) { return _v == r._v; }\n    constexpr bool operator\
    \ != (const mint& r) { return _v != r._v; }\n\n    friend istream& operator >>\
    \ (istream& is, mint& x) {\n        long long t;\n        is >> t;\n        x\
    \ = mint(t);\n        return is;\n    }\n    friend ostream& operator << (ostream&\
    \ os, const mint& x) {\n        return os << x._v;\n    }\n};\n#line 2 \"convolution/ntt.hpp\"\
    \n\nstruct NTT{\n    using mint = StaticModint<998244353>;\n\n    // n: \u7573\
    \u307F\u8FBC\u307F\u5F8C\u306E\u6570\u5217\u306E\u30B5\u30A4\u30BA\n    // nunv:\
    \ n\u306E\u9006\u6570\n    int n, ninv;\n    const mint MOD = 998244353, g = 3;\n\
    \n    // br: \u30D3\u30C3\u30C8\u53CD\u8EE2\u5217\n    // roots: MOD\u4E0A\u306E\
    1\u306En\u4E57\u6839\u306E\u5217\n    vector<int> br;\n    vector<mint> roots;\n\
    \n    NTT() {}\n\n    // \u30D3\u30C3\u30C8\u53CD\u8EE2\u5217\u306E\u751F\u6210\
    \n    // N = 8\u306E\u4F8B\n    // {0}\u306E\u5404\u8981\u7D20\u306B2 ^ 2\u3092\
    \u52A0\u3048\u3066{0, 4}\n    // {0, 4}\u306E\u5404\u8981\u7D20\u306B2 ^ 1\u3092\
    \u52A0\u3048\u3066{0, 4, 2, 6}\n    // {0, 4, 2, 6}\u306E\u5404\u8981\u7D20\u306B\
    2 ^ 0\u3092\u52A0\u3048\u3066{0, 4, 2, 6, 1, 5, 3, 7}\n    void BitReversal(int\
    \ n) {\n        br.resize(n);\n        int p = 1, d = n / 2;\n        while(p\
    \ < n) {\n            for(int i = 0; i < p; i++) {\n                br[i + p]\
    \ = br[i] + d;\n            }\n            p *= 2;\n            d /= 2;\n    \
    \    }\n    }\n\n    // MOD\u4E0A1\u306En\u4E57\u6839\u306E\u914D\u5217\u3092\u751F\
    \u6210\n    // n: \u8981\u7D20\u6570(2\u51AA)\uFF0Cw: 1\u306En\u4E57\u6839\u306E\
    \u3072\u3068\u3064\n    void NthRoots(int n, mint w) {\n        roots.resize(n);\n\
    \        roots[0] = 1;\n        for(int i = 1; i < n; i++) {\n            roots[i]\
    \ = roots[i - 1] * w;\n        }\n    }\n\n    // \u518D\u5E30\u7684\u306B\u5909\
    \u63DB\n    // l: \u66F4\u65B0\u5BFE\u8C61\u533A\u9593\u306E\u5DE6\u7AEF\uFF0C\
    len: \u66F4\u65B0\u5BFE\u8C61\u533A\u9593\u306E\u9577\u3055\n    void TransformRecursive(vector<mint>&\
    \ c, int l, int len) {\n        if(len == 1) return;\n        int d = n / len,\
    \ h = len / 2;\n\n        TransformRecursive(c, l, h);\n        TransformRecursive(c,\
    \ l + h, h);\n\n        // \u30D0\u30BF\u30D5\u30E9\u30A4\u6F14\u7B97\n      \
    \  for(int i = 0; i < h; i++) {\n            mint v0 = c[l + i];\n           \
    \ mint v1 = c[l + h + i] * roots[d * i];\n            c[l + i] = (v0 + v1);\n\
    \            c[l + h + i] = (v0 - v1 + MOD);\n        }\n    }\n\n    // \u6570\
    \u8AD6\u5909\u63DB\uFF0C\u9577\u3055\u306F2\u51AA\n    // c: \u5909\u63DB\u5217\
    \uFF0Cinv: \u9006\u5909\u63DB\u304B\u3069\u3046\u304B\n    vector<mint> Transform(vector<mint>&\
    \ c, bool inv=false) {\n        vector<mint> ret(n, 0);\n\n        // \u30D3\u30C3\
    \u30C8\u53CD\u8EE2\u7F6E\u63DB\n        for(int i = 0; i < c.size(); i++) {\n\
    \            ret[br[i]] = c[i];\n        }\n\n        TransformRecursive(ret,\
    \ 0, n);\n\n        // NTT\u306A\u3089\u305D\u306E\u307E\u307E\u51FA\u529B\n \
    \       if(!inv) return ret;\n\n        // INTT\u306A\u3089(0, N)\u306E\u7BC4\u56F2\
    \u3092\u9006\u9806\u306B\u4E26\u3073\u66FF\u3048\uFF0CN\u3067\u5272\u308B(ninv\u3092\
    \u639B\u3051\u308B)\n        reverse(ret.begin() + 1, ret.end());\n        for(int\
    \ i = 0; i < n; i++) {\n            ret[i] *= ninv;\n        }\n        return\
    \ ret;\n    }\n\n    // \u7573\u307F\u8FBC\u307F\n    vector<long long> Convolution(vector<long\
    \ long>& a, vector<long long>& b) {\n        // n\u306E\u8A08\u7B97\n        n\
    \ = 1; while(n < a.size() + b.size() - 1) n *= 2;\n\n        // ninv\u306E\u8A08\
    \u7B97\n        ninv = mint(n).inv().val();\n\n        BitReversal(n);\n\n   \
    \     // 1\u306En\u4E57\u6839\u8A08\u7B97\n        // MOD - 1 = 119 * 2 ^ 23 =\
    \ d * n\u3068\u8868\u305B\u308B(n\u306F2\u51AA)\n        // g ^ (MOD - 1) = (g\
    \ ^ d) ^ n \u2261 1\u306A\u306E\u3067\uFF0C\u03C9 = g ^ d\n        int d = ((MOD\
    \ - 1) / n).val();\n        mint w = g.pow(d);\n        NthRoots(n, w);\n\n  \
    \      vector<mint> ma(a.size()), mb(b.size());\n        for(int i = 0; i < (int)a.size();\
    \ i++) {\n            ma[i] = a[i];\n        }\n        for(int i = 0; i < (int)b.size();\
    \ i++) {\n            mb[i] = b[i];\n        }\n\n        vector<mint> fa = Transform(ma);\n\
    \        vector<mint> fb = Transform(mb);\n\n        for(int i = 0; i < n; i++)\
    \ {\n            fa[i] *= fb[i];\n        }\n\n        auto c = Transform(fa,\
    \ true);\n\n        vector<long long> ret(a.size() + b.size() - 1);\n        for(int\
    \ i = 0; i < (int)a.size() + b.size() - 1; i++) {\n            ret[i] = c[i].val();\n\
    \        }\n\n        return ret;\n    }\n};\n#line 7 \"test/verify/yosupo_convolution.test.cpp\"\
    \n\nint main() {\n    int N, M;\n    cin >> N >> M;\n    vector<long long> A(N),\
    \ B(M);\n    for(int i = 0; i < N; i++) {\n        cin >> A[i];\n    }\n    for(int\
    \ i = 0; i < M; i++) {\n        cin >> B[i];\n    }\n\n    NTT ntt;\n\n    auto\
    \ c = ntt.Convolution(A, B);\n\n    for(auto i : c) {\n        cout << i << \"\
    \ \";\n    }\n    cout << endl;\n\n    return 0;\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/convolution_mod\"\n\n#include\
    \ <bits/stdc++.h>\nusing namespace std;\n\n#include \"../../convolution/ntt.hpp\"\
    \n\nint main() {\n    int N, M;\n    cin >> N >> M;\n    vector<long long> A(N),\
    \ B(M);\n    for(int i = 0; i < N; i++) {\n        cin >> A[i];\n    }\n    for(int\
    \ i = 0; i < M; i++) {\n        cin >> B[i];\n    }\n\n    NTT ntt;\n\n    auto\
    \ c = ntt.Convolution(A, B);\n\n    for(auto i : c) {\n        cout << i << \"\
    \ \";\n    }\n    cout << endl;\n\n    return 0;\n}"
  dependsOn:
  - convolution/ntt.hpp
  - data_structure/static_modint.hpp
  isVerificationFile: true
  path: test/verify/yosupo_convolution.test.cpp
  requiredBy: []
  timestamp: '2024-06-21 23:20:27+09:00'
  verificationStatus: TEST_WRONG_ANSWER
  verifiedWith: []
documentation_of: test/verify/yosupo_convolution.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo_convolution.test.cpp
- /verify/test/verify/yosupo_convolution.test.cpp.html
title: test/verify/yosupo_convolution.test.cpp
---