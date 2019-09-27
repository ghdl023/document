---
title: 파라미터 관리 
tags: [intent, nlu, basic]
keywords: Basic Conversation
summary: 대화에서 추출한 정보나, 설정된 값을 가지고 대화흐름을 진행합니다.
sidebar: danbee_doc_sidebar
permalink: parameter.html
folder: danbeeDoc
previous: {
    title: 업데이트 로그,
    url: update_log.html
}
next: {
    title: 대화의도 관리,
    url: intent.html
}
---

{% include image.html file="intent/parameter_explain.png" %}

## 파라미터(Parameter)

**파라미터**란 사용자와의 대화에서 뽑아내는 정보를 담아내는 껍데기입니다. 변수와도 같은 개념으로 특정 값을 저장하고 대화흐름에서 사용하기위해 사용됩니다. 파라미터에는 **파라미터명**과 **엔티티**가 반드시 설정되어야합니다. 파라미터명은 변수 명, 엔티티는 변수 타입과 같은 종류로 볼 수 있습니다.

**default** 값은 아무런 정보가 들어오지 않았을 때 파라메터에 담겨있는 값입니다. 해당 값은 엔티티에 담겨 있는 값들과는 상관 없이 설정이 가능합니다.


파라미터의 종류는 크게 두가지로 나눌 수 있습니다.

- 세션 파라미터
- 챗플로우 / 이벤트 파라미터

### 챗플로우 파라미터 / 이벤트 파라미터

**챗플로우 파라미터**와 **이벤트 파라미터**는 대화흐름 시작부터 값이 생성되어 대화흐름이 끝날 때까지만 값을 유지하는 파라미터입니다. 대화흐름내에서만 필요한 정보를 담아놓고 사용할 때 이용하는 파라미터입니다. 

#### 챗플로우 파라미터
<div class="indented">챗플로우 파라미터의 경우 인텐트와 연결되어 있는 파라미터이며, 의도 추론률에 영향을 줍니다. 따라서 챗플로우 파라미터의 경우 수정은 인텐트화면에서 직접 하도록 되어있습니다.</div>

#### 이벤트 파라미터

<div class="indented">이벤트 파라미터의 경우 코드를 통해 호출되는 챗플로우에서 사용되는 파라미터로 생성과 삭제가 자유롭습니다.</div>

### 세션 파라미터

{% include image.html file="intent/parameter_testpanel.png" caption="세션 파라미터 작동 모습" %}

**세션 파라미터**는 챗플로우 완료 여부와 상관없이 사용자 세션동안 값을 계속해서 저장하고 있는 파라미터입니다. 사용자 세션의 길이는 채널별로 상이하며 채널별 정책을 확인하신 후에 챗플로우를 계획하시는 것을 추천드립니다. 세션 파라미터는 매일 새벽 3시에 일괄적으로 초기화됩니다.

----------------------------------

## 파라미터 생성

파라미터를 생성할 때는 다음과 같은 제약사항이 존재합니다.

- 파라미터명에는 띄워쓰기를 허용하지 않는다.
- 파라미터명에는 $와 _를 제외한 특수문를 허용하지 않는다.
- 파라미터명은 유일해야 한다.
- 최대 50자까지 허용한다.

Parameter 등록 방법으로는 크게 2가지가 있습니다.

- [예문에 직접 지정](intent.html#예문에서-정보-추출하기)
- 파라미터관리 패널에서 생성

예문에 직접 지정하는 경우는 "[의도 관리](intent.html#예문에서-정보-추출하기)" 챕터와 함께 보면 더 자세하게 배우실 수 있습니다. 현재 페이지에서는 설명하지 않습니다.

두 번째 경우는 대화흐름 페이지에 있는 파라미터 관리 패널을 통해 파라미터를 생성하는 방법입니다.


### 파라미터 관리 패널

{% include image.html file="intent/parameter_manager.png" %}

**파라미터 관리 패널**은 대화흐름 상세페이지에서 찾으실 수 있습니다. 
파라미터 관리 패널은 두 영역으로 나뉘어져 있으며, 챗봇 세션동안 값이 유지되는 세션 파라미터와 대화흐름 단위로 유지되는 챗플로우 파라미터 또는 이벤트 파라미터로 이루어져 있습니다.
대화의도와 연결된 챗플로우일 때는 챗플로우 파라미터를, 코드를 통해 호출되는 이벤트플로우일 때에는 이벤트 파라미터를 관리합니다.

{% include image.html file="intent/make_intent_parameter.png" caption="세션 파라미터 생성(좌), 챗플로우 파라미터 생성(우)" %}

세션 파라미터를 생성할때에는 파라미터명과 디폴트값만 설정하고, 챗플로우/이벤트 파라미터를 생성할 때에는 각각 파라미터 성격에 맞는 엔티티를 설정하도록 되어있습니다.

### 특수 Parameter

danbee.Ai에서는 다음과 같은 특수한 Parameter를 제공하고 있습니다.
(감성분석 기능은 제휴를 한 사용자를 대상으로만 서비스 됩니다.)

| Parameter명 | Entity | 기능 |
|-------------|-------------|-------------|
| positive | sys.any | 감성 분석 결과 **긍정도**를 제공 |
| negative | sys.any | 감성 분석 결과 **부정도**를 제공 |
| neutral | sys.any | 감성 분석 결고 **중립도**를 제공 |
{: .table .table-striped}

Intent에 위 Parameter들을 추가해두고  **감성분석 및 감성정보 Parameter 공유 설정**을 하시면 해당 특수 Parameter를 사용할 수 있습니다. 해당 Parameter들을 통해 대화흐름 속에서 사용자의 감성을 분석하여 긍정, 부정, 중립에 대한 정도를 수치로 제공받을 수 있습니다.<br/>

파라미터의 구체적인 활용법은 <span class="link">[대화 흐름 설명 페이지](chatflow.html)</span>에서 확인하실 수 있습니다.
