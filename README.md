# Readme
最初に行うべき手順を記載しています。

## ドキュメント一覧
- [docker設定方法](docs/docker設定方法.md)

## 概要
原価・利益管理システムのコードを管理します。
React + Express + MySQL を使用した開発環境。

## セットアップ手順

## 前提
- Docker Desktop がインストールされていること

## 構成
- frontend: React
- backend: Express (Node.js)
- db: MySQL

## フロントエンドセットアップ手順
### ディレクトリ構成
```
frontend/
├── public/
├── src/
└── package.json
```
### 1. frontend ディレクトリでReactアプリを作成
```bash
cd frontend
npx create-react-app frontend
```
### 2. 動作確認
```bash
npm start
```
初期画面(Reactロゴが回転している)が、表示されれば成功。
## バックエンドセットアップ手順
### ディレクトリ構成
```
backend/
├── app.js
├── package.json
└── routes/
    └── health.js
```
### 1. backend ディレクトリに移動
```bash
cd backend
npm init -y
```
### 2. 必要なパッケージをインストール
```
npm install express cors
```
### 3. routes/health.js を作成し、以下を記述
```
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.json({ status: 'ok', message: 'Backend is running!' });
});

module.exports = router;
```
### 4. app.js を作成し、以下を記述
```
const express = require('express');
const cors = require('cors');

const app = express();
const port = 5000;

app.use(cors());
app.use(express.json());

// ルート読み込み
const healthRoute = require('./routes/health');
app.use('/health', healthRoute);

app.listen(port, () => {
  console.log(`Backend server running at http://localhost:${port}`);
});
```
### 5. 動作確認
```bash
npm start

ブラウザで以下URLを開く。
http://localhost:5000/health
```
「{"status":"ok","message":"Backend is running!"}」が、表示されれば成功。
