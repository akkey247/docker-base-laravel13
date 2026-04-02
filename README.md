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
/var/www# install-laravel
```

スターターキット（[Laravel Starter Kits](https://laravel.com/docs/starter-kits) 系）を使う場合の例です。

```
/var/www# install-laravel --kit
/var/www# install-laravel --kit=vue
```

[Laravel Fortify](https://laravel.com/docs/fortify) を入れる場合の例です。

```
/var/www# install-laravel --fortify
```

| オプション | 説明 |
|---|---|
| `--kit` | スターターキットを入れる（既定のスタックは livewire） |
| `--kit=STACK` | スタックを指定。`STACK` には `react` `vue` `svelte` `livewire` が指定できる。 |
| `--fortify` | Laravel Fortify を入れる（通常の Laravel プロジェクト向け） |
| `-h`, `--help` | ヘルプを表示する |
| `-v`, `--version` | バージョンを表示する |

`--kit` と `--fortify` を同時に付けた場合は、スターターキットのインストールのみ行われ、Fortify は実行されません。

### 4. storage ディレクトリの権限を変更

```
/var/www# chown www-data:www-data -R storage
```

※実際のサイトではもっとちゃんと権限設定を行うこと。

### 5. フロントの開発用ビルドサーバー（Vite）を起動する

フロント資産の開発用ビルドと、ホットリロード（HMR）のために Vite を起動する。

```
/var/www# npm run dev
```

### 6. サイトにアクセスする

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

(Laravel13で起きるのかは不明。起きないならこの項目は削除していいかも。)

スターターキットやフロントを使う場合、初期の `vite.config.js` では画面が真っ白になることがあるので、以下の設定を加える。

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
