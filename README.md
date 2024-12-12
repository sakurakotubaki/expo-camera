# Expo Camera App

このプロジェクトは、Expo と React Native を使用してモバイルカメラアプリケーションを実装したものです。

## 環境構築

### 必要条件
- [Bun](https://bun.sh/) がインストールされていること
- [Expo Go](https://expo.dev/client) アプリ（iOS/Android）がインストールされていること

### セットアップ手順

1. プロジェクトのクローン（または新規作成）:
```bash
# 新規プロジェクトを作成する場合
bunx create-expo-app expo-camera
cd expo-camera

# または既存のプロジェクトをクローンした場合
cd expo-camera
bun install
```

2. 必要なパッケージのインストール:
```bash
bun add expo-camera expo-media-library
```

3. アプリの起動:
```bash
bun start
```

## カメラ機能の実装

### 主な機能
- カメラのプレビュー表示
- フロント/バックカメラの切り替え
- フラッシュモードの切り替え
- 写真撮影とギャラリーへの保存

### 必要な権限
アプリを実行するには以下の権限が必要です：
- カメラへのアクセス権限
- メディアライブラリへの保存権限

### 実装例

`App.tsx` にカメラ機能を実装しています。主な実装内容：

1. カメラのパーミッション取得
```typescript
const [permission, requestPermission] = useCameraPermissions();
const [mediaPermission, requestMediaPermission] = MediaLibrary.usePermissions();
```

2. カメラの設定
```typescript
const [facing, setFacing] = useState<CameraType>('back');
const [flash, setFlash] = useState<FlashMode>('off');
```

3. 写真撮影機能
```typescript
const takePicture = async () => {
  if (!cameraRef.current) return;
  try {
    const photo = await cameraRef.current.takePictureAsync();
    await MediaLibrary.saveToLibraryAsync(photo.uri);
  } catch (error) {
    console.error(error);
  }
};
```

## トラブルシューティング

1. パーミッションエラー
- アプリの設定から、カメラとメディアライブラリへのアクセスを許可してください。

2. カメラが起動しない場合
- Expo Go アプリを再起動してください。
- デバイスを再起動してください。

## 開発環境のヒント

- 開発中は実機での動作確認を推奨します（エミュレータでもカメラ機能は使用可能ですが、実機の方がスムーズです）。
- Expo Go アプリを使用することで、簡単にアプリのテストが可能です。

## 参考リンク

- [Expo Camera Documentation](https://docs.expo.dev/versions/latest/sdk/camera/)
- [Expo Media Library Documentation](https://docs.expo.dev/versions/latest/sdk/media-library/)
