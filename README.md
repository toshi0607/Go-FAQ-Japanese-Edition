# Go FAQ Japanese Edition

[Frequently Asked Questions (FAQ)](https://go.dev/doc/faq)の日本語版です。

## 目次

- [Go FAQ Japanese Edition](#go-faq-japanese-edition)
  - [目次](#目次)
  - [起源](#起源)
    - [プロジェクトの目的は？](#プロジェクトの目的は)
    - [プロジェクトの歴史は？](#プロジェクトの歴史は)
    - [ゴーファーマスコットの起源は？](#ゴーファーマスコットの起源は)
    - [言語はGoと呼ぶ？それともGolang？](#言語はgoと呼ぶそれともgolang)
    - [なぜ新しい言語を作った？](#なぜ新しい言語を作った)
    - [Goの先祖は？](#goの先祖は)
    - [設計における指針は？](#設計における指針は)
  - [利用状況](#利用状況)
    - [Googleは社内でGoを利用している？](#googleは社内でgoを利用している)
    - [他のGoを利用している企業は？](#他のgoを利用している企業は)
    - [Goのプログラムは、C/C++のプログラムとリンクできる？](#goのプログラムはccのプログラムとリンクできる)
    - [GoをサポートするIDEは？](#goをサポートするideは)
    - [GoはGoogleのプロトコルバッファをサポートしている？](#goはgoogleのプロトコルバッファをサポートしている)
    - [Goのホームページを他の言語に翻訳することはできる？](#goのホームページを他の言語に翻訳することはできる)
  - [設計](#設計)
    - [Goにはランタイムがある？](#goにはランタイムがある)
    - [Unicodeの識別子はどうなっている？](#unicodeの識別子はどうなっている)
    - [GoにはなぜXという機能がない？](#goにはなぜxという機能がない)
    - [Goはいつジェネリック型が使えるようになった？](#goはいつジェネリック型が使えるようになった)
    - [なぜGoは最初ジェネリック型なしでリリースされた？](#なぜgoは最初ジェネリック型なしでリリースされた)
    - [なぜGoには例外処理機構がない？](#なぜgoには例外処理機構がない)
    - [なぜGoにはアサーションがない？](#なぜgoにはアサーションがない)
    - [なぜCSPのアイデアの上に並行処理を構築する？](#なぜcspのアイデアの上に並行処理を構築する)
    - [なぜスレッドではなくゴルーチン？](#なぜスレッドではなくゴルーチン)
    - [なぜマップ演算はアトミックに定義されていない？](#なぜマップ演算はアトミックに定義されていない)
    - [言語の変更提案は受け入れられる？](#言語の変更提案は受け入れられる)
  - [型](#型)
    - [Goはオブジェクト指向の言語？](#goはオブジェクト指向の言語)
    - [メソッドの動的ディスパッチを行うには？](#メソッドの動的ディスパッチを行うには)
    - [なぜ型の継承がない？](#なぜ型の継承がない)
    - [なぜ`len`はメソッドではなく、関数？](#なぜlenはメソッドではなく関数)
    - [なぜGoはメソッドや演算子のオーバーロードをサポートしない？](#なぜgoはメソッドや演算子のオーバーロードをサポートしない)
    - [なぜGoには「implements」宣言がない？](#なぜgoにはimplements宣言がない)
    - [実装した型がインターフェースを満たしていることを保証するには？](#実装した型がインターフェースを満たしていることを保証するには)
    - [なぜT型はEqualインターフェースを満たさない？](#なぜt型はequalインターフェースを満たさない)
    - [[]Tを[]interface{}に変換できる？](#tをinterfaceに変換できる)
    - [T1とT2が同じ基底型を持つとき[]T1を[]T2に変換できる？](#t1とt2が同じ基底型を持つときt1をt2に変換できる)
    - [なぜnilエラー値はnilと等しくない？](#なぜnilエラー値はnilと等しくない)
    - [なぜCのようにタグなしのunionがない？](#なぜcのようにタグなしのunionがない)

## 起源

### プロジェクトの目的は？

Goが誕生したのはたったの10年前ですが、プログラミングの世界は現在と異なっていました。プロダクションソフトウェアは、通常C++かJavaで書かれており、GitHubは存在せず、ほとんどのコンピュータはまだマルチプロセッサではなく、Visual StudioとEclipse以外にIDEやその他のハイレベルなツールはほとんどなく、ましてやインターネット上で無償で利用できるものはほとんどありませんでした。

その一方で、私たちはサーバーソフトウェアの開発に使用する言語が必要以上に複雑であることに不満を感じていました。C、C++、Javaなどの言語が開発されて以来、コンピュータは劇的に速くなりましたが、プログラミング行為自体はそれほど進歩しませんでした。また、マルチプロセッサが一般的になりつつあることは明らかでしたが、ほとんどの言語には、それらで効率的かつ安全にプログラムするためのサポートはほとんどありませんでした。

技術の発展がするにつれて、今後ソフトウェア工学の主要な課題になっていくのは何か、新しい言語はその解決にどう役立てられるかを一歩踏み込んで考えてみることにしました。例えば、マルチコアCPUの台頭により、言語はある種の並行処理や並列処理を第一級にサポートする必要が生じます。また、大規模な並列プログラムにおいてリソース管理をしやすくするために、ガベージコレクションや、少なくともある種の安全な自動メモリ管理が必要とされます。

このような検討から、最初はアイデアと要望のセットとして、次に言語として、Goが生まれるまでの[一連の議論](https://commandcenter.blogspot.com/2017/09/go-ten-years-and-climbing.html)が始まりました。Goは、ツール化、コードフォーマットなどの雑務の自動化、大規模なコードベースでの作業に対する障害の除去など、現役プログラマーの支援に力を入れることを包括的な目標として掲げました。

Goの目標とその達成方法、少なくともそのアプローチについては、[Go at Google: Language Design in the Service of Software Engineering](https://go.dev/talks/2012/splash.article)という記事で、より広範な説明を見ることができます。

### プロジェクトの歴史は？

2007年9月21日、Robert Griesemer、Rob Pike、Ken Thompsonは、新しい言語の目標をホワイトボードに書き始めました。数日のうちに、目標は何かをする計画や中身の名案に落ち着きました。設計は、別の仕事と並行してパートタイムで継続しました。2008年1月までに、Kenはコンパイラに取り掛かり、アウトプットとしてCのコード生成するというアイディアを模索していました。2008年半ばには、その言語はフルタイムのプロジェクトとなり、プロダクションのコンパイラを試すのに十分な水準に達していました。2008年5月、Ian Taylorが独自に、ドラフト仕様を使ってGo向けのGCCフロントエンドの開発を開始しました。2008年後半にはRuss Coxが参画し、言語とライブラリをプロトタイプから実用に耐えるのものにするのをサポートしました。

Goは、2009年11月10日にオープンソースプロジェクトとして公開されました。コミュニティから数え切れないほどの人々がアイデア、議論、コードに貢献してきました。

現在、世界に何百万人ものGoプログラマ（ゴーファー）がおり、日々増えています。Goの成功は、私たちの期待をはるかに超えるものでした。

### ゴーファーマスコットの起源は？

マスコットとロゴは、[Renée French](https://reneefrench.blogspot.com/)（ルネ・フレンチ）がデザインしました。Plan 9のうさぎ、[Glenda](https://9p.io/plan9/glenda.html)もデザインしています。ゴーファーについてのブログ記事では、何年か前に[WFMU](https://wfmu.org/)のTシャツのデザインに使ったものが元になっていると説明されています。ロゴとマスコットは、[クリエイティブ・コモンズ3.0](https://creativecommons.org/licenses/by/3.0/)ライセンスで保護されています。

ゴーファーには、特徴と正しい表現方法を説明した[モデルシート](https://go.dev/doc/gopher/modelsheet.jpg)があります。このモデルシートは、2016年のGopherconでのRenéeによる[講演](https://www.youtube.com/watch?v=4rw_B4yY69k)で初めて公開されたものです。彼には独自の特徴があります。ただのゴーファー（ホリネズミ）ではなく、*Goのゴーファー*なのです。

### 言語はGoと呼ぶ？それともGolang？

この言語はGoと呼ばれています。「golang」というあだ名は、もともとWebサイトがgolang.orgだったからです（当時は.devドメインはありませんでした）。そうは言うものの、多く人がgolangという名前を使っており、ラベルとして便利です。例えば、Twitterのハッシュタグは「#golang」です。それでも言語の名前は、単純にGoです。

余談として、[公式ロゴ](https://go.dev/blog/go-brand)では大文字を2つ並べていますが、言語名はGOではなく、Goです。

### なぜ新しい言語を作った？

Goは、Googleでの仕事において、既存の言語や環境に対する不満から生まれました。プログラミングはあまりにも難しくなっており、言語の選択もその一因でした。効率的なコンパイル、効率的な実行、プログラミングのしやすさからどれかを選ばなければならず、同じ主流な言語ではこの3つすべては得られませんでした。安全性や効率性よりも手軽さを重視するプログラマーは、C++やJavaよりも、PythonやJavaScriptといった動的型付け言語に移っていきました。

このような懸念を抱いていたのは、私たちだけではありませんでした。プログラミング言語に長年大きな変化がありませんでしたが、Goは、Rust、Elixir、Swiftなど、プログラミング言語の開発を活発で主流な分野の地位に再び押し上げた、いくつかの新しい言語の最初の1つでした。

Goは、インタプリタ型の動的型付け言語のプログラミングの容易さと、静的型付けコンパイル言語の効率性と安全性を組み合わせることで、これらの問題に対処しました。また、ネットワークやマルチコアコンピューティングをサポートする現代的な言語であることも目指しました。単一のコンピュータで大きな実行ファイルをビルドするのにかかる時間は、せいぜい数秒です。これらの目標を達成するためには、表現力が豊かで軽量な型システム、並行処理とガベージコレクション、厳格な依存関係の仕様など、多くの言語的な問題に対処する必要がありました。これらは、ライブラリやツールではうまく対応できず、新しい言語が必要とされたのです。

[Go at Google](https://go.dev/talks/2012/splash.article)という記事では、Go言語の設計の背景とモチベーションについて議論し、このFAQで紹介されている多くの回答についてより詳細に説明しています。

### Goの先祖は？

Goは、ほとんどがC言語系（基本構文）で、Pascal/Modula/Oberon系（宣言、パッケージ）からの影響が大きく、さらにNewsqueakやLimbo（並行処理）など、Tony HoareのCSPに影響を受けた言語からのアイデアも含まれています。しかし、全面的に新しい言語です。あらゆる面で、プログラマが何をするのか、どうすればプログラミング（少なくとも私たちが行うようなプログラミング）をより効果的に、つまりより楽しくできるのかを考えて設計された言語なのです。

### 設計における指針は？

Goが設計された当時、少なくともGoogleでは、サーバを書くのにJavaとC++が最もよく使われていた言語でした。私たちは、これらの言語では簿記のような記述と繰り返しが多すぎると感じていました。プログラマーの中には、効率と型安全性を犠牲にして、Pythonのようなより動的で流動性な言語へと移行した人もいました。私たちは、効率と安全性と流動性を一つの言語で実現できるはずだと考えました。

Goは、どちらの意味でもタイピングの量を減らすことを試みています。設計全体を通して、私たちは煩雑さと複雑さを減らすように努めました。前方宣言やヘッダーファイルはなく、すべてが一度だけ宣言されます。初期化は表現力豊かで、自動的で、簡単に使えます。文法はすっきりしており、キーワードも少ないです。繰り返し（`foo.Foo* myFoo = new(foo.Foo)`）も、`:=` 宣言・初期化構造を使ったシンプルな型派生によって軽減されています。そして、おそらく最も革新的なのは、型の階層がないことです。型はただ存在するだけで、その関係を表明する必要はありません。これらの単純化により、Goは洗練さを犠牲にすることなく、表現力豊かでありながら理解しやすいものとなっています。

もう一つの重要な原則は、概念の直行性を維持することです。メソッドは任意の型に実装できる、構造体はデータを表し、インターフェースは抽象化を表す、などです。直交性を保つことで、物事が組み合わさったときに何が起こるかを理解しやすくなります。

## 利用状況

### Googleは社内でGoを利用している？

利用しています。GoはGoogleの内部の製品で広く使われています。簡単な例は、golang.orgのサーバーです。これは、[Google App Engine](https://cloud.google.com/appengine/docs)上の本番構成で動作するgodocドキュメントサーバーにすぎません。

もっと重要な例は、Googleのダウンロードサーバー（dl.google.com）で、Chromeバイナリや、apt-getパッケージのような大規模なインストールファイルを配信しているというものです。

GoはGoogleで使用される唯一の言語ではありませんし、他にもたくさんの言語を使用しています。しかし、サイト信頼性エンジニアリング（SRE）や大規模データ処理など、多くの分野で重要な言語となっています。

### 他のGoを利用している企業は？

Goの利用は世界中で増加しており、特にクラウドコンピューティングの領域で顕著です。Goで書かれた主要なクラウドインフラプロジェクトには、DockerとKubernetesがありますが、他にもたくさんあります。

クラウドだけではありません。Go Wikiには定期的に更新される[ページ](https://github.com/golang/go/wiki/GoUsers)があり、Goを利用している多くの企業のうちの一部のリストが掲載されています。

また、Wikiには、この言語を使っている企業やプロジェクトの[成功事例](https://github.com/golang/go/wiki/SuccessStories)へのリンクページがあります。

### Goのプログラムは、C/C++のプログラムとリンクできる？

CとGoを同一アドレス空間で一緒に使うことは可能ですが、自然な形ではなく、インターフェースとなる特別なソフトウェアが必要になることがあります。また、C言語とGoのコードをリンクすると、Goが提供するメモリ安全性とスタック管理特性が失われます。問題を解決するためにCライブラリを使用することが絶対に必要な場合がありますが、純粋なGoコードにはないリスク要素が常に発生するため、注意して行ってください。

GoでCを使用する必要がある場合、進め方はGoコンパイラの実装に依存します。GoチームがサポートしているGoコンパイラの実装は3つあります。デフォルトのコンパイラーである`gc`、GCCバックエンドを使用する `gccgo`、そしてLLVMインフラストラクチャを使用する、やや成熟度の低い`gollvm`です。

`gc`は、Cとは異なる呼び出し規則とリンカを使用しているため、Cプログラムから直接呼び出すことはできませんし、その逆も同様です。`cgo`プログラムは、GoコードからCライブラリを安全に呼び出せるようにするための「他言語関数インターフェース」のメカニズムを提供します。SWIGは、この機能をC++ライブラリにも拡張しています。

`cgo`とSWIGを`Gccgo`と`gollvm`と一緒に使うこともできます。これらのコンパイラは伝統的なAPIを使っているので、これらのコンパイラのコードを GCC/LLVM でコンパイルされたCやC++プログラムと直接リンクすることも、細心の注意を払えば可能です。しかし、安全にそうするには、関係するすべての言語の呼び出し規約を理解することと、GoからCやC++を呼び出すときのスタックの制限に気を配ることが必要です。

### GoをサポートするIDEは？

GoプロジェクトにはカスタムIDEはありませんが、言語とライブラリはソースコードの解析が容易になるように設計されています。その結果、ほとんどの有名なエディタとIDEは、直接またはプラグインを通じて、Goを十分にサポートしています。

Goをサポートしている有名なIDEやエディタには、Emacs、Vim、VS Code、Atom、Eclipse、Sublime Text、IntelliJ（GoLandというカスタム版を通して）、その他多数が含まれます。あなたのお気に入りの環境は、Goでプログラミングするのに生産的なものである可能性が高いです。

### GoはGoogleのプロトコルバッファをサポートしている？

必要なコンパイラプラグインやライブラリは、別のオープンソースプロジェクトが提供しています。[github.com/golang/protobuf/](https://github.com/golang/protobuf) で公開されています。

### Goのホームページを他の言語に翻訳することはできる？

もちろんです。私たちは、開発者が自分の言語でGo言語サイトを作成することを推奨しています。ただし、Googleのロゴやブランドをサイトに追加する場合は（[go.dev](https://go.dev/)には表示されていません）、[about.google/brand-resource-center/](https://about.google/brand-resource-center/) にあるガイドラインを遵守してください。

## 設計

### Goにはランタイムがある？

Goには*runtime*と呼ばれる広範なライブラリがあり、すべてのGoプログラムの一部となっています。ランタイムライブラリは、ガベージコレクション、並行処理、スタック管理、Go言語のその他の重要な機能を実装しています。ランタイムは言語の中心的な存在ですが、GoのランタイムはCのライブラリである`libc`に準じています。

しかし、Goのランタイムには、Javaランタイムが提供するような仮想マシンは含まれていないことを理解することが重要です。Goのプログラムは事前にネイティブのマシンコードにコンパイルされます（別実装ではJavaScriptやWebAssemblyにコンパイルされます）。したがって、「ランタイム」という言葉はプログラムが実行される仮想環境を表すためによく使われますが、Goでは重要な言語サービスを提供するライブラリにつけられた名前にすぎません。

### Unicodeの識別子はどうなっている？

Goを設計する際、ASCIIに過度に依存しないようにしたいと考えました。つまり、7ビットASCIIの制約から識別子の空間を拡張するということです。識別子文字はUnicodeで定義された文字か数字でなければならないというGoのルールは、理解も実装も簡単ですが制約があります。例えば、結合文字は設計上除外されており、デーヴァナーガリーなど一部の言語は除外されています。

このルールには、もう一つ残念な結果があります。エクスポートされる識別子は大文字で始まらなければならないので、ある言語の文字から作られた識別子は、定義上エクスポートすることができないのです。今のところ、`X日本語`のようなものを使うのが唯一の解決策ですが、明らかに満足できるものではありません。

Goの初期のバージョンから、他の言語を使用するプログラマに配慮し、識別子空間をどのように拡張するのがベストなのかかなり検討されてきました。まさにまだ議論の余地があり、将来のバージョンでは識別子の定義がより自由になるかもしれません。例えば、Unicodeが[推奨する](http://unicode.org/reports/tr31/)識別子の考え方を採用することも考えられます。いずれにしても、Goの人気のある特徴の1つである、識別子の可視性を文字の大小で決定する方法を維持（あるいは拡張）しながら、互換性を保つようにする必要があります。

現時点では、プログラムを壊さずに後から拡張できるシンプルなルールを採用しています。それにより、曖昧な識別子を認めるルールであれば確実に発生してしまうバグを回避することができます。

### GoにはなぜXという機能がない？

どの言語にも目新しい機能があり、誰かが好きな機能は省かれています。Goは、プログラミングのしやすさ、コンパイルの速さ、概念の直交性、並行処理やガベージコレクションなどの機能をサポートする必要性を大事にして設計されています。あなたの好きな機能は、コンパイルの速度や設計の明快さに影響するため、あるいは基本的なシステムモデルを難しくしすぎるため、省かれているかもしれません。

Goに機能*X*がないことが気に入らない場合、私たちを許してGoにある機能を調査してみてください。*X*がないのを面白い方法で補っていることに気づくかもしれません。

### Goはいつジェネリック型が使えるようになった？

Go 1.18リリースでは、言語に型パラメータが追加されました。これにより、ポリモーフィックやジェネリックプログラミングの一種が可能になります。詳しくは、[言語仕様](https://go.dev/ref/spec)と[提案](https://go.googlesource.com/proposal/+/master/design/43651-type-parameters.md)をご覧ください。

### なぜGoは最初ジェネリック型なしでリリースされた？

Goは、長期にわたって保守しやすいサーバプログラムを書くための言語として設計されました（背景はこの[記事](https://go.dev/talks/2012/splash.article)を参照）。設計では、スケーラビリティ、可読性、並行性などに重点が置かれました。ポリモーフィックプログラミングは当時、この言語の目標に不可欠とされませんでした。そのため、最初はシンプルさを守るために省かれたのです。

ジェネリックは便利ですが、型システムおよびランタイムの複雑さという代償を伴います。複雑さに比例した価値を与えてくれると信じられる構想を練るのに時間がかかりました。

### なぜGoには例外処理機構がない？

`try-catch-finally`イディオムのように例外を制御構造に結びつけると、コードが複雑になると考えています。また、ファイルを開けなかったというような普通のエラーを例外として扱うようプログラマに促す傾向があります。

Goは異なるアプローチを取ります。単純なエラー処理では、Goの複数値の戻り値によって、戻り値をオーバーロードせずにエラーを報告することが簡単にできます。[Goの標準的なエラー型を利用すると、他の機能と相まって](https://go.dev/blog/error-handling-and-go)、エラー処理は快適に行えますが他の言語での処理とはかなり異なっています。

Goには、本当に例外的な状態を通知し、そこから回復するための組み込み関数もいくつかあります。回復機構は、エラー後に関数の状態が破棄される際にのみ実行されます。これは大惨事を処理するには十分ですが、余分な制御構造は必要なく、うまく使えばきれいなエラー処理コードになります。

詳しくは、[Defer, Panic, and Recover](https://go.dev/blog/defer-panic-and-recover)という記事をご覧ください。また、[Errors are values](https://go.dev/blog/errors-are-values)というブログ記事では、エラー処理にGoの力が遺憾なく発揮されていることを示し、Goできれいにエラー処理するためのアプローチを説明しています。エラーは単なる値なのです。

### なぜGoにはアサーションがない？

Goはアサーションを提供しません。アサーションは紛れもなく便利ですが、私たちの経験では、プログラマは適切なエラー処理とレポートを考えるのを避けるために、それを松葉杖として使っています。適切なエラー処理とは、致命的でないエラーが発生しても、サーバーがクラッシュせずに動作を継続することです。適切なエラー報告とは、エラーが直接的で的確であることを意味し、プログラマは膨大なクラッシュトレースを解釈する手間が省けます。プログラマーがコードに精通していない場合、正確なエラーは特に重要です。

私たちは、これが争点になることを理解しています。Go言語とライブラリには、現代の慣行とは異なるものがたくさんあります。それは単に、異なるアプローチを試してみる価値があると感じたからです。

### なぜCSPのアイデアの上に並行処理を構築する？

並行処理とマルチスレッドプログラミングは、長い間、難しいという評価を受け続けてきました。これは、pthreadsのような複雑な設計や、ミューテックス、条件変数、メモリバリアなどの低レベルの詳細が過度に強調されていることが原因だと考えています。高レベルのインタフェースがあることで、たとえその下にまだミューテックスなどがあるとしても、 よりシンプルなコードになります。

並行処理のための高レベルの言語サポートを提供する最も成功したモデルの1つは、HoareのCommunicating Sequential Processes（CSP）に由来します。OccamとErlangは、CSPから派生した2つの有名な言語です。Goの並行処理プリミティブはHoareのCSPから派生したもので、主な成果はチャンネルをファーストクラスのオブジェクトとして扱うという強力な概念です。以前のいくつかの言語での経験から、CSPモデルは手続き型言語のフレームワークにうまく当てはまることが分かっています。

### なぜスレッドではなくゴルーチン？

ゴルーチンは、並行処理を簡単にするためのものです。このアイデアは以前からあり、独立して実行される関数（コルーチン）をスレッドの集合に多重化することです。コルーチンがブロッキングシステムコールを呼び出すなどしてブロックされると、ランタイムは自動的に同じOSスレッド上の他のコルーチンを別の実行可能なスレッドに移動させ、ブロックされないようにします。プログラマーにはこのようなことには気づかず、それが重要な点です。その結果としてのゴルーチンはとても安価です。スタック用のメモリ（数キロバイト）以上のオーバーヘッドはほとんどありません。

スタックを小さくするために、Goのランタイムはサイズ変更可能で境界のあるスタックを使用します。新しく作成されたゴルーチンには数キロバイトが与えられますが、これはほとんど常に十分な量です。足りないときは、ランタイムがスタックを格納するメモリを自動的に拡大（と縮小）させるので、多くのゴルーチンが適度な量のメモリで生存できるようになります。CPUのオーバーヘッドは、関数呼び出し1回につき平均して3個程度の安い命令です。同じアドレス空間に何十万ものゴルーチンを作ることは実務上可能です。もしゴルーチンが単なるスレッドだったら、もっと少ない数でシステムリソースが枯渇してしまうでしょう。

### なぜマップ演算はアトミックに定義されていない？

長い議論の末、マップの典型的な使い方では複数のゴルーチンから安全にアクセスする必要はなく、アクセスする場合でも、マップはすでに同期されている大きなデータ構造または計算の一部である可能性が高いと判断されました。そのため、すべてのマップ操作にミューテックス取得を要求すると、ほとんどのプログラムの速度を低下させ、安全性にはほとんど寄与しません。しかし、これは制御不能なマップアクセスがプログラムをクラッシュさせる可能性があることを意味するので、簡単な決定ではありませんでした。

Goはアトミックなマップ更新を排除しているわけではありません。信頼されていないプログラムをホストする場合など、必要であれば、実装はマップアクセスをインターロックすることができます。

マップへのアクセスが安全でないのは、更新時のみです。すべてのゴルーチンがマップの要素を読み取るだけ（for range ループを使用してマップをイテレーションすることを含め、マップの要素を参照する）だけで、要素への割当や削除によってマップを変更しなければ、同期せずに同時にマップにアクセスしても安全です。

マップを正しく使用するための補助として、Goのいくつかの実装には、並行実行によってマップが安全でない方法で変更された場合に、実行時に自動的に報告する特別なチェック機能があります。

### 言語の変更提案は受け入れられる？

Goの改善はよく提案され、そういった議論の歴史は[メーリングリスト](https://groups.google.com/group/golang-nuts)で確認できます。しかし、それらの変更はほとんど受け入れられてきませんでした。

Goはオープンソースのプロジェクトですが、言語とライブラリは、少なくともソースコードレベルで、既存のプログラムを壊すような変更を防ぐ[互換性の約束](https://go.dev/doc/go1compat)によって守られています（最新の状態に保つために、プログラムは時々再コンパイルする必要があるかもしれません）。提案がGo 1の仕様に違反する場合、その利点にかかわらず、そのアイデアを受け入れられません。将来のメジャーリリースは、Go 1と互換性がないかもしれませんが、このトピックに関する議論は始まったばかりです。1つ確かなことは、その過程で非互換性が生じることはほとんどないということです。さらに、互換性の約束は、そのような状況が発生した場合に古いプログラムが自動で適応する手段を提供することを後押ししてくれます。

変更提案がGo 1の仕様と互換性があったとしても、Goの設計目標の精神にはそぐわないかもしれません。[Go at Google: Language Design in the Service of Software Engineering](https://go.dev/talks/2012/splash.article)という記事では、Goの起源とその設計の動機を説明しています。

## 型

### Goはオブジェクト指向の言語？

イエスでもありノーでもあります。Goには型とメソッドがあり、オブジェクト指向のプログラミングが可能ですが、型の階層はありません。Goの「インターフェース」の概念は、使いやすく、ある意味より一般的だと思われる別のアプローチを提供します。また、型を他の型に埋め込むこともでき、サブクラス化と似ているが同一ではないものを提供します。さらに、GoのメソッドはC++やJavaよりも一般的で、あらゆる種類のデータに対して定義することができ、「ボックス化されていない」整数のような組み込み型に対しても可能です。メソッドは構造体（クラス）に限定されるものではありません。

また、型階層がないため、Goの「オブジェクト」は、C++やJavaなどの言語よりもずっと軽量に感じられます。

### メソッドの動的ディスパッチを行うには？

動的にディスパッチされるメソッドを持つ唯一の方法は、インターフェースを介することです。構造体やその他の具象型に対するメソッドは、常に静的に解決されます。

### なぜ型の継承がない？

オブジェクト指向プログラミングは、少なくとも最もよく知られた言語では、型と型の間の関係についてあまりに多くの議論を必要とし、その関係が自動的に導き出されることがよくあります。Goは異なるアプローチを取ります。

Goでは、2つの型が関連していることをプログラマーが前もって宣言するのではなく、型のもつメソッドのサブセットを指定するインターフェースが自動的に満たされます。このアプローチには、帳簿をつける手間を省けるだけでなく、実際の利点もあります。型は一度に複数のインターフェースを満たすことができ、従来の多重継承のような複雑なことはありません。インターフェースは非常に軽量です。メソッドが1つのインターフェースでも、メソッドがないインターフェースでさえも、役立つ概念を表現できます。新しいアイデアやテストのために、元の型にアノテーションつけることなく、後からインターフェースを追加することができます。型とインターフェースの間には明示的な関係がないので、型階層を管理したり、議論したりする必要はありません。

これらのアイデアを利用して、型安全なUnixパイプに類似したものを構築することが可能です。例えば、`fmt.Fprintf`がファイルだけでなくあらゆる出力に対してフォーマットされたプリントを可能にする方法、`bufio`パッケージがファイルI/Oから完全に分離できる方法、`image`パッケージが圧縮画像ファイルを生成する方法などをご覧ください。これらのアイデアはすべて、単一のメソッド（`Write`）を表す単一のインターフェース（`io.Writer`）に由来しています。そして、これはほんの一部に過ぎません。Goのインターフェースは、プログラムがどのように構造化されるかに大きな影響を及ぼします。

慣れるまで少し時間がかかりますが、この暗黙の型依存のスタイルは、Goの最も生産的なものの1つです。

### なぜ`len`はメソッドではなく、関数？

私たちはこの問題について議論しましたが、`len`とその仲間を関数として実装することは実際に問題はなく、基本型のインターフェース（Goの型の意味で）についての質問を複雑にすることもないと判断しました。

### なぜGoはメソッドや演算子のオーバーロードをサポートしない？

型マッチングも行う必要なければ、メソッドディスパッチは単純化されます。他の言語での経験から、同じ名前でシグネチャが異なるさまざまなメソッドがあると便利なこともありますが、実際には混乱しやすく壊れやすいということがわかりました。名前だけでマッチングし、型における一貫性を要求することは、Goの型システムにおける主要な単純化の決定でした。

演算子のオーバーロードについては、絶対条件というより、利便性の方が高いように思います。繰り返しになりますが、演算子のオーバーロードはないほうがシンプルです。

### なぜGoには「implements」宣言がない？

Goの型は、インターフェースのメソッドを実装するだけでそのインターフェースを満たします。この特性により、既存のコードを変更することなくインターフェースを定義し使用することができます。[構造的な型付け](https://en.wikipedia.org/wiki/Structural_type_system)が可能になるので、関心事の分離が促進され、コードの再利用が向上し、コードが増えるにつれて出現するパターンに基づいて構築することが容易になります。インターフェースのセマンティクスは、Goの軽快さ、軽量さの主な理由の一つです。

詳しくは、[型の継承に関する質問](#なぜ型の継承がない)をご覧ください。

### 実装した型がインターフェースを満たしていることを保証するには？

型`T`がインターフェース`I`を実装しているかどうかは、`T`のゼロ値や`T`へのポインタを適宜使って代入を試みることでコンパイラに確認させることができます。

```go
type T struct{}
var _ I = T{}       // 型TがインターフェースIを実装していることの確認
var _ I = (*T)(nil) // 型*TがインターフェースIを実装していることの確認
```

`T`（または`*T`）が`I`を実装していない場合、その間違いはコンパイル時に検出されます。

あるインターフェースのユーザがそのインターフェースを実装していることを明示的に宣言したい場合、説明的な名前のメソッドをインターフェースのメソッドセットに追加することができます。

例:

```go
type Fooer interface {
    Foo()
    ImplementsFooer()
}
```

型が`Fooer`であるためには、`ImplementsFooer`メソッドを実装し、[go doc](https://pkg.go.dev/cmd/go#hdr-Show_documentation_for_package_or_symbol)の出力でその事実を明確に文書化し、アナウンスする必要があります。

```go
type Bar struct{}
func (b Bar) ImplementsFooer() {}
func (b Bar) Foo() {}
```

ほとんどのコードはこのような制約を利用しません。なぜなら、このような制約はインターフェースのアイデアの有用性を制限してしまうからです。しかし、類似したインターフェース間の曖昧さを解消するために制約が必要になることもあります。

### なぜT型はEqualインターフェースを満たさない？

自分自身と他の値を比較することができるオブジェクトを表現する簡単なインターフェースを考えてみましょう。

```go
type Equaler interface {
    Equal(Equaler) bool
}
```

そしてこれがT型とします。

```go
type T int
func (t T) Equal(u T) bool { return t == u } // does not satisfy Equaler
```

いくつかの多相型システムにおける同様の状況とは異なり、`T`は`Equaler`を実装していません。`T.Equal`の引数の型は`T`であり、文字通り必須の型である`Equaler`ではありません。

Goでは、型システムは`Equal`の引数を積極的にはサポートしません。`Equaler`を実装している`T2`型が示すように、これはプログラマの責任です。

```go
type T2 int
func (t T2) Equal(u Equaler) bool { return t == u.(T2) }  // satisfies Equaler
```

これは他の型システムとは異なります。Goでは、`Equaler`を満たすあらゆる型が`T2.Equal`の引数として渡され、実行時にその引数が`T2`型であることをチェックしなければならないためです。言語によっては、コンパイル時にその保証をするようにアレンジしているものもあります。言語によっては、コンパイル時にその保証をするように取り計らっているものもあります。

関連する例として、逆のケースもあります。

```go
type Opener interface {
   Open() Reader
}

func (t T3) Open() *os.File
```

他の言語では満たすかもしれませんが、Goでは`T3`は`Opener`を満たしません。

このような場合、Goの型システムはプログラマにとってあまり多くをサポートしてくれないのは事実です。しかし、サブタイピングがないため、インターフェースの充足性に関するルールはつぎのように非常に簡単に記述できます。関数の名前とシグネチャはインターフェースのものと全く同じか？また、Goのルールは効率的に実装するのが簡単です。これらの利点は、自動的な型の上位変換（type promotion）がないことを補って余りあるものだと感じています。いつかGoが何らかの多相型付けを採用する日が来れば、これらの例のような考えを表現し、かつ静的にチェックする方法があると思われます。

### []Tを[]interface{}に変換できる？

直接はできません。この2つの型はメモリ上で同じ表現を持っていないため、言語仕様で禁止されています。変換先のスライスに個別に要素をコピーする必要があります。この例では、`int`のスライスを`interface{}`のスライスに変換しています。

```go
t := []int{1, 2, 3, 4}
s := make([]interface{}, len(t))
for i, v := range t {
    s[i] = v
}
```

### T1とT2が同じ基底型を持つとき[]T1を[]T2に変換できる？

このコードサンプルの最後の行は、コンパイルできません。

```go
type T1 int
type T2 int
var t1 T1
var x = T2(t1) // OK
var st1 []T1
var sx = ([]T2)(st1) // NOT OK
```

Goでは、型はメソッドと密接に結びついており、名前のついた型はすべて（おそらく空の）メソッドセットを持っています。原則的には、変換される型の名前は変更できますが（したがって、そのメソッドセットも変更できます）、複合型の要素の名前（とメソッドセット）は変更できません。Goでは、型の変換について明示的である必要があります。

### なぜnilエラー値はnilと等しくない？

内部的には、インターフェースは`T`型と値`V`の2つの要素で実装されています。`V`は`int`、構造体、ポインタなどの具体的な値であり、決してインターフェースそのものではありません。また、`T`型を持ちます。例えば、あるインターフェースに`int`型の値3を格納すると、できあがるインターフェースの値は、模式的に、（`T=int`, `V=3`）となります。あるインターフェース変数がプログラムの実行中に異なる値`V`（とそれに対応する型`T`）を保持する可能性があるため、値`V`はインターフェースの動的値とも呼ばれます。

インターフェースの値が`nil`であるのは、`V`と`T`がともに未設定である場合（`T=nil`で`V`は未設定）だけです。特に、`nil`インターフェースは常に`nil`型を保持することになります。`int`型の`nil`ポインタをインターフェース値の内部に格納すると、ポインタの値に関係なく内部の型は`*int`になります (`T=*int`、`V=nil`)。したがって、このようなインターフェース値は、*内部のポインタ値`V`が`nil`であっても*、非`nil`になります。

この状況は紛らわしいです。エラーリターンなど、インターフェース値の内部にnil値が格納されている場合に発生します。

```go
func returnsError() error {
    var p *MyError = nil
    if bad() {
        p = ErrBad
    }
    return p // Will always return a non-nil error.
}
```

エラーを返す関数では、エラーが正しく作成されることを保証するために、`*MyError`のような具象型ではなく、（上で行ったように）常に`error`型をそのシグネチャで使用することは良いアイデアです。例として、`os.Open`は、`nil`でない場合常に具象型`*os.PathError`であるにもかかわらず、`error`を返します。

ここで説明したのと同じような状況は、インターフェースを使うときにはいつでも起こり得ます。ただ、インターフェースに具体的な値が格納されている場合、インターフェースは`nil`にならないことを覚えておいてください。詳しくは、「[The Laws of Reflection](https://go.dev/blog/laws-of-reflection)」を参照してください。

### なぜCのようにタグなしのunionがない？

タグなしのunionは、Goのメモリ安全保証に違反します。
