# TensorFlowSharp for VisualStudio2010

本レポジトリは [TensorFlowSharp](https://github.com/migueldeicaza/TensorFlowSharp) を部分的に Fork して .NetFramework4 までしか対応していない VisualStudio 2010 でビルド可能なように修正し、VS2010用の .sln と .csproj を加えたものです。アセンブリ名は `TensorFlowSharpNet40.dll` としています。

[ValueTuple 4.4.0](https://www.nuget.org/packages/System.ValueTuple/4.4.0) に依存しているため、実行に .NetFramework 4.6.1 以上が必要な点は変わりません。

基本的にロジック変更しておらず、学習済モデルをロードして予測値を出力する程度の動作は確認しましたが、動作保証はできません。そもそも需要がないと思いますが自己責任で使用してください。

## 変更点

C# 6 や 7 で追加された構文を C# 4 向けに書き直すという不毛な内容です。
1. タプル構文を明示的に ValueTuple型を指定するよう書き換え
1. ValueTuple を戻り値とするメソッドには [TupleElementNames] 属性を追記
1. ラムダ式のメソッドやプロパティをブロック構文の記述に書き換え
1. 自動プロパティの初期化子をコンストラクタでの初期化に変更
1. 文字列補完式を String.Format に書き換え
1. nameof 演算子をコメントアウトしてパラメータをダブルクォートで括って文字列化
1. その他細かなエラー除去

## ビルド手順

VisualStudio2010 にインストールできる [NuGet パッケージ マネージャー](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) では ValueTuple や TensorFlowSharp の NuGet パッケージをインストールできないため、NuGet.CommandLine を入れてコマンドからパッケージを復元します。

1. VisualStudio2010 の `ツール`>`拡張機能マネージャー` から NuGet パッケージ マネージャー をインストール
1. `TensorFlorSharpNet40.sln` を開き、NuGet パッケージ マネージャー から `NuGet.CommandLine` をインストール
1. コマンドプロンプトを開き、ValueTuple と TensorFlowSharp のパッケージを復元
    ```
    > cd [TensorFlowSharpNet40.sln のあるフォルダ]
    > packages\NuGet.CommandLine.4.7.1\tools\NuGet.exe restore
    ```
1. ソリューションをビルド

## License

[本家の License](https://github.com/migueldeicaza/TensorFlowSharp/blob/master/LICENSE)（MIT）に準拠します。
