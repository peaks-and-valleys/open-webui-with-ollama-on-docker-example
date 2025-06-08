# Open WebUI with Ollama on Docker example

## 使い方

1. `docker compose up -d`
2. `http://localhost:8080` に接続
   1. 初回のみ管理者アカウントのメールアドレスとパスワードの設定を求められる

## インストール

以下はすべて Ubuntu 24.04 (WSL 2 on Windows 11) で検証した。

### Ollama 

Linux 環境下であれば [Ollama の README の指示](https://github.com/ollama/ollama/blob/main/docs/linux.md) に従う。

#### TL;DR

インストールとスタートアップサービスへの登録だけ行えば、とりあえず使えそうだった。

- https://github.com/ollama/ollama/blob/main/docs/linux.md#install
- https://github.com/ollama/ollama/blob/main/docs/linux.md#adding-ollama-as-a-startup-service-recommended

#### LLM モデル

https://www.ollama.com/library の中から、マシンスペックと相談しながら使いたいモデルを pull する。
たとえば `gemma3:12b` を使いたい場合は、 `ollama pull gemma3:12b`　をする。

### Open WebUI

`ghcr.io/open-webui/open-webui:ollama` の pull のみで完了する。

## Docker command

この例の `compose.yaml` は、以下の `docker run` コマンドと同等である。

```docker
docker run -d --gpus all --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:ollama
```

Ollama との接続に手こずったため、以下のコマンドをベースにすることで問題を回避した: https://docs.openwebui.com/troubleshooting/connection-error#-docker-connection-error
