---
license: >
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
---

# Windows Phone 플랫폼 가이드 8

이 가이드에서는 Windows Phone 8 장치에 대 한 코르도바 애플 리 케이 션을 배포 하기 위해 SDK 개발 환경을 설정 하는 방법을 보여 줍니다. 7.5 및 8 장치를 타겟팅 하려는 경우 대신 Windows Phone 7 플랫폼 가이드 상세한 Windows Phone 7 개발. 버전 7 인터넷 익스플로러 10에 포함 된 모든 고급 기능을가지고 있지 않습니다 하지만 동일한 Api 집합을 구현 합니다. Windows Phone 8 애플 리 케이 션 *하지* Windows Phone 7 장치에서 실행.

두 버전 모두에 적용 되는 자세한 플랫폼 관련 정보에 대 한 다음 참조.

*   Windows Phone 업그레이드
*   Windows Phone 플러그인
*   Windows Phone 명령줄 도구

위의 명령줄 도구 코르도바 3.0 이전 버전을 참조 하십시오. 현재 인터페이스에 대 한 내용은 명령줄 인터페이스를 참조 하십시오.

## 시스템 요구 사항

*   운영 체제:
    
    *   윈도우 8 또는 윈도우 8 프로 
        *   Windows의 64 비트 버전 (64)가 SDK에 대 한 필요 합니다.
        *   장치 에뮬레이터를 실행할 수 있도록, 프로 버전에 것이 좋습니다.

*   하드웨어:
    
    *   6.5 G B의 하드 디스크 여유 공간
    *   4 기가바이트 램
    *   64 비트 (x64) CPU

*   Windows Phone 에뮬레이터 8
    
    *   그래서이 목록에 포함 되어 그 필수 전화 에뮬레이터 하이퍼-V를 사용 합니다.
    *   윈도우 8 프로 64 비트 버전 또는 더 큰
    *   가상화를 지 원하는 프로세서를 요구 하 고 [두 번째 수준의 주소 변환 (판금)][1] 
        *   [인텔 프로세서를 지원 하려면 VT-x (가상화) EPT (판금) 목록][2] 참조
    *   일반적으로이 기본적으로 비활성화 되어 BIOS 설정에서 가상화 기능 (인텔에 즉, VT-x) 사용.

*   SDK 및 IDE (Visual Studio)
    
    *   비주얼 스튜디오 2012 전문가, 프리미엄, 또는 궁극. Note Visual Studio Express에 대 한 Windows Phone (SDK에 포함)은 권장 하지 않습니다 VS 익스프레스 서식 파일 (아래 참조)를 구축 하지 수 있기 때문에 VS 프로에서 서만 또는 더 높은 **템플릿 내보내기** 기능을 필요 하지 않습니다.

*   등록 및 실제 장치에 응용 프로그램을 설치 하거나 시장 장소에 그것을 제출 하는 경우 [Windows Phone 개발 센터][3] 계정에 대 한 지불.

 [1]: http://en.wikipedia.org/wiki/Second_Level_Address_Translation
 [2]: http://ark.intel.com/Products/VirtualizationTechnology
 [3]: http://dev.windowsphone.com/en-us/publish

**참고**: 가상 컴퓨터에서 SDK를 실행 몇 가지 도전을 제시 수도 있습니다. [Mac에서 Windows Phone][4] 에 대 한 개발 솔루션에 통찰력을 제공이 블로그에 게시물을 읽을 수 있습니다..

 [4]: http://aka.ms/BuildaWP8apponaMac

## SDK 및 코르 도우 바 설치

다운로드 하 고 [Windows Phone SDK][5] 설치.

 [5]: http://www.microsoft.com/en-us/download/details.aspx?id=35471

다운로드 및 [코르도바][6]의 최신 복사본을 추출 합니다. `lib\windows-phone-8\wp8`하위 디렉터리는 작업을 수행 해야 합니다.

 [6]: http://phonegap.com/download

복사는 `CordovaWP8_x_x_x.zip` 파일은 `\My Documents\Visual
Studio 2012\Templates\ProjectTemplates\` 디렉터리.

## 서식 파일 작성

**참고**: 경우이 단계를 건너뛰고는 `lib\windows-phone` 디렉터리에 이미 포함 되어 있는 `CordovaWP8_x_x_x.zip` 파일.

개발을 간소화 하기 위해 코르 도우 바 Visual Studio 템플릿을 빌드하는 스크립트를 묶는다. 이들은 빠르게 코르도바 애플 리 케이 션을 생성 하 고 필요한 경우 수정할 수 있습니다. 아래 단계에는 그것을 생성 하는 방법을 보여 줍니다.

### 설치 된 서식 파일을 만들고 배치 파일을 실행

Repo의 루트 디렉터리에 있는 `createTemplates.bat` 파일. 이것 두 생성을 두 번 클릭 `.zip` 파일: `CordovaWP7_x_x_x.zip` 및 `CordovaWP8_x_x_x.zip` , 여기서 *x.x.x* 는 현재 버전 번호. 쉽게 Visual Studio에서에서 이러한 파일을 사용 하 여 복사를 `My
Documents\Visual Studio 2012\Templates\ProjectTemplates\` . 당신은 다음 **Visual Studio 파일 → 새 프로젝트** 메뉴에서 새로운 아파치 코르도바 Windows Phone 응용 프로그램을 만들 수 있습니다.

명령줄에서 배치 파일을 실행 하면 자동으로 설치 하도록 매개 변수 또한 호출할 수 있습니다.

        > createTemplates.bat-설치
    

## 새 프로젝트 설정

Visual Studio Express에 대 한 Windows Phone 열고 **새 프로젝트** 선택.

**CordovaWP8**를 선택 합니다. 버전 번호는 서식 파일 설명에 표시 됩니다.

프로젝트에 이름을 하 고 **확인** 을 선택 합니다.

![][7]

 [7]: img/guide/platforms/wp8/StandAloneTemplate.png

## 프로젝트 구조를 검토

`www`디렉터리 기능 `html` , `js` , 및 `css` 하위 디렉터리 및 다른 리소스 응용 프로그램 요구 한다. 모든 추가 콘텐츠 Visual Studio 프로젝트의 일부가 될 필요가 있고 내용으로 설정 해야 합니다.

2.3.0는 다음 샘플 구조 대표 프로젝트, 하지만 설치 된 버전에 따라 다를 수 있습니다.

![][8]

 [8]: img/guide/platforms/wp8/projectStructure.png

## 빌드하고 에뮬레이터에 배포

**Windows Phone 에뮬레이터** 주요 드롭 다운 메뉴에 선택 되어 있는지 확인 합니다.

다음 디버깅을 시작 하려면 드롭 다운 메뉴 옆에 있는 녹색 **재생** 버튼을 누르거나 **f5 키** 를 입력합니다.

![][9]

 [9]: img/guide/platforms/wp8/BuildEmulator.png

## 장치에 대 한 프로젝트를 구축

장치에서 응용 프로그램을 테스트 하기 전에 장치를 등록 해야 합니다. 배포 하 고 Windows Phone 8에서 테스트 하는 방법에 대 한 자세한 내용은 [Microsoft의 설명서][10] 를 참조 하십시오. 다음은 기본적인 단계입니다.

 [10]: http://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402565(v=vs.105).aspx

*   귀하의 휴대 전화 연결 되어 있으며 화면 잠긴 ㄴ 다는 것을 확인 하십시오.

*   Visual Studio에서 상단에 드롭 다운 메뉴에서 **장치** 를 선택 합니다.

*   디버깅을 시작 하려면 주요 드롭 다운 메뉴 옆에 있는 녹색 **재생** 버튼을 눌러 또는 다른 **f5 키** 입력.

![][11]

 [11]: img/guide/platforms/wp7/wpd.png

이 시점에서, 당신이 끝났습니다.

## 더 읽기

Windows Phone 개발자 블로그 IE10 웹 킷 브라우저와 모두를 지 원하는 방법에 차이에 [유용한 정보][12] 를 제공 합니다.

 [12]: http://blogs.windows.com/windows_phone/b/wpdev/archive/2012/11/15/adapting-your-webkit-optimized-site-for-internet-explorer-10.aspx