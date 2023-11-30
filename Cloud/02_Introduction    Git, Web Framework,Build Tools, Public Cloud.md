Knowledge  	
Web Frameworkの概要とメリット  
可読性の高いコードの特徴  
Linter, Code Formatterの概要とメリット  
Cloud IDEの概要とローカルPCでの開発環境構築と比較した際のメリット  
Build Toolsの概要とメリット  
Gitの概要とメリット  
リージョン、アベイラビリティゾーン、VPC、サブネットの関係性  
IAMの概要  
セキュリティグループの役割  
Skills  
AWSの各リソースをAWS管理コンソールから作成できる  
アプリケーションフレームワークを用いて、web アプリケーションを作成できる  
Mavenを用いた依存関係追加・ビルドまで実施できる  
コードを読んだだけで他人が理解できるような可読性の高いコードを書くことができる  
ルール通りにGitを用いた開発を遂行できる  
Cloud9の開発環境を「Share」で他人に共有できる  
Spec  
 標準PCからAWS環境のアプリケーションにアクセスし、アプリケーション外部仕様通りに表示される  
概要  
Spring BootでWebアプリを作成する  
AWS上でインフラ構築を行う  
AWS環境にアプリケーションをDeployする  

![image](https://github.com/pantyou/AWS-Service/blob/main/image/systemimage2.png)

![image](https://github.com/pantyou/AWS-Service/blob/main/image/systemimage3.png)

講義
01 Git講義資料を読み、以下について理解する  
バージョン管理とは何か
Gitとは何か
Gitの特徴
Gitの構造
Gitで使用する単語

02 Springboot  
講義資料を読み、以下について理解する
Springbootとは何か
Springbootの特徴

03 セキュリティ（IAM）  
講義資料を読み、以下について理解する
IAMとは何か
IAMのベストプラクティス
スイッチロールとは何か

04 セキュリティ（セキュリティグループ）  
講義資料を読み、以下について理解する
セキュリティグループの役割

アプリケーション
05 開発対象  
アプリケーション外部仕様を実現するアプリケーションを作成する

トップページはHTML単体でなくコントローラクラス使用し/toppageなどのパスで表示されるようにする

一覧ページはServiceから取得したデータ数分だけ拡張して表示する。

データはRepositoryクラスにべた書きで構わない（今回はDatabaseを使用しない為）

Controller,ServiceはL_Java_Springbootを参考に作成する

Code Formatter

Code Formatterはfmt-maven-pluginを使用する。pom.xmlに追記する。
ビルド時に強制的にGoogle Java Style Guideを満たすフォーマットが実施されること

パッケージ名

パッケージ名は以下を設定

jp.scsk.training.trgapp
プロジェクト名

プロジェクト名は以下を設定

web-ui-teamX-個人名

利用するツール

SpringBoot
Thymleaf
SpringbootWeb


クラウド（AWS）
06 IAMロール（EC2）
AWS管理コンソールのIAMから以下の権限を付与する

S3へのアクセス（ReadOnly）
SystemsManagerへのアクセス（AmazonSSMManagedInstanceCore）

07 サブネット  
AWS管理コンソールから各自のサブネットを作成する

詳細

リージョン	東京
VPC	hrd-d0-base-vpc
サブネット名	
hrd-d0-sub-"(pub) or (pri)""Num"-"(teamX) or (name)"

例）hrd-d0-sub-pub1-hri

タグ	
AWSリソース命名規則 に基づき設定する

Name：hrd-d0-sub-pub1-"(teamX) or (name)"
Cost：hrd-d0-"(teamX) or (name)"
Env：hrd-d0

08 ルートテーブル  
AWS管理コンソールから各自のルートテーブルを作成し、

作成したサブネットの関連付け、および Gateway へのルーティングを設定する

PublicGateway：InternetGatewayへのルーティング

PrivateGateway：NatGatewayへのルーティング

09 Route53  
指定の共通ホストゾーンを利用し、サブドメインのホストゾーンを作成する
※サブドメインのトラフィックがルーティングされるよう、共通ホストゾーンにNSレコードの設定を行う

サブドメインのホストゾーンには以下を設定する

Certificate Manager用レコード：CNAME
ELB用レコード：Ａ

10 Certificate Manager
東京リージョンに証明書を発行する（パブリック証明書をDNS検証にて発行）

11 セキュリティグループ（ELB）
以下のようにアクセスを制限する

SCSK環境（※netskopeのグローバルIP）からアクセスできる

12 Target group  
Target group を作成するのみ、EC2作成後にRegister targets からEC2を追加

13 ELB
Load balancer type：Application

14 セキュリティグループ（EC2）
以下のようにアクセスを制限する
ELBからアクセスできる

15 EC2インスタンス
AWS管理コンソールから各自のプライベートサブネット上に作成する。

インスタンスタイプ：t3.micro


新人育成

AMI ID：ami-0cb4639ca5eb232fc
DevOps実践（DevOps研修（初級））

AMI ID：ami-05cb53d3f45fb562e


作成後、Target groupに作成したEC2を登録する

16 EC2へのログイン

AWS管理コンソールのSystemsManagerのSessionManagerを用いて、EC2にログインする

17 EC2へJavaをインストール
JavaはAmazon Correttoをインストールする
Amazon Corretoのバージョンはローカル開発で使用しているバージョンにする

18 S3
AWS管理コンソールから各自のS3バケットを作成する

リージョン：東京
パブリックアクセス設定：パブリックアクセスをすべてブロック

19 アプリケーションのDeploy
ビルドした jar ファイルをS3に配置し、

EC2からS3のファイルをgetする

その後EC2上で jar ファイルを実行し、ブラウザ上からページへ接続できることを確認する

20 既存リソースの削除
スプリントレビュー後に既存リソースを削除する
