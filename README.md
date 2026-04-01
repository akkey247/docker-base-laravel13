# 使い方

## 環境構築

### 1. コンテナのビルド＆起動

```
$ docker-compose up -d
```

### 2. コンテナに入る

```
$ docker-compose exec php bash
```

### 3. 自動インストール

```
/var/www# install-laravel --jetstream=livewire --verification
```

|オプション|説明|
|---|---|
|--breeze|Laravel Breeze をインストールする。標準インストール(Alpne.js)。|
|--breeze=TYPE|Laravel Breeze をインストールする。TYPEには vue, react が指定できる。|
|--jetstream|Laravel Jetstream をインストールする。標準インストール(Livewire)。|
|--jetstream=TYPE|Laravel Jetstream をインストールする。TYPEには livewire, inertia が指定できる。|
|--fortify|Laravel Fortify をインストールする。|
|--teams|Laravel Jetstream のチーム機能を有効にする。(Fortify でも指定可能)|
|--api|Laravel Jetstream のAPI機能を有効にする。|
|--verification|Laravel Jetstream のメールバリデーション機能を有効にする。|
|-h, --help|ヘルプを表示する|
|-v, --version|コマンドのバージョンを表示する|

### 4. storage ディレクトリの権限を変更

```
/var/www# chown www-data:www-data -R storage
```

※実際のサイトではもっとちゃんと権限設定を行うこと。

### 5. サイトにアクセスする

[サイト]
http://localhost:8000/

[PhpMyAdmin]
http://localhost:8080/

[mailhog]
http://localhost:8025/

## 環境構築後

### コンテナを起動する

```
$ docker-compose up -d
```

### コンテナを停止する

```
$ docker-compose down
```

### コンテナを停止＆イメージ削除

```
$ docker-compose down --rmi all --volumes
```

## 備考1: Vue, React 利用時の Vite 設定

初期の `vite.config.js` では画面が真っ白になるので以下の設定を加える。  

```
export default defineConfig({
    plugins: [
        // 省略
    ],
    server: {
        host: true,
        hmr: {
            host: 'localhost'
        },
        watch: {
            usePolling: true,
        },
    },
});
```

# 参考記事

[docker で Laravel 環境構築](https://qiita.com/rope19181/items/10da72374839630af83b)
