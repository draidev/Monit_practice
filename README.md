# Monit

## monit이란?
ChatGPT
모니트(Monit)는 유닉스(Unix) 및 리눅스(Linux) 시스템을 모니터링하고 관리하는 데 사용할 수 있는 오픈 소스 유틸리티입니다. 시스템 관리자가 일반적인 시스템 문제의 모니터링과 수리를 자동화하여 전반적인 시스템 건강상태와 성능을 보장하도록 설계되었습니다.   

다음은 모니트의 주요 기능 및 이점입니다   

- 시스템 자원 모니터링: 모니트는 CPU 사용량, 메모리 사용량, 디스크 공간 등의 시스템 자원을 모니터링하고 일정 임계값을 초과하면 조치를 취할 수 있습니다. 이를 통해 자원 고갈 및 성능 저하를 방지하고 중요한 서비스의 가용성을 보장할 수 있습니다.     
- 자동 문제 감지 및 수리: 모니트는 프로세스 충돌, 메모리 누수 및 기타 성능 문제와 같은 일반적인 시스템 문제를 감지하고 자동으로 수리할 수 있습니다. 이를 통해 다운 타임을 최소화하고 시스템 안정성을 보장할 수 있습니다.   
- 사용자 정의 가능한 경고 및 알림: 모니트는 특정 조건이 충족되면 경고 및 알림을 보내도록 구성할 수 있습니다. 이를 통해 시스템 관리자가 시스템에 영향을 미칠 수 있는 문제를 인식하고 조치할 수 있도록 보장합니다.   
- 유연하고 사용자 정의 가능: 모니트는 Linux, Unix, macOS 및 Windows와 같은 다양한 플랫폼을 지원하며 매우 유연하고 사용자 정의 가능합니다. 웹 인터페이스나 구성 파일을 통해 구성할 수 있으며 Nagios 및 Zabbix와 같은 다른 도구와 통합하여 더욱 고급 모니터링 및 경고 기능을 제공할 수 있습니다.   
- 사용이 쉽습니다: 모니트는 쉽게 사용할 수 있도록 설계되어 최소한의 구성만으로 시작할 수 있습니다. 웹 인터페이스는 시스템을 구성하고 모니터링하는 간단하고 직관적인 방법을 제공하여 기술적인 전문 지식 수준에 따라 사용자가 액세스할 수 있습니다.    

전반적으로, Monit은 시스템 관리자가 시스템을 원활하게 유지하고 서비스의 높은 가용성을 보장해야 하는 경우 강력하고 유용한 도구입니다. 일반적인 시스템 문제의 모니터링과 자동 복구를 자동화함으로써 Monit은 다운 타임을 최소화하고 시스템의 안정성을 보장하는 데 도움이 되며, Unix 또는 Linux 시스템에 의존하는 모든 조직에게 필수적인 도구입니다.   

---

## monit 사용법   
- monit의 기본 설정 파일은 ```/etc/monit/monitrc```에 있다.   
- log는 ```/var/log/monit.log```에 쌓인다.   
- 기본 설정 파일(monitrc)에서 ```/etc/monit/conf.d```폴더의 모든 파일을 include한다.   
	- ```include /etc/monit/conf.d/*```   

## daemon config 만들기   
- ```/var/run/[process name].pid```파일이 생성되는 것으로 프로세스가 돌고 있는 것을 확인한다. ```.pid```파일 안에는 pid번호가 쓰여있다.   

- Debian 계열(Ubuntu)   
	- vi /etc/monit/conf.d/[process name]   
	```
	# docker의 process 확인을 pidfile로 한다   
	check process docker with pidfile /var/run/docker.pid   
	start program = "/etc/init.d/docker start"   
	# stop program = "/etc/init.d/systemctl stop"   
	```   
- RedHat 계열(CentOS)   
	- vi /etc/monit.d/[process name]
	```
	check process docker with pidfile /var/run/docker.pid   
    start program = "/usr/bin/systemctl start docker"   
    # stop program = "/usr/bin/systemctl stop docker"   
	```   
	
