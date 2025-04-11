name: Build and Obfuscate BPB Panel

on:
  push:
    branches:
      - main
  schedule:
    # 每天凌晨1:00运行
    - cron: "0 1 * * *"

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 设置 Node.js 环境
        uses: actions/setup-node@v4
        with:
          node-version: "latest"

      - name: 安装依赖项
        run: |
          npm install -g javascript-obfuscator

      - name: 下载 BPB worker.js
        run: |
          wget -O origin.js https://raw.githubusercontent.com/bia-pain-bache/BPB-Worker-Panel/main/build/unobfuscated-worker.js

      - name: 混淆 BPB worker.js
        run: |
          javascript-obfuscator origin.js --output _worker.js \
            --compact true \
            --control-flow-flattening false \
            --dead-code-injection false \
            --identifier-names-generator mangled \
            --rename-globals false \
            --string-array true \
            --string-array-encoding 'rc4' \
            --string-array-threshold 0.75 \
            --transform-object-keys true \
            --unicode-escape-sequence true

      - name: 提交更改
        uses: stefanzweifel/git-auto-commit-action@v5
        with:
          branch: main
          commit_message: ':arrow_up: 更新最新的 BPB 面板'
          commit_author: 'github-actions[bot] <github-actions[bot]@users.noreply.github.com>'
          push_options: '--set-upstream'
