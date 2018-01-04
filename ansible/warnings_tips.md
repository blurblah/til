# Variables in conditions
when 구문에서 변수는 따옴표를 포함해 이중 중괄호로 묶을 필요가 없
묶어서 사용할 경우 warning 발생
```yaml
# Warning
- name: check distribution
  fail:
    msg: "Not supported {{ ansible_distribution }}"
  when: "{{ ansible_distribution }} != 'Ubuntu'"

# Fixed
  when: ansible_distribution != 'Ubuntu'
```

# register & set_fact
Playbook에 정의된 variable을 task에서 사용할 때 **register**로 재정의가 안됨
**set_fact** module을 사용하는 경우 재정의 가능

# Warning in loop
apt module 사용시 with_items로 반복 설치하도록 해두었는데 외부에서 가져온 변수는 사용하지 말라는 warning 발생함(deprecate 예정)
이해가 잘 되지는 않지만 아래처럼 변경했더니 warning 사라짐
```yaml
# Warning
- name: Install packages
  apt: "{{ item }}"
  with_items:
    - { name: apt-transport-https }
    - { name: ca-certificates }
    - { name: curl }
    - { name: software-properties-common }
    - { name: "{{ docker_package }}" }

# Fixed
- name: Install packages
  apt: name={{ item }}
  with_items:
    - apt-transport-https
    - ca-certificates
    - curl
    - software-properties-common
    - "{{ docker_package }}"
```
