---
title: 셀레니움 탐지 기본적인 회피 코드
categories: [Python, Selenium]
tags: [Selenium,크롤링,코딩]     # TAG names should always be lowercase
---


웹사이트에서 브라우저 자동화를 덜 탐지하도록 하기 위해 Selenium WebDriver, 특히 Chrome용으로 구성하는 데 사용됩니다.

```python
chrome_options.add_argument("--disable-blink-features=AutomationControlled")
chrome_options.add_experimental_option("excludeSwitches", ["enable-automation"])
chrome_options.add_experimental_option('useAutomationExtension', False)
```

각 줄은 브라우저가 사람이 아닌 자동화된 소프트웨어에 의해 제어되고 있다는 사실을 숨기려고 합니다. 각 줄의 의미는 다음과 같습니다.


1. options.add_argument("--disable-blink-features=AutomationControlled") 

자동화된 브라우저 제어를 나타낼 수 있는 Blink 렌더링 엔진(Chrome이 구축된 엔진) 내의 특정 기능을 비활성화합니다. 

구체적으로 AutomationControlled 기능을 비활성화하여 브라우저가 웹사이트에 자신을 알리는 방식에 영향을 미치고 웹사이트가 자동화를 탐지하는 일부 방법을 회피할 수 있습니다.

1. options.add_experimental_option("excludeSwitches", ["enable-automation"]) 

일반적으로 Selenium이 Chrome을 제어할 때 "자동화" 플래그와 함께 브라우저를 시작합니다. 

이는 페이지의 JavaScript를 통해 특정 속성(예: navigator.webdriver)으로 탐지될 수 있습니다. 이 줄은 Chrome이 이 플래그 없이 시작하도록 지시하여 세션이 자동화 도구에 의해 제어되고 있음이 웹사이트에 덜 명확하게 합니다.

3. options.add_experimental_option("useAutomationExtension", False)  

Chrome이 자동화 테스트 환경에서 일반적으로 로드되는 확장 프로그램을 로드하지 못하게 합니다. 

이 확장 프로그램은 특정 자동화 기능을 제공하지만 브라우저가 소프트웨어에 의해 제어되고 있음을 웹사이트에 명확하게 보여줍니다. 이를 비활성화하면 탐지 가능성이 줄어듭니다.

