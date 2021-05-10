2021-05-10-使用Github-Action自動部署Jekyll專案.md
- copy chirpy專案的tool還有創建.yml
- 使用以下指令安創建linux平台的bundle lock
```
bundle lock --add-platform ruby
bundle lock --add-platform x86_64-linux
```
- add gem 'html-proofer'