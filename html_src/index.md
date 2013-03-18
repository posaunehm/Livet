---
layout: layout
title: Livet
---


#Livet

![image](http://ugaya40.net/wp-content/uploads/LivetLogo_thumb.png)

##What's Livet?
Livet is a MVVM (Model-View-ViewModel) infrastructure for WPF4/4.5 running on .NET Framework 4(Client Profile) or higher. distributed under [zlib/libpng license](http://opensource.org/licenses/Zlib). 

##Installation
Livet provides project templates, item templates and code snippets for Visual Studio 2010/2012 as well as Livet main binary. You can install all of them via Visual Studio Extension Manager.

![image](http://ugaya40.net/wp-content/uploads/image_thumb1.png)

Or you can install via Nuget.

	PM> Install-Package LivetCask

However, Nuget package contains main binary only. Templates and snippets are also key components for the productivity of Livet, so we strongry recommend to use Extension Manager. 


> If you use Express Edition(VS2010/2012), you can install Livet using [msi installer](http://visualstudiogallery.msdn.microsoft.com/ee198b62-fa45-496c-9c1c-e8f63b43f677?SRC=VSIDE), instead of Extension Manager.

##Features

### 1. Tool Support
Livet greatly enhances Visual Studio and Blend.

#### Visual Studio 2010/2012 Support

<!--WPFでは、プロジェクトの初期設定のコストも馬鹿になりません。また、ビヘイビア・トリガー・アクションの開発にも高いコストがかかります。-->

In WPF Projects, it's very messy procedure to cofigure project settings, as well as to Behaviors, Triggers, and Actions.

<!--
Livetではプロジェクトテンプレート・アイテムテンプレートはもちろんの事、コードスニペットにて各種Commad、変更通知プロパティを提供しています。-->
<!--
※コードスニペットのガイドは、プロジェクトテンプレート・アイテムテンプレートにあります)-->

Livet make them much easier to provide project templates, and item templates. In addition, Livet also provides useful code snnipets for Commands and Notification Properties. (Snnipet documentations are included in templates.)




#### Blendable(Blend Support)

<!--LivetのView機能は極力Blendで作業しやすくなるように定義されています。
-->

Every view-support function is designed with usability on Blend. So you can use Livet functions very naturally on Blend.

### 2. View Support

Livet has a very simple principle on view support functions; *To Make Unbindable bindable.* Thats it.

For view support libraries on XAML platform, not limited in WPF or MVVM, can do only two things; "expanding or supplementing control functionality" and "enabling to add more functions for binding". Since Livet is not a control library but a MVVM infrastructure, it's very natural focusing the principle, "To Make Unbindable Bindable".

<!--
Livetの特徴② – View Support
LivetのViewサポートの方針は簡単です。「バインドで解決できる箇所を増やす」- これのみです。

WPFに限らずMVVMに限らずXAML系プラットフォームの特徴を活かしたViewサポートライブラリに出来る事はもともと基本的に「Viewコントロールの機能の補完」と「バインドで解決できる場所を増やす」のみです。LivetはMVVMインフラストラクチャですから「バインドで解決できる箇所を増やす」に注力するのは至極当然と言えます。-->

#### Make "Unbindable" Properties Bindable

<!--コントロールのバインドできないプロパティ(依存関係プロパティではないプロパティ)の存在がViewModelでのViewの状態管理を苦しくする事は少なくありません。Livetではすべてのコントロールの、全ての(System.Windowsで始まる型のプロパティは除く)依存関係プロパティではないプロパティの単方向のバインドを可能にするビヘイビアとアクションを提供しています。

xxxSetStateToSourceAction (xxxコントロールからバインドソースへ値を送信)



xxxSetStateToControlBehavior (バインドソースからxxxコントロールへ値を送信)



また、TextBoxとPasswordBoxに限っては本来バインドできないプロパティを双方向バインド可能にするビヘイビアを別途用意してあります。(TextBoxBindingSupportBehavior/PasswordBoxBindingSupportBehavior)。
-->

#### Command-Less ViewModel - Direct Method Binding

<!--一般的なMVVMのサンプルとされるコードでViewからViewModelに操作を要求したい時にICommandを介するのは何故か？。

Viewの抽象化要件の上ではICommandはViewModelで意味的な操作の塊を提示するという意義があります。しかし多くの場合Viewの抽象要件は不要です。Viewの抽象化要件がなく、Modelが十分にリッチでViewModelが適切な厚さを持っている場合、ICommandはただメソッドを直接バインドできないがために存在します。

その状況(つまり多くの状況)でMVVMを適切に考慮すれば、それはむしろICommandを使わない事になるはずです。

LivetではICommandをサポートするすべてのView機能が同時にメソッドの直接バインディングをサポートしています。

代表的なそれはLivetCallMethodActionです。BlendSDKのCallMethodActionは引数はとれませんが、LivetCallMethodActionは一つの引数を取れ(ICommandと同条件)、なおかつBlendSDKのCallMethodActionより高いパフォーマンスを誇ります。

LivetCallMethodAction



後述するメッセージ機構も含めてLivetにおいてはすべてのICommandを要求するような機能が同時にメソッドの直接バインディングをサポートしていますし、開発者が独自にビヘイビア・トリガー・アクションを作成する際もメソッドの直接バインディングが簡単に実装できるようにMethodBinderという機構を用意してあります。

MethodBinderはLivetのすべてのメソッドバインディング機能で使用されています。MethodBinderをシンプルに使用するだけで、内部ではリフレクションと式木をフル活用して最大限メソッドキャッシュ管理の効率化をしてくれます。-->

#### Message Triggerable Action

<!--Livet.Behaviors.Messaging名前空間にはメッセージを受け取る事の出来るActionが用意されています。メッセージを受け取るActionは汎用性が高く、View上でEventTriggerなどから通常通りActionを起動する事も、ViewModel上のMessengerからMessageを送信して起動する事もできます。また戻り値のあるメッセージに対応したActionでは、Actionの結果が格納されたメッセージを引数にViewModelのメソッドやコマンドを呼び出すこともできます。

PrismのInteractionRequestと似た機構ですが、決定的に異なるのはメッセージをView上でも定義可能なところとコールバックをコマンド呼び出しだけではなくメソッドでも可能な所です。View上でメッセージが定義できる事で実装上の制約からくるViewとViewModel間の不要な通信を抑える事ができます。

メッセージを受け取るアクションは、通常通りのアクションとして使う事も、ViewModel→View方向の通知手段として使う事も出来ます。

Clickイベントを切っ掛けに確認ダイアログを呼び出し、結果をViewModelのRequestCloseメソッドを呼び出すことで通知



ViewModelのMessengerから”Info”というキーでメッセージが飛んできた場合、情報ダイアログを表示

View側



ViewModel側



Livetに標準で定義されているメッセージとアクションの組み合わせには、確認・情報ダイアログ・ファイルダイアログ・画面遷移・フォルダーダイアログ(Windows API Code Packを参照しているためLivet.Extensionsという別アセンブリに定義)などがあります。

Livet.Extensionsのフォルダー選択メッセージとアクションは、Vista以前と以降でTaskDialogとFolderBrowserDialogを自動で切り替えて使用できる



また、開発者が簡単にメッセージ対応アクション・メッセージを定義できるように、アイテムテンプレートに相互作用アクションとメッセージのテンプレートをそれぞれ用意してあります。-->

#### Generic EnumToBooleanConverter
<!--
View抽象化要件がない場合、Converterを使わなければならない箇所は限られては来ますが、しかしそれでもViewModelの使いまわしをしたい等の場合にIValueConverterを必要とする場合があります。LivetではSystem.Windows名前空間配下の全てのEnum型をbooleanと相互変換するIValueConverterを用意してあります。-->



#### Miscellaneous 
<!--Blend SDKのDataTriggerは初期値に対応していません。その対処として初期値に対応するLivetDataTrigger、フォーカスを制御するSetFocusAction、Windowのクローズキャンセルや、クローズキャンセル可否判断をViewModelに委譲する事が出来るWindowCloseCancelBehavior、RoutedEventTrigger、DataContextがIDisposableであった場合DataContextをDisposeするDataContextDisposeActionなどを用意してあります。-->

### 3. ViewModel Support

<!--LivetのViewModelサポート機能は、ViewとModelを極力PDSにそってデザインした場合に必然的に薄くなるViewModel、そしてその薄くなったViewModelが多くの開発シナリオで多用するであろう機能を前提にデザインしてあります。-->

#### Messenger and CompositeDisposable

<!--Messengerは前述のView機能 – メッセージを受け取るアクションに、ViewModelからメッセージを伝えるために用意されています。CompositeDisposableはIEnumerable<IDisposable>型で、ViewModelがDisposeされる際に同時に破棄したいリソースを格納するために使用されます。LivetのViewModel機能を使用する場合は、ViewModelと一緒に破棄したいリソースは基本的にViewModelのCompositeDisposableに格納する事になります。

ReactiveExtensionsと併用する場合には、RxのCompositeDisposableをLivetのViewModelのCompositeDisposableに放り込んでやるとよいでしょう。-->

#### DispatcherCollection and ReadOnlyDispatcherCollection

<!--
DispatcherCollectionは、既存の変更通知コレクションをコンストラクタの引数にとり、その変更通知を指定されたDispatcher上で行うコレクションです。ReadOnlyDispatcherCollection、DispatcherCollectionをコンストラクタの引数にとる読み取り専用ラッパーとなります。
-->

#### ViewModelHelper.CreateReadOnlyDispatcherCollection&lt;TModel,TViewModel&gt;

<!--
CreateReadOnlyDispatcherCollectionを使用すると、Modelの変更通知コレクションを指定し、そのModelのコレクションの変更と連動するReadOnlyDispatcherCollectionを生成できます。Func<TModel,TViewModel>を指定してTModel型とTViewModel型の相互変換を行います。



CreateReadOnlyDispatcherCollectionを使用して生成されたTViewModelの要素がIDisposableであった場合、sourceコレクションからRemoveされた場合など要素削除時にはDisposeが呼ばれます。

生成されたコレクションのDisposeを呼ぶことで、ソースコレクションとの連動は解除され、TViewModelがIDisposableであった場合は生成されたTViewModel型に対してDiposeが呼ばれます。-->

#### PropertyChangedEventListener CollectionChangedEventListener

<!--Modelのイベントを監視するのはViewModelの大きな役目です。しかしC#ではイベントハンドラの監視と解除を以下のような構文で行えません。



Livetでは特に煩雑になりがちなPropertyChangedイベントの監視と解除を容易にするため、PropertyChangedEventListenerクラスを用意してあります。

様々な形でのPropertyChangedイベントハンドリング



CollectionChangedEventListenerはそのコレクション変更通知版です。PropertyChangedEventListenerほど多機能ではありませんが似た様な事が可能です。

また、汎用EventListenerとしてEventListenerを用意してあります。



EventListenerやPropertyChangedEventListener/CollectionChangedEventListenerはIDisposable型であり、Disposeする事でハンドラの監視を解除します。

ViewModelのCompositeDisposableに放り込んでおけば何も考えずともイベントハンドラの監視解除が行えます。-->

### 3. Model Support
<!--ModelはMVVMの関心領域ではないため、Livetでも特に手厚いサポートはありません。

しかし最低限の機能として、変更通知イベント基底クラスとなるNotificationObjectと、スレッドセーフな変更通知コレクションであるObservableSynchronizedCollectionを用意してあります。

ObservableSyncronizedCollectionはMonitorベースのスレッドセーフなコレクションではなく、ReaderWriterLockSlimによるスレッドセーフなコレクションであり、読み書きが等しく複数スレッドから煩雑に行われるシナリオにおいて、パフォーマンスと変更通知のタイミングの偏りのバランスが良い様に設計されています。

前述したViewModelのDispatcherCollectionはただのラッパーであるため、Modelでは通常のObservableCollectionとObservableSyncronizedCollectionを用途に応じて使い分け、それをViewModelでは同様に扱う事ができます。-->

 
