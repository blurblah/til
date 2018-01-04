# prompt
### Git clone시 password 입력할 수 있는 방법
Bitbucket의 경우 저장소가 기본적으로 private이고 clone을 하려면 key를 통해 ssh로 진행하거나 http의 경우 password 입력 필요
이 때 사용할 수 있는게 prompt인데, playbook 실행시 prompt에 기술된 문자열이 뜨면서 입력을 받고 입력된 문자열은 name으로 지정한 변수로 저장됨
Built-in으로 보이는 vars_prompt와 함께 사용하고 private 항목을 yes로 하면 입력하는 문자열이 화면에 표시되지 않고 가려짐
```yaml
- hosts: test_host
  vars:
    bitbucket_username: test_user
  vars_prompt:
    - name: bitbucket_password
      prompt: Password for bitbucket?
      private: yes
  tasks:
    - name: Clone the repository
      git:
        repo: 'http://{{ bitbucket_username }}:{{ bitbucket_password }}@bitbucket.org/test_group/test_repo.git'
        dest: '/tmp/test_repo'
```
http로 clone하면서 username과 password를 넘겨주려면 위의 예시처럼 username:password 형태로 colon으로 묶어주면 가능

# Slack notification
Ansible에 slack module이 있는데 slack의 webhook을 사용하도록 되어있음
우선 Slack에서 incoming webhook을 하나 추가하거나 존재하는 webhook에 configuration을 추가해야 함
Configuration 추가시 메세지를 전송할 channel을 지정해야 하는데 slack module에도 channel key가 존재함
Slack module의 channel을 지정하면 Slackbot으로 메세지가 들어옴
Module에서 channel을 지정하지 않고 webhook 설정을 그대로 따라가게 두면 webhook 설정대로 지정한 channel에 메세지가 전달됨
이 때, channel 별로 token이 달라지므로 playbook에서는 해당 token만 교체하면서 사용