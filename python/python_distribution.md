# Python Distribution

### Package
Package로 만들기 위해서 `__init__.py` 파일이 root에 있어야 하고 하위 모듈도 인식될 수 있도록 없다면 추가

### PyPI에 가입
https://pypi.python.org 에 가입이 되어있어야 한다.

### setup.py 생성
Distribution package에 대한 정보를 setup.py의 setup() 함수에 기술한다.
상세 내용은 [Distributing packages 문서][distributing-packages-link] 참조.
실제 사용된 예제는 [setup.py][ec2ss-setup-link].
이 때 package가 아니라 실행 스크립트 자체도 배포하고 싶다면 scripts 항목에 파일들을 추가해줘야 한다.

### setuptools, wheel 설치
이미 설치된게 없다면 pip로 설치해준다.

### twin 설치
Package upload를 위한 twin을 pip로 설치한다.

### Packaging
setup.py 파일이 있는 root 경로에서 아래의 command를 실행한다.
```bash
python setup.py bdist_wheel
```

### Upload
Packaging이 되면 dist 경로에 whl 파일이 생성되는데 새로 packaging 된 파일을 twine으로 업로드한다.
```bash
twine upload dist/PACKAGED_WHL_FILENAME
```

[distributing-packages-link]: https://packaging.python.org/tutorials/distributing-packages/
[ec2ss-setup-link]: https://github.com/blurblah/ec2_start_stop/blob/master/setup.py