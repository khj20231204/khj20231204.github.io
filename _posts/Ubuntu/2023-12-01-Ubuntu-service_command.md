---
layout: single
title: 시스템 서비스 명령어
categories: Ubuntu
tag: []
---

1. # 시스템 서비스 명령어
   2. systemctl: 서비스 관리를 위해 사용되는 명령어입니다. 이 명령어를 사용하여 시스템 서비스의 시작, 중지, 다시 시작, 상태 확인 등을 수행할 수 있습니다. systemctl은 시스템의 상태를 관리하고 필요한 서비스를 제어하는데 사용됩니다.   
   
   2. service: 서비스 관리 명령어로, systemctl과 유사한 기능을 제공합니다. 서비스의 시작, 중지, 다시 시작 등을 수행할 수 있습니다. 하지만 최신 버전의 리눅스 배포판에서는 systemctl이 더 권장되는 방식입니다.   

   2. init: 시스템 초기화 및 서비스 관리를 위한 명령어입니다. 이전에 주로 사용되던 초기화 시스템으로, init 명령어를 사용하여 서비스를 제어할 수 있습니다. 하지만 최신 버전의 리눅스 배포판에서는 systemd가 기본 초기화 시스템으로 사용되므로 systemctl을 사용하는 것이 좋습니다.   

   2. chkconfig: 서비스를 부팅 시 자동으로 시작하도록 설정하거나 확인하는 명령어입니다. 다양한 리눅스 배포판에서 사용할 수 있으며, systemctl이나 service와 같은 기능을 일부 제공합니다.   

   2. sysv-rc-conf: init 시스템에서 서비스를 관리하는 텍스트 기반 도구입니다. 서비스의 부팅 시 자동 실행 여부를 설정하고 확인할 수 있습니다. 하지만 최신 버전의 리눅스 배포판에서는 systemd를 사용하므로 systemctl을 사용하는 것이 좋습니다.   

1. # systemctl 옵션
   2. start: 서비스를 시작   
   2. stop: 서비스를 중지   
   2. restart: 서비스를 다시 시작   
   2. reload: 서비스를 다시 로드   
   2. status: 서비스의 현재 상태를 확인   
   2. enable: 부팅 시 자동으로 서비스를 시작하도록 설정   
   2. disable: 부팅 시 자동으로 서비스를 시작하지 않도록 설정   
   2. mask: 서비스를 비활성화하고 관련 파일을 링크하여 수정을 방지   
   2. unmask: mask된 서비스를 다시 활성화   
   2. is-active: 서비스가 현재 활성화되어 있는지 확인   
   2. is-enabled: 서비스가 부팅 시 자동으로 시작되도록 설정되었는지 확인   
   2. is-failed: 서비스가 실패한 경우 확인   

   위의 옵션 외에도 systemctl에는 다양한 옵션이 있으며, “systemctl –help”를 실행하여 자세한 내용을 확인할 수 있습니다.