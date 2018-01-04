# Ansible task import 기능
Ansible에서 다른 파일에 기술된 task를 불러오기 위해서 기존에는 include 만으로 가능
include가 deprecated 되면서 import_tasks or include_tasks를 사용해야 함 (2.4 이후)
import_tasks와 include_tasks 모두 불러올 yml 파일만 지정하면 됨
import_tasks는 static, include_tasks는 dynamic이라고 기술되어 있음
불러올 yml 파일명에 variable이 사용된 경우 import_tasks를 이용하면 오류 발생
Variable이 사용된 경우 동적으로 변경되기 때문에 include_tasks를 사용해야만 한다.