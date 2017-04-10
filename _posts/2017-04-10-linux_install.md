---
layout: post
title: linux mint install
---

### 듀얼부팅으로 linux mint를 실행하는 방법
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
    step1: select - linux mint  
    step2: browse - 다운받은 iso파일 선택  
    step3: usb드라이버 선택, format 클릭  
    step4: 건드릴 것 없음  
3. HDD(SSD) 영역 확보
4. 설치  
  a. usb 꽂고 재부팅(자동으로 민트 실행됨)  
  b. 바탕화면의 민트 설치하기 아이콘 클릭  
  c. 설치 언어: 한국어  
  d. 키보드 - 한국어 / 한국어(101/104키 호환) (어짜피 설치 후 다시 설정 해줘야 함)  
  e. 업데이트, 서드파티 소프트웨어는 선택사항  
  f. 설치 형식 &rarr; 기타 &rarr; 다음  
  g. 드라이브 형식이 ext4인 것이 있을 것임 &rarr; 클릭  
     모든 파티션은 논리 파티션으로 설정  
     ii. 좌측 하단 (+)버튼 &rarr; 크기:2048mb, 용도:스왑영역  
     iii. 좌측 하단 (+)버튼 &rarr; 크기:남은 영역 전부, 용도:ext4 저널링 파일 시스템, 위치:/  
     iv. 부트로더를 설치할 장치: 위의 ext4 저널링 파일 시스템을 설치한 장치 ex) /dev/sda3 등의 이름(설치 환경마다 sda번호는 다를 수 있음)  
     v. 다음  
  h. 지역: seoul  
  i. 설치 진행 &rarr; 완료 후 usb빼고 재부팅  
  j. 만약 grub 화면(linux mint, windows 선택 화면)이 뜨지 않는다면 &rarr; [grub오류해결](link)
5. 한글 입력 설정  
  a.   

5. sadf
6. sadf 
7. sadf
8. sadf
9. sadf
10. sadf
11. sadf
