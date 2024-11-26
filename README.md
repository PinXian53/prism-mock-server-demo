# stoplight-prism-demo
> stoplight prism: https://stoplight.io/open-source/prism

只需要在 openapi 寫好 response 的 example<br/>
就可以用 stoplight prism 將 openapi 文件變成 mock server

## 啟動 mock server (stoplight prism)
```shell
docker compose -f ./docker/docker-compose.yml -p stoplight-prism-demo up -d
```

## 測試

### 回傳 http status 200 (預設都是回傳 200)
- 指令
  ```shell
  curl --location 'http://localhost:3000/api/v1/user/add' \
  --header 'Content-Type: application/json' \
  --data '{
      "name": "Andy",
      "gender": "F",
      "age": 19
  }'
  ```
- response
  - http status: 200
  - body
    ```json
    {"code":"0","msg":"success"}
    ```
### 指定回傳的 http status
- 指令
  > header 增加 `Prefer` 參數，內容為 `code=<http-code>`
  ```shell
  curl --location 'http://localhost:3000/api/v1/user/add' \
  --header 'Prefer: code=400' \
  --header 'Content-Type: application/json' \
  --data '{
      "name": "Andy",
      "gender": "F",
      "age": 19
  }'
  ```
- response
    - http status: 400
    - body
      ```json
      {"code":"1","msg":"invalid parameter"}
      ```
