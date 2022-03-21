---
title: GitHub에 GPG 서명 등록하기 (macOS)
date: 2018-10-24
update: 2020-01-31
tags:
  - github
keywords:
  - github gpg
  - github gpg key
  - gpg 키 생성
  - gpg 키
  - gpg 서명
---

## 설치

우선 Homebrew 를 통해 gpg 패키지를 설치한다,

```shell
$ brew install gpg
```

추가로 gpg 키 관리 프로그램인 GPG-SUITE를 설치한다.

```shell
$ brew cask install gpg-suite
```

## key 생성

키 생성 방법은 두가지가 있다.

1. gpg-suite를 통한 설치
2. 터미널내에서 설치

1번의 경우 시스템 환경설정에서 확인 할 수 있는 GPG KeyChain을 통해 생성하는 방법이다.  
본 글에서는 터미널에서 생성하는 방법을 소개하고 있기 때문에 1번의 방법은 [링크](https://medium.com/@star_zero/github%E3%81%AEgpg-key%E3%82%92%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B-70e22874e533)를 확인해 보시기를 바란다.

아래는 터미널에서 키를 생성하는 과정이다.

우선 아래 명령어를 이용 키 생성 과정에 들어간다.

```shell
$ gpg --full-generate-key
```

아래 자세한 생성하는 과정이 나와있고, 간단히 요약하면 이러하다.

- 암호화 방식 선택 (권장: 1)
- 암호화 키 크기 선택 (권장: 4096)
- 키 유효기간 설정 (권장: 0) // Enter 입력하여 패스
- 이름, 이메일, 코멘트(공란 가능) 입력
- 이후 보안 암호 문구 작성 창에서 암호 입력 (이후 첫 commit시 입력하는 암호로 쓰인다)

```shell
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 1


RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 4096


Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)


GnuPG needs to construct a user ID to identify your key.

Real name: Junho Baik
Email address: junhobaik@gmail.com
Comment:
You selected this USER-ID:
    "Junho Baik <junhobaik@gmail.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
```

위의 과정을 마치고 나면 키가 생성되었고,

이제 아래 명령어(`gpg --list-secret-keys --keyid-format LONG`)를 이용하여 생성한 키를 확인한다.

```shell
$ gpg --list-secret-keys --keyid-format LONG

-----------------------------------
sec   rsa4096/ABCDE12345678900 2018-10-24 [SC]
      AFWAEGWEGWAEDVADKAWGJIWRGLWJRGAIWALGRHRG
uid                 [ultimate] Junho Baik <junhobaik@gmail.com>
ssb   rsa4096/AGRJIWGJWRGJIRWG 2018-10-24 [E]
```

위의 예제에서 `ABCDE12345678900`에 해당하는 부분을 복사하고 아래 명령어에 넣는다.

```shell
$ gpg --armor --export ABCDE12345678900
```

위 명령어를 입력한 후 출력되는 키를 복사한다,  
`-----BEGIN PGP PUBLIC KEY BLOCK-----`부터 `-----END PGP PUBLIC KEY BLOCK——.`를 포함해서 모두 복사하여야 한다.

## GitHub 에 GPG Key 등록

GitHub - Settings - [SSH and GPG keys](https://github.com/settings/keys)

위의 메뉴로 진입하여 GPG Keys 부분의 new GPG key 버튼을 클릭하고 복사한 키를 등록한다.

## Git 에 GPG Key 등록

아래 명령어를 통해 `~/.gitconfig`에 gpg 정보를 입력한다.

여기서 `ABCDE12345678900`에 해당하는 것은 위에서 확인한 Key 부분이며, 본인의 것을 입력한다.

```shell
$ git config --global user.signingkey ABCDE12345678900
$ git config --global gpg.program $(which gpg)
```

이제 등록이 되었고, 이후 commit 부터는 `-S` 플래그를 넣음으로 서명을 적용한 Commit 을 보낼 수 있다.

```shell
$ git commit -S
```

아래 명령어를 이용하면 `-S` 플래그를 번번히 넣지 않아도 항상 서명이 적용한 Commit 을 보내게 된다.

```shell
$ git config --global commit.gpgsign true
```

추가로 commit 시 오류가 발생한다면, 아래 내용을 `~/.zshrc` 또는 `~/.bashrc`에 추가해준다.

```
export GPG_TTY=$(tty)
```

추가로 가끔씩 물어보는 GPG 패스워드를 묻지 않길 원하면 `~/.gnupg/gpg-agent.conf` 파일을 수정한다.

```
default-cache-ttl 31536000
maximum-cache-ttl 31536000
```

GPG2.1 이후에서는 `maximum-cache-ttl`이 `max-cache-ttl`로 바뀌었으니 버전에 따라 다르게 입력해주어야 한다.  
보통 처음 gpg-agent.conf 파일을 열었을때 두 값이 있으므로 어떤 값으로 써야할 지 알 수 있다. 하지만 알 수 없을 경우 버전을 확인하여 올바른 값을 입력해야한다.  
31536000는 1년에 해당하는 초(sec)값이다.

---

### References

- [Generating a new GPG key](https://help.github.com/articles/generating-a-new-gpg-key/)
- [KenjiAbe|GitHub の GPG Key を設定する](https://medium.com/@star_zero/github%E3%81%AEgpg-key%E3%82%92%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B-70e22874e533)
- [Keep GnuPG credentials cached for entire user session](https://superuser.com/questions/624343/keep-gnupg-credentials-cached-for-entire-user-session)
