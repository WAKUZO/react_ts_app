# ①ディレクトリを作成

```
mkdir react_ts_app
cd react_ts_app
```

## ②各種設定ファイルを準備する

```
% touch {docker-compose.yml,Dockerfile}
```

**Dockerfile**
```yml:Dockerfile
FROM node:17.4.0-alpine
WORKDIR /usr/src/app
```

**docker-compose.yml**
```yml:docker-compose.yml
version: '3'
services:
  frontend:
    build: .
    # Node.jsのグローバル変数です。開発用途なのでdevelopmentを指定します。
    environment:
      - NODE_ENV=development
    volumes:
      - ./:/usr/src/app
    command: sh -c 'cd frontend && yarn start'
    ports:
      - 8000:3000
    tty: true
```

# ③イメージの構築
```
% docker-compose build
```

# ④React＋TypeScriptでプロジェクトを作成

TypeScriptを指定して、create-react-appする

```
% docker-compose run --rm frontend sh -c 'npx create-react-app frontend --template typescript'
```

# ⑤コンテナの作成と起動

```
% docker-compose up -d
```

# ⑥ローカルホストに接続

http://localhost:8000/ にアクセスする

以下が表示されれば完了
![](https://storage.googleapis.com/zenn-user-upload/673b42e5a48a-20220820.png)


# ローカルで動かす

git clone後

```
% docker-compose build
% docker-compose run --rm frontend yarn install
% docker-compose up -d
````

http://localhost:8000/ にアクセスする


## 環境

```
Apple M1 Pro
macOS BigSur 12.1
Docker Engine 20.10.12
Docker Compose 1.29.2
react 18.0.17
react-dom 18.0.6
typescript 4.7.4
```
