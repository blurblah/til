# Ansible compile test
[Dev guide][devguide-link] 참조
compile, sanity test 모두 2.6, 2.7, 3.5, 3.6 버전에서 테스트하도록 되어있음
특정 버전 대상으로 테스트하고 싶다면 `--python VERSION` option 사용

### Multiple python version
[pyenv][pyenv-repo]를 설치하면 여러개의 python version을 설치하고 관리할 수 있음
아래는 간단한 사용법

```bash
# list to install
pyenv install --list
# install a specific version
pyenv install 3.6.3
# show installed versions
pyenv versions
# change to a specific version
pyenv shell 3.6.3
```
shell subcommand 실행시 오류가 발생하기 때문에 아래와 같은 구문을 .profile에 넣어줘야 함
```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"

if command -v pyenv 1>/dev/null 2>&1; then
    eval "$(pyenv init -)"
fi
```
pyenv로 특정 python version 설치시 ssl 부분에서 오류가 발생한다면 아래처럼 설치
[Common build problem][common-build-problems-link] 참조
```bash
CFLAGS="-I$(brew --prefix openssl)/include" \
LDFLAGS="-L$(brew --prefix openssl)/lib" \
pyenv install -v 3.4.3
```

[pyenv-repo]: https://github.com/pyenv/pyenv#installation
[devguide-link]: http://docs.ansible.com/ansible/latest/dev_guide/testing.html
[common-build-problems-link]: https://github.com/pyenv/pyenv/wiki/Common-build-problems#error-the-python-ssl-extension-was-not-compiled-missing-the-openssl-lib
