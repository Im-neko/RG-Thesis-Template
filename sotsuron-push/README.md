# README
- 初回は手動でSFSに成果登録を行ってください．(初回と2回目で登録フローが異なるが未対応の為)
- selenium/hub, selenium/node-chromeを併用する想定です．
  - アップロードしたいファイルは起動時のディレクトリに対して`../paper`に配置してください．
  - ex) ../paper/thesis.pdf
- 環境変数でSFSのログイン情報を渡してください．
- FILE_TITLEは指定が無い場合`thesis`になります
- 実行しているファイルのソースコードはここです
- (https://github.com/Im-neko/RG-Thesis-Template/tree/master/sotsuron-push)


## sample docker-compose.yml
```
version: '2'

services:
  hub:
    image: selenium/hub:2.44.0
    ports:
      - "4444:4444"
    volumes:
      - ../:/src

  chrome:
    image: selenium/node-chrome-debug:2.44.0
    ports:
      - "15900:5900"
    environment:
      - HUB_PORT_4444_TCP_ADDR=hub
      - HUB_PORT_4444_TCP_PORT=4444
    volumes:
      - /dev/urandom:/dev/random
      - ../:/src
    links:
      - hub

  uploader:
    image: imneko/thesis-uploader:latest
    environment:
      LOGIN_ID: $LOGIN_ID
      LOGIN_PASS: $LOGIN_PASS
      FILE_TITLE: $FILE_TITLE
    links:
      - chrome
      - hub

```
