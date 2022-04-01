<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# 2. 自動マウント

## fstab
Linuxの起動したときに自動でマウントされるデバイスは`/etc/fstab`に記述されている。

```
[device/uuid] [mount-point] [file-system] [options] [dump flsg] [fsck check]
```
|||
|---|---|
| device / uuid | `fdisk -l`などで取得できるDevice名かUUID |
| mount-point | マウントポイント |
| file-system | ex.) ext4, ext3, cifs(SambaやNFSなどのネットワークドライブ) |
| options | 通常は`defaults` 複数指定する場合は空白なしでcomma区切り |
| dump flag | `dump`コマンドの設定　0ならバックアップしない。 普通0 |
| fsck check | `fsck`でデバイスの検査をする順。 ルートファイルシステムが1 0の場合はチェックしない。<br>0でないとき起動時に未接続などでマウント失敗すればOSがRescueモードになる。 普通0 |

### ex.)

`fdisk -l`で取得したデバイス"/dev/sdb1"をLinux起動時に`/mnt`に割り当てるとする。

`/etc/fstab`を`vim`等で編集してファイルに以下を追記
```
/dev/sdb1 /mnt ext4 defaults 0 0
```
区切りはtabでもspaceでも構わない。


## マウント(テスト)
```
sudo mount -a
```
`mount`コマンドで確認する。
不完全なまま再起動をかけると最悪OSが起動できない。

----

[次のセクション "3. Sambaのマウント" へ](./3_SambaMount.md)

----
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
