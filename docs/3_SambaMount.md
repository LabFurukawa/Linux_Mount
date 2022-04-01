<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# 3. Sambaのマウント

SambaはWindowsのディレクトリのネットワーク機能が元となったファイルサーバーのソフトウェアでそれにより作成されたネットワークドライブをLinuxにマウントする。

## パッケージのインストール

```
sudo apt install cifs-utils
```

## マウントポイント
好きなところにマウントすればいいが行儀よくマウントポイントを設定

今回は"samba_dir"というディレクトリを作りマウントする。

```
_YOUR_NAME_@_MACHINE_:~$ sudo mkdir samba_dir
```
これで"/mnt/samba_dir"が作成されたはずである。

## fstab

ここではSambaサーバーが"192.168.1.2"あるとして"Homeディレクトリ"を公開しているとする。
Sambaで登録されているユーザー名を"sample"とパスワードを"samplepassword"とすると

`/etc/fstab`は
```
//192.168.1.2/Home /mnt/samba_dir cifs username=sample,password=samplepassword,defaults 0 0
```
気を付ける点は
- ファイルシステムがcifs。
- 第4引数はcomma区切り、空白なし。
- defaultではなくdefault"s"
- 最終引数を1にしようものならネットワークにつながらなかったりするだけでOSが起動しないことになる。

## マウント確認
```
sudo mount -a
```

## シンボリックリンク

`/mnt/samba_dir`に毎回アクセスするのも面倒なのでショートカットのようなもの : シンボリックリンクをユーザーディレクトリに作成するといい。


`ln`コマンドを使うがシンボリックリンクを利用するときはオプション`-s`を加えて
```
_YOUR_NAME_@_MACHINE_:~$ ln -s /mnt/samba_dir shortcut_samba_dir
```
これにより対象のディレクトリに"shortcut_samba_dir"というファイルができる。

そこに対して
```
_YOUR_NAME_@_MACHINE_:~$ cd shortcut_samba_dir
```
のようにディレクトリのように飛ぶと"/mnt/samba_dir"に移動できる。

どこでも好きにマウントするのは行儀が悪いのでマウントは`/mnt`以下、あとはシンボリックリンクと徹底するというのが望ましいだろう。


----
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
