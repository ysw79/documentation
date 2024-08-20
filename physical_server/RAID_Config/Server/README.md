# 서버 세팅

## 1. BIOS 세팅

### 1.1 BIOS 진입

![이미지](images/01.png)
위 화면에서 DEL키를 연타

![이미지](images/02.png)
기본 password는 서버에 부착된 라벨에 기입되어 있음 ("\***\*\*\*\*\***")

![이미지](images/03.png)
통과

![이미지](images/04.png)
**Device Manager**로 진입

![이미지](images/05.png)
**BROADCOM <MegaRAID ...> Configuration Utility...** 를 선택한다.

### 1.2 기존 세팅 초기화

- 기존에 리눅스 설치나 RAID 설정 등 이미 세팅한 바가 있다면 초기화한다.
- 해당사항이 없거나 서버 개봉 후 첫 설치라면 이 과정은 PASS.

![이미지](images/06.png)
**Main Menu** 선택

![이미지](images/07.png)
**Configuration Management** 선택

![이미지](images/08.png)
**Clear Configuration**으로 설정 초기화

![이미지](images/09.png)
**Confirm**에서 엔터를 눌러 Enabled로 전환시켜준다.

![이미지](images/10.png)
한번 더 확인을 거친다. **Yes** 선택

![이미지](images/11.png)
초기화가 성공적으로 끝났다는 메세지가 뜬다.
**OK**를 누른 후 **ESC** 키를 눌러 빠져나간다.

![이미지](images/12.png)
한번 더 **ESC**

![이미지](images/13.png)
설정이 제대로 초기화되었는지 확인하자.
**드라이브 관리자**로 진입한다.

![이미지](images/14.png)
디스크들이 Unconfigured 상태로 전환되었는지 확인한다.
**ESC**키를 눌러 **Main Menu**로 돌아간다.

### 1.3 RAID 설정

![이미지](images/06.png)
**Main Menu** 선택

![이미지](images/15.png)
**Configuration management**로 진입

![이미지](images/16.png)
**Create Virtual Drive**로 진입

![이미지](images/17.png)
**Select RAID Level**에 들어가서 RAID5로 전환해준다.  
RAID 번호는 새 프로젝트의 형태나 서버의 드라이브 구성에 따라 변경될 수 있다.

![이미지](images/18.png)
아래아래의 **Select Drives**로 진입

![이미지](images/19.png)
현재 서버에 탑재되어 있는 드라이브들이 나열된다(현재 화면에서는 총 8개).  
여기서는 7개의 드라이브를 RAID로 묶고 1개의 드라이브는 핫스페어로 운용할 예정이다.  
따라서 위와 같이 7개는 Enabled로 설정하고 나머지 1개는 그대로 둔다.

설정한 사항은 반드시 저장해야 반영이 된다. 최상단 혹은 최하단의 **Apply Changes**를 선택.

![이미지](images/20.png)
**OK**

![이미지](images/21.png)
**ESC**로 빠져나온다.

![이미지](images/22.png)
설정을 저장하기 위해 **Save Configuration**을 선택

![이미지](images/23.png)
**Yes**

![이미지](images/24.png)
**OK**

![이미지](images/25.png)
**ESC**로 빠져나온 후 **Drive Management**로 들어가 확인해보면

![이미지](images/26.png)
7개의 드라이브는 Online, 마지막 1개는 Unconfigured 상태일 것이다.

![이미지](images/27.png)
마지막 1개를 핫스페어로 설정하기 위해 선택

![이미지](images/28.png)
**Operation** 선택

![이미지](images/29.png)
**Spare Drive Assign Global**로 변경한다.

![이미지](images/30.png)
**Go**를 선택해줘야 적용된다.

![이미지](images/31.png)
**ESC**를 눌러 빠져나가면

![이미지](images/32.png)
위와 같이 변경되었다면 성공이다.

--

## 2. Rocky9 설치

### 2.1 USB로 부팅하기

여기서는 USB로 설치하는 것으로 가정한다.  
Rocky9 이미지가 담긴 USB를 서버에 연결 후 아래 과정을 실행한다.

![이미지](images/50.png)
최상단으로 빠져나와서 **Boot Manager**로 진입한다.

![이미지](images/51.png)
**Other Devie**의 **USB**를 선택한다.
곧바로 재부팅된다.

### 2.2 Rocky9 설치

![이미지](images/43.png)
첫번째 혹은 두번째 중 아무거나 선택한다.

![이미지](images/33.png)

![이미지](images/35.png)
Time & Date 등을 설정하고 네트워크 설정으로 이동한다.  
! **Installation Destination** 외 다른 설정들은 install 완료 후 Rocky9에 들어가서 설정해도 무방하다.

![이미지](images/34.png)
네트워크 설정에서

![이미지](images/36.png)
두번째 항목 **Ethernet(ens65f0)**을 활성화한다.

오른쪽 하단의 **Configure** 버튼을 클릭하고

![이미지](images/37.png)
IPv6 Settings는 **Disabled**를

![이미지](images/38.png)
IPv4 Settings에서는 **Manual**을 선택

![이미지](images/39.png)
그 후 서버 IP, 서브넷 마스크, Gateway를 설정하고 **Save**한다.

![이미지](images/40.png)
왼쪽 상단의 **Done**을 클릭하여 빠져나온다.

![이미지](images/62.png)
**Installation Destination**을 클릭하여 설치 디스크 세팅으로 들어간다.

![이미지](images/42.png)
RAID로 묶어놓은 드라이브를 선택하고

![이미지](images/44.png)
하단에서 **Custom**으로 변경 후 **Done**을 클릭하면

![이미지](images/46.png)
수동 파티션 설정이 뜨는데, Rocky Linux 9.3 for x86_64 부분의 ">"를 클릭하여 펼친다.

![이미지](images/55.png)
디폴트로 생성되는 home 파티션을 삭제하고 루트 디렉토리로 모든 용량을 몰아주자.
home 디렉토리를 선택후 하단에서 **-** 버튼을 클릭하여 파티션을 삭제한다.

![이미지](images/56.png)
루트 디렉토리를 다시 생성하고 남은 용량을 모두 할당하기 위해 루트 디렉토리도 제거한다.

![이미지](images/57.png)
home과 루트 디렉토리 모두 제거한 상태.

![이미지](images/61.png)
swap 용량은 "1024 GiB"로 수정한다. (일반적으로 서버 램 용량과 동일하게 맞춘다고 한다)

![이미지](images/58.png)
**+** 버튼을 클릭해서 "/" 디렉토리를 생성한다.

![이미지](images/59.png)
Desired Capacity에 남은 전체 용량이 할당되었는지 확인한다.

![이미지](images/62.png)
**Done**을 눌러 빠져나온다.  
아까와 다르게 **Installation Destination**에 경고 메시지가 없어져 있는 것을 볼 수 있다.

이제 Root 계정의 비밀번호를 변경해주고 User 계정을 차례로 생성해준다.

![이미지](images/63.png)
![이미지](images/64.png)
Root 계정의 비밀번호를 설정해준다.

![이미지](images/67.png)
이어서 User 계정도 생성해준다.

![이미지](images/66.png)
Begin Installation을 클릭하여 Rocky9 설치를 진행한다.

-- 끝 --
