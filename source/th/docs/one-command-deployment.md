---
title: Deployment
---
hexo สนับสนุนวิธีรวดเร็วและเรียบง่ายสำหรับ deployment คุณ deploy
เว็บไซต์ของคุณไปถึงเซร์ฟเวอร์ได้ด้วยคำสั่งบรรทัดเดียว

``` bash
$ hexo deploy
```

ก่อน deployment ครั้งแรกของคุณ คุณต้องการแก้ไขการตั้งค่าบางอย่างใน `_config
.yml`  การตั้งค่า deployment ท่ีเกิดผลได้ต้องมี field ท่ีเป็น `type`
ยกตัวอย่างเช่น:

``` yaml
deploy:
  type: git
```

คุณยังเลื่อก deployer ได้หลายตัว hexo จะ execute deployer ทุกตัวตามลำดับ

``` yaml
deploy:
- type: git
  repo:
- type: heroku
  repo:
```

Refer to the [Plugins](https://hexo.io/plugins/) list for more deployment plugins.

## Git

1. Install [hexo-deployer-git].

```bash
$ npm install hexo-deployer-git --save
```

2. Edit **\_config.yml** (with example values shown below as comments):

```yaml
deploy:
  type: git
  repo: <repository url> #https://bitbucket.org/JohnSmith/johnsmith.bitbucket.io
  branch: [branch]
  message: [message]
```

Option | Description | Default
--- | --- | ---
`repo` | URL of the target repository |
`branch` | Branch name. | `gh-pages` (GitHub)<br>`coding-pages` (Coding.net)<br>`master` (others)
`message` | Customize commit message. | `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`
`token` | Optional token value to authenticate with the repo. Prefix with `$` to read token from environment variable

3. Deploy your site `hexo clean && hexo deploy`.
  - You will be prompted with username and password of the target repository, unless you authenticate with a token or ssh key.
  - hexo-deployer-git does not store your username and password. Use [git-credential-cache](https://git-scm.com/docs/git-credential-cache) to store them temporarily.
4. Navigate to your repository settings and change the "Pages" branch to `gh-pages` (or the branch specified in your config). The deployed site should be live on the link shown on the "Pages" setting.

## Heroku

ติดตั้ง [hexo-deployer-heroku].

``` bash
$ npm install hexo-deployer-heroku --save
```

แก้ไขการตั้งค่า

``` yaml
deploy:
  type: heroku
  repo: <repository url>
  message: [message]
```

Option | Description
--- | ---
`repo`, `repository` | Heroku repository URL
`message` | Customize commit message (Default to `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`)

## Netlify

[Netlify](https://www.netlify.com/) สนับสนุน deployment ต่อเนื่องกัน
(ซึ้งสร้างด้วย git) สนับสนุน CDN แบบทั่วโลก DNS ทุกอย่าง（รวม domain
ท่ีตั้งค่าด้วยตนด้วย）HTTPS ท่ีควบคุมโดยขบวนการอัตโนมัติ
การเพิ่มความเร็วของวัตถุดิบ และสิ่งอื่นๆอีกมากมาย Netlify
เป็นแพลตฟอร์มซึ่งรวมทุกอย่างเป็นหนึ่งเดียว
ทำให้การสร้างไซต์หรือแอปของแว็บท่ีมีแระสิทธิภาพและรักษาได้ง่ายนั้นเป็นขบวนการอัตโนมัติ


 มีทั้งหมดสองวิธีในเรื่อง deploy เว็บไซต์ของตน  วิธีทั่วไปท่ีสุดคือการใช้ web
  UI คุณสามารถไปท่ี [create a new site page](https://app.netlify.com/start) และเลือก repo ของ project คุณจาก Github Gitlab หรือ Bitbucket และทำตามวิธีการใช้

วิธีท่ีสองคือ การใช้เครื่องมือ [Node based CLI](https://www.netlify.com/docs/cli/) ของ Netlify เพื่อบริหารและ deploy ไซต์บน Netlify
โดยไม่ต้องผ่าน terminal

คุณสามารถเพิ่ม [Deploy to Netlify Button](https://www.netlify.com/docs/deploy-button/) ไปถึงไฟล์ README ของคุณ ดังนั้นจะอนุญาตให้คนอื่น
copy respository ของคุณและ deploy ไปถึง Netlify ด้วยคลิกเดียว


## Rsync

ติดตั้ง [hexo-deployer-rsync].

``` bash
$ npm install hexo-deployer-rsync --save
```

แก้ไขการตั้งค่า

``` yaml
deploy:
  type: rsync
  host: <host>
  user: <user>
  root: <root>
  port: [port]
  delete: [true|false]
  verbose: [true|false]
  ignore_errors: [true|false]
```

Option | Description | Default
--- | --- | ---
`host` | Address of remote host |
`user` | Username |
`root` | Root directory of remote host |
`port` | Port | 22
`delete` | Delete old files on remote host | true
`verbose` | Display verbose messages | true
`ignore_errors` | Ignore errors | false

## OpenShift

ติดตั้ง [hexo-deployer-openshift].

``` bash
$ npm install hexo-deployer-openshift --save
```

แก้ไขการตั้งค่า

``` yaml
deploy:
  type: openshift
  repo: <repository url>
  message: [message]
```

Option | Description
--- | ---
`repo` | OpenShift repository URL
`message` | Customize commit message (Default to `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`)

## FTPSync

ติดตั้ง [hexo-deployer-ftpsync].

``` bash
$ npm install hexo-deployer-ftpsync --save
```

แก้ไขการตั้งค่า

``` yaml
deploy:
  type: ftpsync
  host: <host>
  user: <user>
  pass: <password>
  remote: [remote]
  port: [port]
  ignore: [ignore]
  connections: [connections]
  verbose: [true|false]
```

Option | Description | Default
--- | --- | ---
`host` | Address of remote host |
`user` | Username |
`pass` | Password |
`remote` | Root directory of remote host | `/`
`port` | Port | 21
`ignore` | Ignore the files on either host or remote |
`connections` | Connections number | 1
`verbose` | Display verbose messages | false

## SFTP

ติดตั้ง [hexo-deployer-sftp]. deploy ไซต์ได้โดย SFTP และใช้ password ได้ด้วย ssh-agent

``` bash
$ npm install hexo-deployer-sftp --save
```

แก้ไขการตั้งค่า

``` yaml
deploy:
  type: sftp
  host: <host>
  user: <user>
  pass: <password>
  remotePath: [remote path]
  port: [port]
  privateKey: [path/to/privateKey]
  passphrase: [passphrase]
  agent: [path/to/agent/socket]
```

Option | Description | Default
--- | --- | ---
`host` | Address of remote host |
`user` | Username |
`pass` | Password |
`remotePath` | Root directory of remote host | `/`
`port` | Port | 22
`privateKey` | Path to a ssh private key |
`passphrase` | Optional passphrase for the private key |
`agent` | Path to the ssh-agent socket | `$SSH_AUTH_SOCK`

## 21YunBox

1. ที่ [21YunBox](https://www.21yunbox.com) ให้ตั้งค่าโครงการ 'ไซต์แบบคงที่' ใหม่จาก GitHub ด้วยการตั้งค่าต่อไปนี้:

- **Build command:** `yarn && hexo deploy`
- **Publish directory:** `public`

2.กดปรับใช้บิวตัน!

แค่นั้นเอง แอปของคุณจะอยู่บน URL 21YunBox ทันทีที่สร้างเสร็จสิ้น

แอปตัวอย่างสําหรับ 'hexo' ถูกปรับใช้ที่ [https://hexo.21yunbox.com/](https://hexo.21yunbox.com/)

สําหรับรายละเอียดเพิ่มเติม โปรดทําตามคําแนะนํานี้ที่ [https://www.21yunbox.com/docs/#/deploy-hexo](https://www.21yunbox.com/docs/#/deploy-hexo)

## Other Methods

ไฟล์ท่ีต้องการ generate จะบันทึกอยู่ใน folder `public` คุณสามารถ copy
ไลฟ์เหล่านี้ไปถึงท่ีท่ีคุณอยากย้ายไป

[hexo-deployer-git]: https://github.com/hexojs/hexo-deployer-git
[hexo-deployer-heroku]: https://github.com/hexojs/hexo-deployer-heroku
[hexo-deployer-rsync]: https://github.com/hexojs/hexo-deployer-rsync
[hexo-deployer-openshift]: https://github.com/hexojs/hexo-deployer-openshift
[hexo-deployer-ftpsync]: https://github.com/hexojs/hexo-deployer-ftpsync
