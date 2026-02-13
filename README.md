# Spring PetClinic サンプルアプリケーション [![Build Status](https://github.com/spring-projects/spring-petclinic/actions/workflows/maven-build.yml/badge.svg)](https://github.com/spring-projects/spring-petclinic/actions/workflows/maven-build.yml)[![Build Status](https://github.com/spring-projects/spring-petclinic/actions/workflows/gradle-build.yml/badge.svg)](https://github.com/spring-projects/spring-petclinic/actions/workflows/gradle-build.yml)

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/spring-projects/spring-petclinic) [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=7517918)

## いくつかの図を使用したSpring Petclinicアプリケーションの理解

[プレゼンテーションはこちら](https://speakerdeck.com/michaelisvy/spring-petclinic-sample-application)

## Petclinicをローカルで実行

Spring Petclinicは、[Maven](https://spring.io/guides/gs/maven/)または[Gradle](https://spring.io/guides/gs/gradle/)を使用してビルドされた[Spring Boot](https://spring.io/guides/gs/spring-boot)アプリケーションです。jarファイルをビルドし、コマンドラインから実行できます（Java 17以降で動作します）：

```bash
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic
./mvnw package
java -jar target/*.jar
```

(Windowsの場合、またはシェルがglobを展開しない場合は、最後のコマンドラインでJARファイル名を明示的に指定する必要があるかもしれません。)

その後、<http://localhost:8080/>でPetclinicにアクセスできます。

<img width="1042" alt="petclinic-screenshot" src="https://cloud.githubusercontent.com/assets/838318/19727082/2aee6d6c-9b8e-11e6-81fe-e889a5ddfded.png">

または、Spring Boot Mavenプラグインを使用してMavenから直接実行することもできます。この方法を使用すると、プロジェクトで行った変更が即座に反映されます（Javaソースファイルの変更にはコンパイルも必要です - ほとんどの人はこれにIDEを使用します）：

```bash
./mvnw spring-boot:run
```

> 注意: Gradleを使用する場合は、`./gradlew build`でアプリをビルドし、`build/libs`でjarファイルを探してください。

## コンテナのビルド

このプロジェクトには`Dockerfile`はありません。Spring Bootビルドプラグインを使用して（dockerデーモンがある場合）コンテナイメージをビルドできます：

```bash
./mvnw spring-boot:build-image
```

## Spring Petclinicのバグや改善提案を見つけた場合

課題トラッカーは[こちら](https://github.com/spring-projects/spring-petclinic/issues)で利用可能です。

## データベース設定

デフォルト設定では、Petclinicは起動時にデータが投入されるインメモリデータベース（H2）を使用します。h2コンソールは`http://localhost:8080/h2-console`で公開されており、`jdbc:h2:mem:<uuid>` URLを使用してデータベースの内容を検査できます。UUIDは起動時にコンソールに出力されます。

永続的なデータベース設定が必要な場合、MySQLとPostgreSQLについても同様のセットアップが提供されています。データベースタイプが変更される場合は常に、アプリは異なるプロファイルで実行する必要があることに注意してください：MySQLの場合は`spring.profiles.active=mysql`、PostgreSQLの場合は`spring.profiles.active=postgres`です。アクティブなプロファイルの設定方法の詳細については、[Spring Bootドキュメント](https://docs.spring.io/spring-boot/how-to/properties-and-configuration.html#howto.properties-and-configuration.set-active-spring-profiles)を参照してください。

OSに適したインストーラーを使用してMySQLまたはPostgreSQLをローカルで起動するか、dockerを使用できます：

```bash
docker run -e MYSQL_USER=petclinic -e MYSQL_PASSWORD=petclinic -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=petclinic -p 3306:3306 mysql:9.2
```

or

```bash
docker run -e POSTGRES_USER=petclinic -e POSTGRES_PASSWORD=petclinic -e POSTGRES_DB=petclinic -p 5432:5432 postgres:17.5
```

[MySQL](https://github.com/spring-projects/spring-petclinic/blob/main/src/main/resources/db/mysql/petclinic_db_setup_mysql.txt)と[PostgreSQL](https://github.com/spring-projects/spring-petclinic/blob/main/src/main/resources/db/postgres/petclinic_db_setup_postgres.txt)の詳細なドキュメントが提供されています。

通常の`docker`の代わりに、提供されている`docker-compose.yml`ファイルを使用してデータベースコンテナを起動することもできます。各サービスはSpringプロファイルに基づいて名前が付けられています：

```bash
docker compose up mysql
```

or

```bash
docker compose up postgres
```

## テストアプリケーション

開発時には、`PetClinicIntegrationTests`（デフォルトのH2データベースを使用し、Spring Boot Devtoolsも追加）、`MySqlTestApplication`、`PostgresIntegrationTests`の`main()`メソッドとして設定されたテストアプリケーションを使用することをお勧めします。これらは、IDEでアプリを実行して迅速なフィードバックを得ることができ、同じクラスをそれぞれのデータベースに対する統合テストとして実行することもできるように設定されています。MySql統合テストはTestcontainersを使用してDockerコンテナでデータベースを起動し、PostgresテストはDocker Composeを使用して同じことを行います。

## CSSのコンパイル

`src/main/resources/static/resources/css`に`petclinic.css`があります。これは`petclinic.scss`ソースから[Bootstrap](https://getbootstrap.com/)ライブラリと組み合わせて生成されました。`scss`に変更を加えた場合、またはBootstrapをアップグレードした場合は、Mavenプロファイル「css」を使用してCSSリソースを再コンパイルする必要があります。つまり`./mvnw package -P css`です。GradleにはCSSをコンパイルするためのビルドプロファイルはありません。

## IDEでPetclinicを使用する

### 前提条件

システムに以下のアイテムがインストールされている必要があります：

- Java 17以降（JREではなく完全なJDK）
- [Gitコマンドラインツール](https://help.github.com/articles/set-up-git)
- お好みのIDE
  - m2eプラグインを使用したEclipse。注意：m2eが利用可能な場合、`Help -> About`ダイアログにm2アイコンがあります。m2eがない場合は、[こちら](https://www.eclipse.org/m2e/)のインストールプロセスに従ってください
  - [Spring Tools Suite](https://spring.io/tools) (STS)
  - [IntelliJ IDEA](https://www.jetbrains.com/idea/)
  - [VS Code](https://code.visualstudio.com)

### 手順

1. コマンドラインで実行：

    ```bash
    git clone https://github.com/spring-projects/spring-petclinic.git
    ```

1. EclipseまたはSTSの場合：

    `File -> Import -> Maven -> Existing Maven project`からプロジェクトを開き、クローンしたリポジトリのルートディレクトリを選択します。

    次に、コマンドラインで`./mvnw generate-resources`をビルドするか、Eclipseランチャーを使用して（プロジェクトを右クリックして`Run As -> Maven install`）CSSを生成します。アプリケーションのmainメソッドを右クリックして`Run As -> Java Application`を選択して実行します。

1. IntelliJ IDEAの場合：

    メインメニューで`File -> Open`を選択し、Petclinicの[pom.xml](pom.xml)を選択します。`Open`ボタンをクリックします。

    - CSSファイルはMavenビルドから生成されます。コマンドラインで`./mvnw generate-resources`をビルドするか、`spring-petclinic`プロジェクトを右クリックして`Maven -> Generates sources and Update Folders`を選択できます。

    - 最近のUltimateバージョンを使用している場合、`PetClinicApplication`という名前の実行構成が作成されているはずです。それ以外の場合は、`PetClinicApplication`メインクラスを右クリックして`Run 'PetClinicApplication'`を選択してアプリケーションを実行します。

1. Petclinicに移動

    ブラウザで[http://localhost:8080](http://localhost:8080)にアクセスします。

## 特定のものをお探しですか？

|Spring Boot設定 | クラスまたはJavaプロパティファイル  |
|--------------------------|---|
|メインクラス | [PetClinicApplication](https://github.com/spring-projects/spring-petclinic/blob/main/src/main/java/org/springframework/samples/petclinic/PetClinicApplication.java) |
|プロパティファイル | [application.properties](https://github.com/spring-projects/spring-petclinic/blob/main/src/main/resources) |
|キャッシング | [CacheConfiguration](https://github.com/spring-projects/spring-petclinic/blob/main/src/main/java/org/springframework/samples/petclinic/system/CacheConfiguration.java) |

## 興味深いSpring Petclinicのブランチとフォーク

[spring-projects](https://github.com/spring-projects/spring-petclinic) GitHub organizationのSpring Petclinic「main」ブランチは、Spring BootとThymeleafに基づいた「標準的な」実装です。GitHub organization [spring-petclinic](https://github.com/spring-petclinic)には[多数のフォーク](https://spring-petclinic.github.io/docs/forks.html)があります。異なる技術スタックを使用してPet Clinicを実装することに興味がある場合は、そこのコミュニティに参加してください。

## Interaction with other open-source projects

One of the best parts about working on the Spring Petclinic application is that we have the opportunity to work in direct contact with many Open Source projects. We found bugs/suggested improvements on various topics such as Spring, Spring Data, Bean Validation and even Eclipse! In many cases, they've been fixed/implemented in just a few days.
Here is a list of them:

| 名前 | Issue |
|------|-------|
| Spring JDBC: NamedParameterJdbcTemplateの使用を簡素化 | [SPR-10256](https://github.com/spring-projects/spring-framework/issues/14889)および[SPR-10257](https://github.com/spring-projects/spring-framework/issues/14890) |
| Bean Validation / Hibernate Validator: Maven依存関係と後方互換性の簡素化 |[HV-790](https://hibernate.atlassian.net/browse/HV-790)および[HV-792](https://hibernate.atlassian.net/browse/HV-792) |
| Spring Data: JPQLクエリを使用する際の柔軟性の向上 | [DATAJPA-292](https://github.com/spring-projects/spring-data-jpa/issues/704) |

## コントリビューション

バグレポート、機能リクエスト、プルリクエストの送信には、[課題トラッカー](https://github.com/spring-projects/spring-petclinic/issues)が推奨されるチャンネルです。

プルリクエストの場合、一般的なテキストエディタで簡単に使用できるように、[editor config](.editorconfig)にエディタの設定が用意されています。詳細については<https://editorconfig.org>で確認し、プラグインをダウンロードしてください。すべてのコミットには、コントリビューターがDeveloper Certificate of Originに同意していることを示すために、各コミットメッセージの最後に__Signed-off-by__トレーラーを含める必要があります。
詳細については、ブログ記事[Hello DCO, Goodbye CLA: Simplifying Contributions to Spring](https://spring.io/blog/2025/01/06/hello-dco-goodbye-cla-simplifying-contributions-to-spring)を参照してください。

## ライセンス

Spring PetClinicサンプルアプリケーションは、[Apache License](https://www.apache.org/licenses/LICENSE-2.0)バージョン2.0の下でリリースされています。
