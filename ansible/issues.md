# Ansible issues
Ansible issues 확인함
그 중에서 undefined variable에 대한 [bug][issue-link] 확인
2.3.2에서는 inventory_file이라는 변수에 할당된 값이 없어도 오류 발생하지 않음
2.4.0부터는 undefined variable 오류
실제로 [문서][magic-variables-link]에는 magic variables 중에 inventory_file 존재
Ansible 실행 버전을 switch 하기 위한 편리한 방법 필요함

### Apply ansible devel branch
devel branch에서 ansible을 적용하기 위한 방법
```bash
cd ansible
source hacking/env-setup
```
코드 수정 후 make를 해서 실행파일들이 bin/ 에 반영되게 만들어야할 것으로 보임

[issue-link]: https://github.com/ansible/ansible/issues/32914
[magic-variables-link]: http://docs.ansible.com/ansible/latest/playbooks_variables.html#magic-variables-and-how-to-access-information-about-other-hosts
