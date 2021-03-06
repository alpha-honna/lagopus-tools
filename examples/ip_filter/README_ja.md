# IPフィルタ

パケットの宛先がフィルタリング対象のIPアドレスだった場合に、パケットを破棄する。  
対話的にフィルタの追加、削除、確認が行える。

## IPフィルタの使い方

IPフィルタのアプリケーションを実行するためには、Ryuがインストールされている必要がある。
インストールされていない場合は、[README](./path/to/ansible_readme)に従って、OpenFlowスイッチ(Lagopus)とRyuをインストールする。

### IPフィルタの実行

`ryu-manager`からIPフィルタを起動することができる。

```
$ ryu-manager ip_filter.py
```

**Note**: このアプリケーションはIPフィルタ以外の機能を持っていないため、`simple_switch_13.pt`と同時に起動する。

```
$ ryu-manager ip_filter.py simple_switch_13.py
```

### フィルタの追加、削除

アプリケーションが起動すると、端末上に`input > `と表示される。
ここにコマンドの入力してフィルタの追加と削除を行う。

フィルタを追加する。

```
input > add 192.168.0.1
```

フィルタの一覧を表示する。

```
input > show
       DPID       |      IPv4       |      COUNT
------------------+-----------------+------------------
        1         |   192.168.0.1   |        0
```

フィルタを削除する。

```
input > del 192.168.0.1
```

フィルタが削除されていることを確認する。

```
input > show
Filters not found
```

### コマンド一覧

```
add [dpid] ip : フィルタを追加する
del [dpid] ip : フィルタを削除する
show          : 全てのフィルタを表形式で出力する
dump          : 全てのFlow Ruleをjson形式で出力する

ip   : IPアドレス
dpid : 対象とするスイッチのDPID (指定がない場合、全てのスイッチが対象になる)
```






