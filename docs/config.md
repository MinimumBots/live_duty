# 設定コマンドの解説
キス魔では、ボットへの**メンションに続けて**指定されたコマンド文と設定値を入力し、
送信することで設定値を反映させることができます。  
メンション、コマンド文、設定値の間は**必ず**半角スペース1文字で区切ってください。  
  
以下のコマンド解説では`{a|b}`のように表記された部分は`a`か`b`どちらかを入力し、
`<variable>`のように表記された部分は、設定したい値を入力してください。  
また、`...`が付く表記は、その部分を2つ以上入力することができます。  

## 共通設定

### 管理者ロール
設定コマンドは**管理者**権限を持ったメンバー全員が実行できますが、
管理者ロールに登録されたロールは権限に関わらず、設定コマンドを実行できるようになります。  
  
`<role>`にはロールメンション、またはロールIDを指定します。  
```
admin {add|remove} <role>...
```

## 実況チャンネル設定

### 実況受付チャンネル
実況を受け付けるチャンネルを設定できます。  
設定されたチャンネルでURLを含むメッセージが送信されると、自動で実況チャンネルを確保します。  
実況チャンネルを設定していない場合は実況チャンネル機能が無効になります。  
設定の変更と同時に、[実況チャンネル名](#実況チャンネル名)に一致するチャンネルが検索され、
そのチャンネル数がチャンネル数の
[上限値と下限値](#実況チャンネル上限・下限)に、それぞれ設定されます。  
  
`<channel>`にはチャンネルメンション、またはチャンネルIDを指定します。  
```
live {set|remove} <channel>
```

### 実況チャンネル名
指定された実況チャンネル名を元に、`実況チャンネル1, 実況チャンネル2, 実況チャンネル3...`
といった、数字が付くチャンネルを実況チャンネルとして認識します。  
設定の変更と同時に、名前と一致するチャンネルが検索され、
そのチャンネルの数がチャンネル数の
[上限値と下限値](#実況チャンネル上限・下限)に、それぞれ設定されます。  
また、ボットによって自動的にチャンネルが作成される際にも、この名前が使用されます。  
  
`<string>`には設定したいチャンネル名を最大90文字で指定します。  
```
live name <string>
```

### トピック・レート制限(秒)・NSFW
ボットがチャンネルを作成する際に設定される
チャンネルのトピック・レート制限・NSFWを指定できます。  
  
`<topic>`には設定したいトピックを最大900文字で指定します。  
`<limit>`には設定したいレート制限(秒)を半角数字で指定します。  
```
live topic <topic>
live rate-limit <limit>
live nsfw {enable|disable}
```
この設定値は、その後ボットによってチャンネルが作成される際に反映されます。  

### 実況開始可能ロール
[実況受付チャンネル](#実況受付チャンネル)で実況を開始できるロールを設定します。  
ロールが1つも登録されていない場合は、すべてのメンバーが実況を開始できます。  

`<role>`にはロールメンション、またはロールIDを指定します。  
```
live allow {add|remove} <role>...
```

### 実況チャンネル上限・下限
実況チャンネルの数の上限と下限を設定できます。  
通常は上限・下限ともに、元のチャンネル数と同じ数が指定されていますが、
上限値を下限値より大きい値にすることで、実況チャンネルが不足した際に
上限値に達するまで自動でチャンネルを作成します。  
自動で作成されたチャンネルは実況終了後に、自動で削除されます。  
  
また、下限値を変更するとそれに併せて過不足分のチャンネルを追加/削除します。  
  
なお、実況チャンネルが上限に達した場合でも、
**チャンネルの管理**権限を持ったメンバーや[管理者ロール](#管理者ロール)
に登録されたロールを持つメンバーは、🆕リアクションを押すことで
一時的にチャンネルを増やすことができます。  
  
`<limit>`には上限値・下限値を半角数字で指定します。  
```
live {min|max} <limit>
```

### 実況終了リアクション絵文字
実況受付チャンネルで開始した実況を終了させるリアクションを設定できます。  
  
`<emoji>`にはデフォルト絵文字かサーバー絵文字を1文字指定できます。  
```
live close-emoji <emoji>
```

### 実況終了を本人に限定
実況を終了できるメンバーを本人に限定します。  
ただし、**チャンネルの管理**権限を持ったメンバーや[管理者ロール](#管理者ロール)
に登録されたロールを持つメンバーは、設定に関係なく実況を終了できます。  
  
```
live only-self {enable|disable}
```

### 実況終了後の発言無効ロール
実況終了後のチャンネルでメッセージの送信が禁止されるロールを設定できます。  
  
`<role>`にはロールメンション、またはロールIDを指定します。  
```
live restric {add|remove} <role>...
```

### 実況自動終了時間(分)
実況中のチャンネルで一定時間メッセージの送信が無かった場合、
自動で実況を終了する時間(分)を設定できます。  
`0`に設定した場合、機能が無効になります。  
  
`<time>`には半角数字で時間(分)を指定します。  
```
live auto-close <time>
```

### 実況リンクピン止め
実況開始のトリガーになったメッセージの内容は、実況チャンネルにコピーされますが、
これを実況チャンネルにピン止めするか否かを設定できます。  
  
```
live pin-message {enable|disable}
```