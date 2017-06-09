---
title: Activation Events - package.json
MetaDescription: To support lazy activation of Visual Studio Code extensions (plug-ins), your extension controls when it should be loaded through a set of activation events in the package.json extension manifest file.
commitid: 42757495f4d9a4a7a959e45a7eb459c388b04aaf
status: old
---

拡張機能は、それが必要になるまで読み込まれません。その結果、拡張機能をアクティブにする必要があるときVS Codeにコンテキストを提供する必要があります。次のアクティブイベントをサポートしています:

* `onLanguage:${language}`
* `onCommand:${command}`
* `onDebug:${type}`
* `workspaceContains:${toplevelfilename}`
* `*`

また、[`package.json` extension manifest](/docs/extensionapi/extension-manifest.md) の概要と必須フィールドについても説明します。

## activationEvents.onLanguage

任意の拡張子のファイルを開いたときに、拡張機能をアクティベートします。

```json
...
"activationEvents": [
    "onLanguage:python"
]
...
```

## activationEvents.onCommand

コマンドを呼び出したときに、拡張機能をアクティベートします。

```json
...
"activationEvents": [
    "onCommand:extension.sayHello"
]
...
```

## activationEvents.onDebug

デバッグを開始したときに、特定のタイプのデバッグセッションなら拡張機能をアクティベートします。

```json
...
"activationEvents": [
    "onDebug:node"
]
...
```

## activationEvents.workspaceContains

フォルダーを開いたときに、特定のファイルがフォルダーに存在する場合拡張機能をアクティベートします。

```json
...
"activationEvents": [
    "workspaceContains:.editorconfig"
]
...
```

## activationEvents.*

VS Codeを起動したときに、拡張機能をアクティベートします。ユーザーエクスペリエンスを確保するために、他のアクティベーションイベントの組み合わせが使用できない場合にのみで使用してください。

```json
...
"activationEvents": [
    "*"
]
...
```

> **Note:** 拡張機能は複数の活性化イベントを受け入れます。ですから、`"*"`よりも最適な方法が必ずあります。

> **Note:** 拡張機能は、メインモジュールから`activate()`関数をエクスポート**しなければなりません**。これは指定したアクティベーションイベントのいずれかを発行したときVS Codeによって**一度だけ**呼び出されます。また拡張機能は 、VS Codeをシャットダウン時クリーンアップタスクを実行するために、メインモジュールから`deactivate()`関数をエクスポートする**必要**があります。拡張機能はクリーンアッププロセスが非同期の場合、`deactivate()`からPromiseを**返さなければなりません**。クリーンアップを同期して実行している場合、拡張機能は`deactivate()`から`undefined`を返します。

## 次のステップ

VS Codeの拡張モデルの詳細については次のトピックを試してください:

* [Extension Manifest File](/docs/extensionapi/extension-manifest.md) - VS Code package.json extension manifest file reference
* [Contribution Points](/docs/extensionapi/extension-points.md) - VS Code contribution points reference
