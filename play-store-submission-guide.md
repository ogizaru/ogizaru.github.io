# Luvid Google Play ベータ版（テスト）提出用ガイド・下書き集

このファイルは Google Play Console へ Luvid（`com.luvid.app`）のテストトラック（内部テスト / クローズドテスト / オープンテスト）を提出する際の入力用下書きです。

---

## 1. ビルド済み成果物と鍵情報

* **提出用 App Bundle**: `C:\dev\Luvid\android\app\build\outputs\bundle\release\app-release.aab`
* **アイコン画像 (512×512 PNG)**: `C:\dev\Luvid\play_store_assets\app_icon_512x512.png`
* **フィーチャーグラフィック (1024×500 PNG)**: `C:\dev\Luvid\play_store_assets\feature_graphic_1024x500.png`
* **プライバシーポリシー HTML**: `C:\dev\Luvid\docs\privacy-policy.html`
  * ※ 公開前に最下部の `[ここに運営者名と連絡先メールアドレスを記入してください]` を書き換え、GitHub Pages 等の公開 URL に配置してください。

---

## 2. ストア掲載情報（コピペ用下書き）

### アプリ名（30文字以内）
```text
Luvid - ライブ配信スイッチャー
```

### 簡単な説明（80文字以内・現在 66 文字）
```text
外部HDMI/UVCカメラと内蔵カメラを切り替え、テロップ・画像・BGM合成でYouTube等へライブ配信＆録画できるモバイルスイッチャー。
```

### 詳しい説明（4000文字以内）
```text
Luvid（ルヴィド）は、Android スマートフォン 1 台でマルチカメラ切り替え・音声ミキシング・テロップ/画像オーバーレイ合成・ライブ配信・ローカル録画を行えるモバイル向けライブ配信スイッチャーです。

■ 主な機能
1. 外部 HDMI / USB UVC カメラ＆内蔵カメラ対応
   - USB UVC キャプチャ経由の外部カメラ / HDMI 映像入力に対応
   - インカメラ / アウトカメラの切り替え、解像度・FPS・回転・スケーリング設定に対応
   - 露出・フォーカス・ホワイトバランス・ズームのカメラ調整に対応

2. シーン切り替え＆オーバーレイ合成
   - カット / クロスフェード等のトランジション付きシーン切り替え
   - 2系統のテキストテロップ（フォント・サイズ・縁取り・背景・スナップ配置）
   - 透過 PNG ロゴオーバーレイ、全画面 JPEG / 連番スライドショー表示（背景単色塗りつぶし対応）

3. オーディオミキサー＆BGMプレイヤー
   - 内蔵マイク / USB オーディオ（UAC）/ Bluetooth マイクの入力切り替え
   - チャンネルごとの音量・ミュート・ソロ・コンプレッサー調整
   - 端末内音声ファイルを使った BGM プレイリスト管理＆音声ダッキング

4. 配信プロトコル＆通信復旧対策
   - RTMP / RTMPS / SRT / ローカル録画に対応
   - 自動ビットレート調整・通信断時の自動再接続に対応
   - YouTube 連携による配信枠の取得・作成・タイトル/概要欄編集、ライブチャット取得＆画面上コメント表示

※ 現在ベータテスト中のため、一部機能や UI は今後のアップデートで改善・変更される場合があります。
```

### リリースノート例（`ja-JP`）
```text
Luvid ベータ版テストリリースです。
外部HDMI/UVC入力、内蔵カメラ切り替え、シーン・テロップ・PNG/JPEGオーバーレイ合成、音声ミキシング・BGM再生、YouTubeライブ配信・録画機能をお試しいただけます。
```

---

## 3. アプリのコンテンツ（審査申告用ガイド）

### A. プライバシーポリシー
* `docs/privacy-policy.html` の公開 URL を登録します。

### B. データセーフティ（Data Safety）回答の目安
* **アプリはユーザーデータを収集または共有しますか？**
  * 開発者独自の収集・第三者共有サーバーはありません。
  * ただし、Google アカウント / YouTube 連携機能において Google 認証（メールアドレス・名前）や YouTube API 通信を行う場合は、機能提供・アカウント管理目的（端末内暗号化保持・ユーザー任意連携のみ）として申告方針を Play Console の質問に沿って入力してください（他社への共有: いいえ、広告目的: いいえ、送信中の暗号化: はい（HTTPS）、データ削除の仕組み: アプリ内連携解除＆アンインストール）。

### C. フォアグラウンドサービスの権限申告
Play Console で `FOREGROUND_SERVICE` の用途確認が表示された場合、宣言している 4 種類の用途を以下のように回答します：
* `camera` / `microphone` / `connectedDevice` / `mediaPlayback`:
  * **日本語概要**: アプリがバックグラウンドへ移行してもライブ配信・ローカル録画・USB接続キャプチャ機器からの映像/音声取り込み・BGMミキシング再生を途切れさせずに継続するため。配信/録画中は継続通知を表示し、通知の停止ボタンまたはアプリ内ボタンからいつでも停止可能。
  * **English Summary (審査入力推奨)**:
    `Used to maintain uninterrupted live video/audio streaming, local MP4 recording, external USB UVC/UAC capture device input, and background BGM mixing playback when the user navigates away or locks the screen. A persistent notification with a Stop action is shown while active.`

### D. アプリアクセス権（App Access）
* Google / YouTube 連携を使わなくてもカスタム RTMP / SRT やローカル録画機能は操作可能ですが、YouTube 連携部分を審査チームに伝える場合は「YouTube Live 連携機能のみ Google ログイン（OAuth）が必要で、カメラプレビュー・シーン合成・ローカル録画・カスタム RTMP 入力はログイン不要で動作する」旨を記載してください。

---

## 4. Google Play Console 公開手順まとめ

1. **Google Play Console** を開き、左メニュー **「テスト」 > 「内部テスト」** を選択。
2. **「新しいリリースを作成」** をクリックし、Play アプリ署名（Google Play App Signing）の画面が出たら **「続行」**（推奨設定）を選択。
3. **`app-release.aab`** をアップロードし、リリースノートを入力して **「次へ」 > 「保存」 > 「公開」**。
4. 同じページの **「テスター」タブ** で自分の Gmail（またはテスターリスト）を選択し、画面下部の **「リンクをコピー」** からオプトイン URL を取得。
5. 実機でその URL を開き「テスターになる」をタップ → Google Play ストア経由で Luvid をインストール。
6. 動作確認後、**「クローズドテスト」**（トラックを作成）へ **「リリースをプロモート」** し、必要なテスター登録・アプリのコンテンツ審査提出を行ってベータ配信を開始します。
7. **YouTube 連携を使う場合の OAuth 注意事項**:
   * Play Console の **「テストとリリース > 設定 > アプリの署名」** にある **「アプリ署名鍵の証明書」の SHA-1** を控えてください。
   * Google Cloud Console で Android OAuth クライアント等を利用している場合は、その **Play 側の SHA-1** も追加登録し、OAuth 同意画面のテストユーザーへテスターのメールアドレスを追加してください。
