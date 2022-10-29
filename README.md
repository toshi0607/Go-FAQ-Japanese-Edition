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
