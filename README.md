# laravel_dev
laravel開発用
これをフォークすることによりプロジェクトを作成してください。

homestead,vagrant,virtualboxな環境です。
あらかじめ
vagrant,virtualbox,vagrant-vbguest
はインストールしてください。
フォークしたプロジェクトは
```
$ cd laravel_dev
$ git submodule init homestead_vagrant/
$ git submodule update homestead_vagrant/
$ cd homestead_vagrant
$ vagrant up
```
で簡単にvagrant環境を作成することができ、

vagrant guestOS側で
```
vagrant@vagrant:~/projects/:$ laravel new your_project
```

という形でlaravel環境を作成することができます。

host側からみると
laravel_dev/projects/
配下にプロジェクトが作成されます。

vscodeなどでホスト側から
ファイルを修正することができます。

コマンドを打つときはguest側の
osからコマンドを入力してください。

## visual studiocodeでの開発について
ほぼ必須なプラグイン一覧

```
$ code --install-extension onecentlin.laravel5-snippets # Laravel Snippets
$ code --install-extension onecentlin.laravel-blade # Laravel Blade Snippets
$ code --install-extension thekalinga.bootstrap4-vscode # Bootstrap 4, Font awesome 4, Font Awesome 5 Free & Pro snippets
```

## データベースについて
homesteadを使っているため、
mysqlは
user: homestead
password: secret

user: root
password: secret

postgresqlは
user: homestead
password: secret

user: postgres
password: postgres

が予め作成されています。

どちらを使うにせよ
簡単のため、
```
# useradd homestead
```
としてGuestOS側にもホームディレクトリを作成せず、ユーザーだけ作成することをおすすめします。

また、使わない方のデータベースを
```
# systemctl disable [RDB to want to stop]
```

としてデータベースを止めておくこと。
初期設定では、laravelはmysqlが
config/database.php
に書かれているので、迷ったらmysqlの方がいいかも。

## aws,gcpについて
submodule homestead_vagrant側のVagrantファイルに
awscli,gcloudコマンドを
インストールするようにスクリプトが書かれている。
もし必要無いなら、コメントアウトすること。

## dataディレクトリについて
プロジェクトの内容以外の
GuestOS,HostOS間のデータのやりとりに利用してください。
.gitignoreにdataフォルダ配下のファイルは無視するように
書かれているので、それぞれの開発用PCで共有したいファイルに使うと
いい感じです。

## projectsディレクトリについて
projectsディレクトリはにもdataディレクトリ同様に、
gitignoreが使われているので、projects配下のファイルは
laravel_devから無視されます。

/home/vagrant/projects/your_projects
のみgithubなり、awsなり、gcpなりにレポジトリを作って
ソースコードを管理してください。

## submoduleについて
submodule側のレポジトリが更新された場合は下のコマンドで追随します。
```
$ git submodule foreach git pull origin master
```

## 未実装
### eclipse theia 
[公式サイト](https://theia-ide.org/)
gcp,IBM,gitpodなどで実績はあるが、
まだ、vscodeにあって、eclipse theiaに無いプラグインがあるため
未実装。
http以外のvagrant GuestOSのポート以外は
閉じた状態、かつprivate networkでvaglant環境内にIDE含め開発環境がすべて揃うため
ぜひ導入したい。
名だたる企業がcontributerのため、一般にも定着するのは早く2020年末から2021年だと思われる。
