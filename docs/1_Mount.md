<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# 1. マウント

Ubuntu DesktopはUSBメモリを指した場合、自動的にその内容を読み込む。
しかしこれはマウントという操作を自動的に行っているためである

`マウント`は取り付けられた記憶メディアを任意のディレクトリに紐づけてその中にメディアの中身が存在するように割り振る行為である。

ここでは手動でドライブなどをマウントする手順を示す。

## デバイスを探す

```
sudo fdisk -l
```
以上のコマンドですべてのドライブを取得できる。
```
Disk /dev/sda: 465.78 GiB, 500107862016 bytes, 976773168 sectors
Disk model: xxxx
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: gpt
Disk identifier: xxxx

Device       Start       End   Sectors   Size Type
/dev/sda1     2048   1050623   1048576   512M EFI System
/dev/sda2  1050624   3147775   2097152     1G Linux filesystem
/dev/sda3  3147776 976771071 973623296 464.3G Linux filesystem
```
上のようにデバイスとパーティションが列挙される。


## [command] `mount`

デバイスをマウントポイント(任意のディレクトリ)にマウントする。

一般的には/mntかその下のディレクトリ

```
mount [options] [device] [mount-point]
```
ここで`/dev/sdb`にパーティション`/dev/sdb1`というデバイスがあった場合

```
_YOUR_NAME_@_MACHINE_:~$ sudo mount /dev/sdb1 /mnt
```
で`/mnt`ディレクトリにマウントされる。

## デバイスへのアクセス

`/mnt`ディレクトリにマウントした場合普通のディレクトリと同じように
```
_YOUR_NAME_@_MACHINE_:~$ cd /mnt
```
のように`cd`コマンドなどで利用することができる。

## 複数のマウント

マウントするデバイスは1つでないことも少なくない。例えばHDDを2つ追加でマウントしたい場合もあるだろうが1つのマウントポイントにマウントすることができるのは1つだけである。

`/mnt`に複数割り当てるわけにもいかないので`/mnt`にディレクトリを作ってそこにマウントする。

例えば
```
_YOUR_NAME_@_MACHINE_:~$ sudo mkdir /mnt/hdd1
_YOUR_NAME_@_MACHINE_:~$ sudo mkdir /mnt/hdd2
```
とディレクトリを作れば
```
_YOUR_NAME_@_MACHINE_:~$ ls /mnt
hdd1 hdd2
```
となるだろう。ここに対して
```
_YOUR_NAME_@_MACHINE_:~$ sudo mount /dev/sdb1 /mnt/hdd1
_YOUR_NAME_@_MACHINE_:~$ sudo mount /dev/sdc1 /mnt/hdd2
```
という風に`fdisk -l`で取得したHDD 1個目 "/dev/sdb1"と2個目 "/dev/sdc1"をそれぞれのディレクトリにマウントすることができる。

----

[次のセクション "2. 自動マウント" へ](./2_AutoMount.md)

----
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
