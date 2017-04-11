---
layout: post
title: linux mint install(듀얼부팅)
category: Linux
---

설치 환경: 윈도우10  

준비물  
- usb(2GB 이상)  
- [UUI](https://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/#button){:target="_blank"}  
- [linux mint Cinnamon 64-bit](https://www.linuxmint.com/download.php){:target="_blank"}  

실행 순서  
1. 작업 전 bios 설정  
  a. boot mode: legacy mode  
  b. boot priority: legacy mode  
  c. usb 우선부팅  
  
2. 부팅 usb 만들기  
  a. UUI 실행  
     ㄱ. step1: select - linux mint  
     ㄴ. step2: browse - 다운받은 iso파일 선택  
     ㄷ. step3: usb드라이버 선택, format 클릭  
     ㄹ. step4: 건드릴 것 없음  
  
3. HDD(SSD) 영역 확보  
  a. 파일탐색기  
  b. 내 PC 우클릭 &rarr; 관리 &rarr; 디스크 관리  
  c. 하단 (C:) 우클릭 &rarr; 볼륨 확장 &rarr; 다음 &rarr; 공간 선택(MB): 64000 (64GB 정도면 충분)  
  
4. 설치  
  a. usb 꽂고 재부팅(자동으로 민트 실행됨)  
  b. 바탕화면의 민트 설치하기 아이콘 클릭  
  c. 설치 언어: 한국어  
  d. 키보드 - 한국어 / 한국어(101/104키 호환) (어짜피 설치 후 다시 설정 해줘야 함)  
  e. 업데이트, 서드파티 소프트웨어는 선택사항  
  f. 설치 형식 &rarr; 기타 &rarr; 다음  
  g. 드라이브 형식이 ext4인 것이 있을 것임 &rarr; 클릭  
     ㄱ. 모든 파티션은 논리 파티션으로 설정  
     ㄴ. 좌측 하단 (+)버튼 &rarr; 크기:2048mb, 용도:스왑영역  
     ㄷ. 좌측 하단 (+)버튼 &rarr; 크기:남은 영역 전부, 용도:ext4 저널링 파일 시스템, 위치:/  
     ㄹ. 부트로더 설치할 장치: ext4 저널링 파일 시스템을 설치한 장치 ex) /dev/sda3 (sda번호는 다를 수 있음)  
     ㅁ. 다음  
  h. 지역: seoul  
  i. 설치 진행 &rarr; 완료 후 usb빼고 재부팅  
  j. 만약 grub 화면(linux mint, windows 선택 화면)이 뜨지 않는다면  
    ㄱ. 인터넷연결필요  
    ㄴ. 부팅usb꽂은 상태에서 try ubuntu without install 실행  
    ㄷ. 터미널 실행  
    ㄹ. sudo add-apt-repository ppa:yannubuntu/boot-repair  
    ㅁ. sudo apt-get update  
    ㅂ. sudo apt-get install -y boot-repair  
    ㅅ. boot-repair 실행  
    ㅇ. recommended repair  
    ㅈ. 완료 후 재부팅  
  
5. 한글 입력 설정  
  a. menu → setting → languages → install/remove languages → korean → input method(languages 내의 상단 탭) →  UIM 설치 -> Input method(uim 선택)  
  b. menu → setting → keyboard → layouts → + → korean(101/104key compatible) → 상단으로 올리기  
  c. menu → uim input method → global settings → default input method:Byeoru → specify default IM(click)  
  d. menu → input method → Byeoru key bindings1 → [Byeoru] on - edit - ‘한/영'키 입력 - add - 기존의 것은 삭제  
  e. menu → input method → Byeoru key bindings1 → [Byeoru] off - edit - ‘한/영'키 입력 - add - 기존의 것은 삭제  
  f. menu → input method → Byeoru key bindings1 → [Byeoru] convert hangul to chinese characters - edit - ‘한자'키 입력 - add - 기존의 것은 삭제  
  g. 리부팅  
