---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: convolution/ntt.hpp
    title: convolution/ntt.hpp
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: verify/yosupo/yosupo_convolution.test.cpp
    title: verify/yosupo/yosupo_convolution.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"data_structure/static_modint.hpp\"\ntemplate<int m=998244353>\
    \ struct StaticModint {\n    using mint = StaticModint;\n    int _v;\n\n    constexpr\
    \ StaticModint() : _v(0) {}\n    template<class T>\n    constexpr StaticModint(T\
    \ v) : _v((v % m + m) % m) {}\n\n    constexpr int val() const { return _v; }\n\
    \n    constexpr mint& operator ++ () { return *this += 1; }\n    constexpr mint&\
    \ operator -- () { return *this -= 1; }\n    constexpr mint operator ++ (int)\
    \ { mint res = *this; ++*this; return res; }\n    constexpr mint operator -- (int)\
    \ { mint res = *this; --*this; return res; }\n\n    constexpr mint& operator +=\
    \ (const mint& r) {\n        if(_v >= m - r._v) _v -= m;\n        _v += r._v;\
    \ return *this;\n    }\n    constexpr mint& operator -= (const mint& r) {\n  \
    \      if(_v < r._v) _v += m;\n        _v -= r._v; return *this;\n    }\n    constexpr\
    \ mint& operator *= (const mint& r) {\n        unsigned long long z = _v;\n  \
    \      z *= r._v;\n        _v = (unsigned int)(z % m); return *this;\n    }\n\
    \    constexpr mint& operator /= (const mint& r) {\n        return *this *= r.inv();\
    \ \n    }\n\n    constexpr mint pow(long long n) const {\n        mint x = *this,\
    \ r = 1; \n        while(n) {\n            if(n & 1) r *= x;\n            x *=\
    \ x;\n            n >>= 1;\n        }\n        return r;\n    }\n    constexpr\
    \ mint inv() const {\n        return pow(m - 2);\n    }\n\n    constexpr mint\
    \ operator + () const { return *this; }\n    constexpr mint operator - () const\
    \ { return mint() - *this; }\n\n    constexpr mint operator + (const mint& r)\
    \ const { return mint(*this) += r; }\n    constexpr mint operator - (const mint&\
    \ r) const { return mint(*this) -= r; }\n    constexpr mint operator * (const\
    \ mint& r) const { return mint(*this) *= r; }\n    constexpr mint operator / (const\
    \ mint& r) const { return mint(*this) /= r; }\n    \n    constexpr bool operator\
    \ == (const mint& r) { return _v == r._v; }\n    constexpr bool operator != (const\
    \ mint& r) { return _v != r._v; }\n\n    friend istream& operator >> (istream&\
    \ is, mint& x) {\n        long long t;\n        is >> t;\n        x = mint(t);\n\
    \        return is;\n    }\n    friend ostream& operator << (ostream& os, const\
    \ mint& x) {\n        return os << x._v;\n    }\n};\n"
  code: "template<int m=998244353> struct StaticModint {\n    using mint = StaticModint;\n\
    \    int _v;\n\n    constexpr StaticModint() : _v(0) {}\n    template<class T>\n\
    \    constexpr StaticModint(T v) : _v((v % m + m) % m) {}\n\n    constexpr int\
    \ val() const { return _v; }\n\n    constexpr mint& operator ++ () { return *this\
    \ += 1; }\n    constexpr mint& operator -- () { return *this -= 1; }\n    constexpr\
    \ mint operator ++ (int) { mint res = *this; ++*this; return res; }\n    constexpr\
    \ mint operator -- (int) { mint res = *this; --*this; return res; }\n\n    constexpr\
    \ mint& operator += (const mint& r) {\n        if(_v >= m - r._v) _v -= m;\n \
    \       _v += r._v; return *this;\n    }\n    constexpr mint& operator -= (const\
    \ mint& r) {\n        if(_v < r._v) _v += m;\n        _v -= r._v; return *this;\n\
    \    }\n    constexpr mint& operator *= (const mint& r) {\n        unsigned long\
    \ long z = _v;\n        z *= r._v;\n        _v = (unsigned int)(z % m); return\
    \ *this;\n    }\n    constexpr mint& operator /= (const mint& r) {\n        return\
    \ *this *= r.inv(); \n    }\n\n    constexpr mint pow(long long n) const {\n \
    \       mint x = *this, r = 1; \n        while(n) {\n            if(n & 1) r *=\
    \ x;\n            x *= x;\n            n >>= 1;\n        }\n        return r;\n\
    \    }\n    constexpr mint inv() const {\n        return pow(m - 2);\n    }\n\n\
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
    \ os, const mint& x) {\n        return os << x._v;\n    }\n};"
  dependsOn: []
  isVerificationFile: false
  path: data_structure/static_modint.hpp
  requiredBy:
  - convolution/ntt.hpp
  timestamp: '2024-06-25 02:50:28+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - verify/yosupo/yosupo_convolution.test.cpp
documentation_of: data_structure/static_modint.hpp
layout: document
redirect_from:
- /library/data_structure/static_modint.hpp
- /library/data_structure/static_modint.hpp.html
title: data_structure/static_modint.hpp
---