# Ruby 2.6 on Rails

### Ginza.rb / @y-yagi

---

### これは何

Ruby 2.6に向けて、Railsでも色々な対応が行われました(& 行われています). いつも通りですね. 何があったか見てみましょう、という資料です.

---

### そもそもテストは通っているか

これ書いている時点ではまだ

---

### 何がエラーになっているか

BigDecimal関連

https://travis-ci.org/rails/rails/jobs/469320845#L2562-L2564

---

### BigDecimal

* compatibility issuesがある
  * https://github.com/ruby/ruby/blob/trunk/NEWS#stdlib-compatibility-issues-excluding-feature-bug-fixes
* BigDecimal() や String#to_d の結果が地味に変わっている
* その変更に対する対応がまだ足りていない

---

### BigDecimal

```ruby
# BigDecimal 1.3
"1,1".to_d # => 0.1e1

# BigDecimal 1.4
"1,1".to_d # => 0.0
```

---

### それ以外の対応をざっと

---

### Range#===

* [Allow Range#=== and Range#cover? on Range](https://github.com/rails/rails/commit/0fcb921a65e615c301450d7820b03473acd53898)
  * `Range#===`がRange#include?`ではなく`cover?`を使うようになった対応の影響
* これ5.2にバックポートするの忘れていたので、今リリースされているRails全てで期待通りに動作しないはず

---

### warning出る系

* [Deprecate safe_level of `ERB.new` in Ruby 2.6](https://github.com/rails/rails/pull/32170)
* [Do not use deprecated Object#!~ in Ruby 2.6](https://github.com/rails/rails/commit/db080527a4b6915b1ae7d9bc678467990ecece61)
* [Ruby 2.6 will not require monkey patched `URI#unescape`](https://github.com/rails/rails/pull/32319)
* [2.6 warnings: passing splat keyword arguments as a single Hash](https://github.com/rails/rails/pull/32447)

---

### 結論

RangeとBigDecimal以外はwarning出るだけのはずだけど、気になる人は[[WIP] Ruby 2.6 suport for 5-2-stable branch](https://github.com/rails/rails/pull/34720) がマージされるまではちょっと待って
