# Git 入門

このドキュメントは非技術者 & Windows ユーザ向けに Git の使い方をまとめたものです。

##### 関連情報

* [Backlog](https://coopnext.backlog.jp/projects/TECH_STUDY)
* Git for Windows 関連
    + [Git for Windows のインストール方法](https://qiita.com/elu_jaune/items/280b4773a3a66c7956fe)
    + [Git for Windows のダウンロード](https://git-scm.com/download/win)
    + [Git for Windows の初期設定 & ssh-key の作り方](https://qiita.com/hollyhock0518/items/a3fee20951cd92c87ed9)
* SourceTree 関連
    + [佐野さん資料](https://coopnext.backlog.jp/alias/file/1094505376)
    + [SourceTree のダウンロード](https://www.atlassian.com/ja/software/sourcetree)

## Git とは

* ファイルのバージョン管理システムのひとつ

* 「分散型」の特徴を持つ
    
    * cf:「subversion」は中央集中型
    
* サーバ不要・ローカルだけでも完結
* 他者と共有する場合はリモートリポジトリが必要

* リモートとのやりとりはまとめて行う
    * ローカルで commit & commit & commit ....
    * あとでまとめて反映！（push）
    
* とにかく速い！

    * リモートとのやりとりがミニマム
    * リモートへの送受信はバイナリデータ

* 賢い！
  
    * 適当にmergeしてもいい感じにやってくれる
    
    

### そもそもバージョン管理とはなんぞや

* テキストファイルについて __行単位__ で変更履歴を残す仕組み

* いつ・誰が・どのファイルのどの行に・どのような変更を行ったのかを履歴に残す

* 特定の履歴へバージョンを戻す、特定の履歴のみ適用する・撤去する などが可能

* 画像ファイルなどのテキストファイル以外のバージョン管理には不向き

    

## ことば

* __リポジトリ__
    * 実体はコミット(変更内容)の集合
    * 一般的には、バージョン管理する対象ブランチ群・ファイル群・変更内容一式をまとめて指す

* __ローカル（リポジトリ）__

* __リモート（リポジトリ）__

* __ブランチ__
  
    * 実体は関連するコミットの集合
    * 一般的には、ファイル群一式で捉えられる
    * 初期ブランチは「master」
    * 案件・作業ごとに切り替えて使用する
    
* __コミット（ハッシュ）__
    * 変更内容のこと
    * git のコミットIDは 40文字のランダムな英数字(SHA-1ハッシュ)で表す
        * 例: ```43625a2de9c9913e099afa3bd62a88333f1f70d4```
        * リポジトリを超えて一意
    * 先頭の7文字でもOK
        * 例: ```43625a2```
    
    

##### リポジトリとブランチのイメージ

![repo_image](https://raw.githubusercontent.com/uzura8/git_study/master/img/repo_image.png)



## 手順超概要

__変更をまとめて(add して)から確定！(commit)__

__確定した変更をまとめてリモートにドン！(push)__

1. 手元でファイルを変更する
2. 作業のキリのいいところで「変更まとめ（index）」に追加する(add)
3. やりたいことが完了したら「変更まとめ（index）」リポジトリに登録する(commit)

4. 納品など、他への共有が必要になったらリモートリポジトリに反映する(push)



## 必須操作（コマンド）

### 設置系

* __git init__
    * ローカルに新規にリポジトリ作る・リポジトリの初期化
    * git remote add <remote のリポジトリURL> →  git push でremoteリポジトリ作成
* __git clone__
    * リモートリポジトリをとってくる
    * ```git clone <リモートリポジトリのURL> (設置ディレクトリ名)```
        * 「設置ディレクトリ名」を省略するとリポジトリ名が適用される
* __git checkout__
    * ローカルにてブランチを切り替える
    * 変更の取り消しにも使う

### ローカル系

#### 確認系

* __git branch__
    * 現在のブランチを確認する
    * -r オプションをつけると remote のブランチも確認
* __git status__
    * 現在の local の変更状態を確認する
        * modified: 変更あり
        * deleted: 削除された など
* __git diff__
    * 現在の local の変更差分を確認する
    * その他、色々応用あり

* __git show__
    * コミットハッシュを指定して変更内容を確認する
        * ```git show コミットハッシュ```

* __git log__
    * 変更履歴を確認する
    * -p オプションをつけると、差分付きで確認できる

#### 編集系

* __git add__
    * 現在の変更をコミット対象（インデックス）に追加する
* __git commit__
    * コミット対象（インデックス）に追加された変更を確定する（コミットする）
    * コミットメッセージは適切に指定すべし（後々助かる）
        * →「コミットメッセージ」の章を参照
* __その他__
    * git rm: ファイル削除(remove)
    * git mv: ファイル移動(move)

#### 管理・運用系

* __git merge__
    * 

### リモートやり取り系

* __git fetch__
  
    * remote の変更をまとめて local に持ってくる（反映はしない）
* __git pull__
    * ブランチを指定してremote の変更をとってきて、反映する
    * 例: remote の ブランチ「hoge」 を local の「hoge」 に反映する
        * ```git pull --rebase origin hoge```
    * git fetch && git merge と同じ
* __git push__
    *  local の変更を remote に送る
    *  例: local の ブランチ「hoge」 を remote の「hoge」 に反映する
        * ```git remote origin hoge```
    
    

##### リモートリポジトリとのやり取りのイメージ

![remote_repo_image](https://raw.githubusercontent.com/uzura8/git_study/master/img/remote_repo_image.png)


## 運用のコツ

#### 作業前には必ずリモートの変更をとってこよう！

* git pull --rebase する
* 同じところ変更すると push 時にエラーになるよ

#### コミット前に必ず差分を確認しよう！

* 意図しない変更は無いか？
* 改行コード・文字コードが変わっていないか？
* 変なインデント・不要な空白はないか？

##### 差分の確認方法

まとめ中

#### 適切なコミットメッセージを必ずつけよう！

ルールまとめ中

#### ちゃんとしたイケてるエディタを使おう！

まとめ中



## 運用ルール（git flow）

まとめ中



## 実際にやってみよう！

#### 1. ツールのインストール

* GUI（グラフィカルなツールで）
    * SourceTree
    * TortoiseGit
* CUI（コマンドで）
    * Git for Windows ※推奨
* エディタ付属型
    * VSCode
    * ATOM (オマケ的についている)

#### 2. remote リポジトリを local に持ってくる

* git clone

#### 3. 自分用のブランチを作ろう

* git checkout -b 新ブランチ名

#### 4. 変更しよう

* git diff

#### 5. コミットしよう

* git add / git commit

#### 6. remote に反映しよう

* git push

#### 7. メンバーの変更を merge しよう

* git merge



## 確認環境（pgit.be）

事前に登録したリポジトリの変更を、実際のパス構成でリアルタイムに確認可能な環境

※リポジトリ追加時のみ山田まで要連絡

#### ドメインのルール

* __サブドメイン__ 
    * 「リポジトリ識別子」と「変換したブランチ名」を「. (ドット)」で連結したもの
    * __変換したブランチ名__
        * ドメインに使用不可の文字（ / _ @ など）を「- (ハイフン)」に置換
        * 大文字は小文字に置換
* 例: リポジトリ「shop」のブランチ「feature/ACTION-123」のURL
    * http://shop.feature-action-123.pgit.be



##### 変更&確認フロー

![deploy_flow](https://raw.githubusercontent.com/uzura8/git_study/master/img/deploy_flow.png)



## その他のトピック

#### 「リモートリポジトリのURL」とは？

* git clone で指定するURL
* プロトコルは ssh と https の2種類ある
* ssh でやり取りする場合、ssh-key の作成・登録が必要（最初だけ）
* https  でやり取りする場合、ID/PASS の入力が都度必要（ツールにより覚えてくれる）

#### ssh-key の作成・登録

* 「Git for WIndows」を入れた場合の ssh-key の作成方法
    * 参考: https://qiita.com/hollyhock0518/items/a3fee20951cd92c87ed9
* 都度パスフレーズの入力が面倒な場合はパスフレーズを指定しない（空エンターする）
* 秘密鍵（id_rsa）と公開鍵（id_rsa.pub）が作成される
* リモートリポジトリを提供するサービスに公開鍵（id_rsa.pub）を登録する

#### origin って何？

* git はリモートリポジトリを複数登録できる（1対多 にできる）
* 紐づくリモートリポジトリのあだ名（識別名）を自由につけられる
* 「origin」はデフォルトのあだ名（変更可）

![origin_image](https://raw.githubusercontent.com/uzura8/git_study/master/img/origin_image.png)

