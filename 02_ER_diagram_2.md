# ER図2
## 全体
- 消費税はどこに入れるか
 > 消費税はどのように管理しますか？
- 入荷管理用のテーブルがない
 > 入荷情報はどのように管理しますか？
- PKのカラム名は「ID」とするのが正しい
 > PKのカラム名は全て「ID」にしましょう。

## 管理者
- エンドユーザーとリレーションを結ぶは必要はない
 > エンドユーザーとのリレーションは必要ありますか？
- 商品とリレーションを結ぶは必要はない
 > 商品とのリレーションは必要ですか？

## エンドユーザー
- 名カラムがない
 > 「名」カラムが抜けています。
- 配送先と住所はべつ？
 > 配送先にはどのような情報が入りますか？住所=配送先ではないということでしょうか？
- 住所を一つしか持てない
 > ユーザーが住所を複数持つ場合は、住所をどのように管理しますか？

## 商品
- 「ディスク枚数カラム」必要ない
 > 「ディスク枚数」カラムは必要ですか？
- 論理削除考慮していない
 > 商品を削除した場合、該当するレコードはどうなりますか？
- [商品]が1で[ディスク]が多の関係が適切。リレーションが逆、「ディスクID」必要ない
 > [商品]が1で[ディスク]が多の関係が適切です。リレーションが逆で「ディスクID」も必要ありません。
- 発売日カラムがない
 >　発売日カラムがが抜けいています。
- 在庫数カラムは必要ない
 > 在庫数カラムがありますが、在庫数はカラムで管理するべきではありません。
- カートアイテムとのリレーションが1対1以上となっているが、正しくは1対0以上
 > カートアイテムとのリレーションが1対1以上となっているが、正しくは1対0以上です。

## ディスク
- [ディスク]が1で[曲]が多の関係が適切。リレーションが逆、「曲名ID」は必要ない
 > [ディスク]が1で[曲]が多の関係が適切です。リレーションが逆で「曲名ID」も必要ありません。
- トラックNo.の用途が不明。ディスクの番号を把握したいはずなので、「ディスク番号」などにすべき
 > 「トラックNo.」となっていますが、ディスクの番号を把握したいはずなので、「ディスク番号」などにすべきです。

## 曲名
- 曲順を管理できない
 > 曲順はどのように管理しますか？
- ##ディスク でも述べたとおり、リレーションが逆。FKとして「ディスクID」をもつ必要がある
 > ##ディスク でも述べたとおり、リレーションが逆なのと、FKとして「ディスクID」をもつ必要があります。

## カートアイテム
- PKがない
 > PKがぬけています。
- まだ購入していないので「購入枚数」という名前は適切でない。「小計金額」カラムは必要ない。
 > カートに追加した時点では、まだ購入していないはずなので、「購入枚数」という名前は適切でないのと、「小計金額」カラムは「商品ID」から「税別価格」の情報を取り出し「税別価格 * 枚数 (* 消費税)」という式で算出できるので、必要ありません。

## 購入詳細
- テーブル名は管理者視点で命名すべきなので、「受注詳細」にすべき
 > テーブル名は管理者目線で「受注詳細」などと命名しましょう。
- FKとして「商品id」がない→[商品]とリレーションを結ぶ必要がある。
 > 購入した商品が何かはどう判別しますか？
- [購入]が1で[購入詳細]が多の関係が適切。「購入ID」が必要
 > [購入]が1で[購入詳細]が多の関係が適切です。リレーションが逆で「購入ID」が必要です。
- 購入時価格を保持するカラムがない
 > 購入したときの価格はどのように管理しますか？

## 購入
- テーブル名は管理者視点で命名すべきなので、「受注」にすべき
> テーブル名は管理者目線で「受注」などと命名しましょう。
- ##購入詳細でも述べたが[購入]が1で[購入詳細]が多の関係が適切。「購入詳細ID」は必要ない
 > ##購入詳細でも述べたとおり、[購入]が1で[購入詳細]が多の関係が適切で、FKの「購入詳細ID」は必要ありません。
- 郵便番号カラムがない
 > 郵便番号カラムが抜けています。
- 購入日は登録日時で代用できる
 > 購入日は登録日時と同じ内容なので必要ありません。

## ジャンル,レーベル,アーティスト
- [商品]テーブルとのリレーションの記号が誤っている,1対1以上ではなく1対0以上
 > [商品]テーブルとのリレーションの記号が間違っています。1対1以上ではなく1対0以上が適切です。

## ジャンル
- カラムに「ジャンル」とあるが、何が入るのかわからないので「ジャンル名」とすべき
 > ジャンルというカラム名では何が入るかわからないので、「ジャンル名」としましょう。

## レーベル
- カラムにレーベルとあるが、何が入るのかわからないので「レーベル名」とすべき
 > レーベルというカラム名では何が入るかわからないので、「レーベル名」としましょう。



# 指摘事項

## エンドユーザー
- 配送先と住所はべつ？
 > 配送先と住所はどのような違いがありますか？
    - これはどういうことでしょうか？
## カートアイテム
- まだ購入していないので「購入枚数」という名前は適切でない。「小計金額」カラムは必要ない。
 > カートに追加した時点では、まだ購入していないはずなので、「購入枚数」という名前は適切でないのと、「小計金額」カラムは必要ありません。
    - 小径金額カラムはなぜ必要ではないかまでかけると○
## 購入詳細
- FKとして「商品id」がない→[商品]とリレーションを結ぶ必要がある。
 > 商品と購入詳細は1:多の関係ではありませんか？
    - 購入した商品が何かはどう判別できますか？というような書き方が良いかなと思います！