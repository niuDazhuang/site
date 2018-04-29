# travis
[![Build Status](https://www.travis-ci.org/niuDazhuang/site.svg?branch=master)](https://www.travis-ci.org/niuDazhuang/site)

> gem install travis
> touch .travis.yml

```
language: node_js
node_js:
- '8'
branchs:
  only:
  - master
install:
- npm install
script:
- npm run build
- chmod 600 ~/.ssh/id_rsa
- mv dist site && tar zcvf site.tar.gz site
addons:
  ssh_known_hosts:
  - 101.132.193.88
after_success:
- scp site.tar.gz root@101.132.193.88:/www/pc
- ssh root@101.132.193.88 -o StrictHostKeyChecking=no
  'cd /www/pc && tar zxvf site.tar.gz'
```

> travis encrypt-file ~/.ssh/id_rsa --add

```
before_install:
- openssl aes-256-cbc -K $encrypted_ee699fc33e43_key -iv $encrypted_ee699fc33e43_iv
  -in id_rsa.enc -out ~/.ssh/id_rsa -d
```
