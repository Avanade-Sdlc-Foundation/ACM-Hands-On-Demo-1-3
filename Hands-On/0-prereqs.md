# 演習 0: 環境のセットアップと前提条件

| [README](./README.md) | [次の手順: カスタム指示ファイル作成 →](./1-agent-instructions.md) |
|:--|--:|

このハンズオンを始める前に、必要な環境設定と前提条件を確認し、準備を整えます。

## シナリオ

Spring Boot PetClinicプロジェクトを使用して、GitHub Copilotの高度な機能を活用したドキュメント生成ワークフローを実践します。最新のCopilot機能を効果的に利用するために、適切な環境設定が重要です。

## 必須 1. 開発環境の確認

### 1.1 Visual Studio Codeバージョン確認

1. VS Codeを起動します
2. `Help` > `About`をクリックして、バージョン情報を確認します
3. 最新版（推奨: 1.85以降）であることを確認します
   - 古いバージョンの場合は、`Help` > `Check for Updates`でアップデートしてください

### 1.2 GitHub Copilot拡張機能の確認

1. VS Codeの拡張機能ビューを開きます (`Ctrl+Shift+X`)
2. 以下の拡張機能がインストール・有効化されていることを確認します：
   - **GitHub Copilot** (必須)
   - **GitHub Copilot Chat** (必須)
   
   拡張機能が見つからない場合：
   - 検索ボックスで「GitHub Copilot」を検索
   - 「Install」ボタンをクリックしてインストール
3. 各拡張機能が最新版であることを確認し、必要に応じて更新します

### 1.3 GitHubアカウントとライセンス確認

1. GitHub Copilotの有効なライセンスを持っていることを確認します
2. VS CodeでGitHubアカウントにサインインしていることを確認します
   - `View` > `Command Palette` > `GitHub: Sign In`

## 必須 2. プロジェクトの準備

### 2.1 Spring Boot PetClinicプロジェクトの確認

1. 現在のワークスペースにSpring Boot PetClinicプロジェクトが開かれていることを確認します
2. 主要なフォルダー構成を確認します：
   ```
   ├── src/main/java/org/springframework/samples/petclinic/
   ├── src/main/resources/
   ├── pom.xml (Maven使用の場合)
   ├── build.gradle (Gradle使用の場合)
   ```

### 2.2 必要なファイルの存在確認

以下のファイルが存在することを確認します：
- `PetClinicApplication.java`
- `owner/OwnerController.java`
- `vet/VetController.java`
- `pet/PetController.java`

## 必須 3. 作業用ブランチの作成

### 3.1 新しいブランチの作成

演習での変更がメインブランチに影響することを防ぐため、専用の作業ブランチを作成します。

1. 現在のGit状態を確認します：
   ```bash
   git status
   ```
   未コミットの変更がある場合は、コミットまたはstashしてください。

2. VS Codeのターミナルを開きます（`Ctrl+Shift+`` または `View` > `Terminal`）
3. 以下のコマンドで新しいブランチを作成・切り替えします：
   ```bash
   git checkout -b handson-copilot-docs
   ```
4. ブランチが正しく作成されたことを確認します：
   ```bash
   git branch
   ```
   `* handson-copilot-docs` と表示されることを確認してください。

## 必須 4. GitHub Copilot Chatの起動と動作確認

### 4.1 Copilot Chatの起動

1. VS CodeサイドバーのCopilot Chatアイコン（メッセージバブルのようなアイコン）をクリックします
   ![GitHub Copilot Chat アイコン - サイドバーの右側にあるチャットバブル形状のアイコン](images/chat-icon.png)
2. または、キーボードショートカットを使用します：
   - Windows/Linux: `Ctrl+Alt+I`
   - Mac: `Cmd+Option+I`

### 4.2 基本動作確認

1. Copilot Chatに以下のテストメッセージを入力します：
   ```
   このプロジェクトの概要を教えてください
   ```
2. 適切な応答が返ることを確認します
3. ワークスペースのファイルを認識していることを確認します

## 参考 5. 追加設定（オプション）

### 5.1 ワークスペースの最適化

1. VS Codeでフォルダー全体を開いていることを確認します
2. Javaプロジェクトの場合、Java拡張機能パックも有効にすることを推奨します

### 5.2 Copilot設定の確認

1. `File` > `Preferences` > `Settings`を開きます
2. `Copilot`で検索し、以下の設定を確認します：
   - `Copilot: Enable` - 有効になっていること
   - `Copilot Chat: Enable` - 有効になっていること

## トラブルシューティング

### よくある問題

1. **Copilot Chatが応答しない場合**
   - インターネット接続を確認
   - GitHub Copilotライセンスの有効性を確認
   - VS Codeの再起動を試行

2. **プロジェクトを認識しない場合**
   - VS Codeでプロジェクトのルートフォルダーを開いていることを確認
   - ファイルエクスプローラーでプロジェクト構造を確認

3. **拡張機能が動作しない場合**
   - 拡張機能の無効化・有効化を試行
   - VS Codeの再起動
   - 拡張機能の再インストール

## まとめと次のステップ

環境設定が完了しました。これで以下の準備が整いました：

- GitHub Copilotの動作確認完了
- Spring Boot PetClinicプロジェクトの認識確認
- Copilot Chatの基本動作確認

次のステップでは、GitHub Copilot Agentモードを使用して、プロジェクト固有のカスタム指示ファイルを作成します。これにより、より精度の高いコード生成とドキュメント作成が可能になります。

## リソース

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [VS Code Copilot Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
- [Spring PetClinic Project](https://github.com/spring-projects/spring-petclinic)

---

| [README](./README.md) | [次の手順: カスタム指示ファイル作成 →](./1-agent-instructions.md) |
|:--|--:|