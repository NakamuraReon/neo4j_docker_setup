# Dockerを使用したPythonとNeo4jの開発環境を構築
<div id="top"></div>

## 使用技術一覧

<!-- シールド一覧 -->
<!-- 該当するプロジェクトの中から任意のものを選ぶ-->
<p style="display: inline">
  <img src="https://img.shields.io/badge/-Python-F2C63C.svg?logo=python&style=for-the-badge">
  <img src="https://img.shields.io/badge/-Docker-1488C6.svg?logo=docker&style=for-the-badge">
  <img src="https://img.shields.io/badge/-Neo4j-FFFFFF.svg?logo=neo4j&style=for-the-badge">

</p>

## 目次

1. [リポジトリの説明](#リポジトリの説明)
2. [環境](#環境)
3. [ディレクトリ構成](#ディレクトリ構成)
4. [環境構築](#環境構築)
5. [動作確認](#動作確認)
5. [留意点](#留意点)

<!-- プロジェクト名を記載 -->

## リポジトリの説明
Dockerを使用したPythonとNeo4jの開発環境を構築方法を紹介しています．  
[こちらのQiitaの記事](https://qiita.com/Ryo412/items/0d82934c401ccd6a5df4)を参考にしています．  

<!-- プロジェクトについて -->


## 環境

<!-- 言語、フレームワーク、ミドルウェア、インフラの一覧とバージョンを記載 -->

| 言語・フレームワーク  | バージョン |
| --------------------- | ---------- |
| Python                | 3.11.4     |
| Neo4j                 | 5.13.0     |

その他のパッケージのバージョンは docker-compose.yml と python_docker/Dockerfile と python_docker/requirements.txt を参照してください


## ディレクトリ構成

<!-- Treeコマンドを使ってディレクトリ構成を記載 -->
    neo4j_docker_setup
       ├ src
       |   ├ neo4j_test.py
       |   └ search_test.py
       ├ python_docker
       |     ├ Dockerfile　
       |     └ requirements.txt
       ├ docker-compose.yml
       ├ .gitignore
       └ README.me


## 環境構築
<!-- コンテナの作成方法、パッケージのインストール方法など、開発環境構築に必要な情報を記載 -->
1. イメージの作成
    ```
    % docker-compose build
    ```
2. コンテナの構築と起動
    ```
    % docker-compose up -d
    ```
3. Neo4jデータベースへの接続  
    http://localhost:7474/browser にアクセス．  
    ユーザ名とパスワードはそれぞれ**neo4j**と**p@ssw0rd**．
4. コンテナを停止する際
    ```
    % docker-compose down
    ```


## 動作確認
VS CodeのRemote-Containers等を使用して**my_python**コンテナに入る．  
ワーキングディレクトリは`app/`．
1. ノードの作成
    ```
    % python src/neo4j_test.py
    ```
2. ノードの検索
    ```
    % python src/search_test.py
    ```


## 留意点
1. docker-compose.ymlを書き換えてコンテナを再構築・起動する際  
neo4j_docker_setup下にあるneo4jフォルダを削除してから再起動する．

2. Neo4jのユーザ名とパスワードの変更  
docker-compose.ymlの`NEO4J_AUTH=neo4j/p@ssw0rd`を編集する．  
編集後は留意点１を実行．

3. neo4jのバージョンを変更  
docker-compose.ymlの`image: neo4j:5.13.0`を編集して自分の利用したいバージョンのイメージをpullする．  
編集後は留意点１を実行．

4. Neo4j Desktopを使用する際  
LOCAL DBMSを作成し起動が完了してから，Dockerコンテナの構築と起動を実行する．  
LOCAL DBMSはPluginsからAPOCのインストールを行う．
