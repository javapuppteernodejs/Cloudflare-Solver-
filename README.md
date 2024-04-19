# How to solve cloudflare turnstile and challange 5s in 2024 | Best Cloudflare solver
![](https://assets.capsolver.com/prod/images/post/2024-04-19/ee96165e-e325-42b9-8d55-2cbd41358c2e.png)



Cloudflare, a popular security and performance solution, employs various protection mechanisms, including Turnstile and Challenge 5s, to safeguard websites from malicious activity. However, as a web user or developer, encountering these security measures can sometimes be a hindrance. This article will guide you through effective methods and discuss the best Cloudflare solvers to overcome Cloudflare Turnstile and Challenge 5s in 2024.

## Bonus Code
 A bonus code for top captcha solutions; [CapSolver](https://www.capsolver.com/): **WEBS**. After redeeming it, you will get an extra 5% bonus after each recharge, Unlimited

![](https://assets.capsolver.com/prod/images/post/2024-03-29/fbc29472-886c-45b2-9eb2-2b307f6d9700.png)

## Understanding Cloudflare Turnstile
Cloudflare Turnstile is a free tool that aims to replace CAPTCHAs. By implementing a simple snippet of code, Turnstile provides website visitors with a hassle-free browsing experience, free from CAPTCHA challenges. It effectively prevents abuse and verifies the authenticity of visitors without compromising data privacy or subjecting them to the unpleasant user experience associated with CAPTCHAs. With Turnstile, websites can offer a more seamless and enjoyable interaction for their users.

## Turnstiles types Supported by CapSolver
Introducing [CapSolver](https://www.capsolver.com/) - The Ultimate Automated CAPTCHA Solver:
CapSolver emerges as the leading automated CAPTCHA solver, offering unparalleled capabilities in solving CAPTCHAs. With its state-of-the-art automation techniques and robust infrastructure, CapSolver ensures accurate and efficient CAPTCHA solving, making it the ideal choice for tackling Turnstile and other CAPTCHA challenges in 2024 and beyond.

![](https://assets.capsolver.com/prod/images/post/2023-05-13/254a86e2-c054-4c42-9b57-5c219af2a3f8.gif)

The Turnstile/Challenge verification code is another attempt to replace reCaptcha/hCaptcha.CapSolver automatically support all of its subtypes:
- Manually
- Non-Interactive
- Invisible


## How to solve cloudflare turnstile
Next we'll cover then solving Cloudflare Turnstile by means of a token. In the beginning, there is no need to specify subtypes during your call. It is not necessary to provide your own custom `User-Agent` yet,
Lets  ignore this parameter.


The task type `type` is as follows

- `AntiTurnstileTaskProxyLess`

### Step 1 Create the task

Create the task with the [createTask](../api-createtask.md).

In the process of using turnstile, we must input `websiteURL` and `websiteKey`, other parameters are optional.

#### Task Object Structure

| Properties     | Type               | Required | Description                                                  |
| -------------- | ------------------ | -------- | ------------------------------------------------------------ |
| type           | String             | Required | `AntiTurnstileTaskProxyLess`                                 |
| websiteURL     | String             | Required | The address of the target page.                              |
| websiteKey     | String             | Required | Turnstile website key.                                       |
| metadata       | Map<String,String> | Required | Turnstile extra data . [Turnstile Documentation](https://developers.cloudflare.com/turnstile/get-started/client-side-rendering/) |
| metadata.acton | String             | Optional | The value of the `data-action` attribute of the Turnstile element if it exists. |
| metadata.cdata | String             | Optional | The value of the `data-cdata` attribute of the Turnstile element if it exists. |

#### **Example Request**

```txt
POST https://api.capsolver.com/createTask
Host: api.capsolver.com
Content-Type: application/json
```

```json lines
{
  "clientKey": "YOUR_API_KEY",
  "task": {
    "type": "AntiTurnstileTaskProxyLess",
    "websiteURL": "https://www.yourwebsite.com",
    "websiteKey": "0x4XXXXXXXXXXXXXXXXX",
    "metadata": {
       "action": "login",  //optional
       "cdata": "0000-1111-2222-3333-example-cdata"  //optional
    }
  }
}
```

#### Example Response

```json lines
{
  "errorId": 0,
  "status": "idle",
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"   // record taskId
}

```

### Step 2  **Getting Result**

Use the [getTaskResult](../api-gettaskresult.md) method to get the recognition results

Depending on the system load, you will get the results within the interval of `1s` to `20s`

#### **Example Request**

```txt
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json
```

```json lines
{
  "clientKey": "YOUR_API_KEY",
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"
}
```

#### Example Response

```json lines
{
  "errorId": 0,
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006",
  "status": "ready",
  "errorCode": null,
  "errorDescription": null,
  "solution": {
    "token": "0.mF74FV8wEufAWOdvOak_xFaVy3lqIDel7SwNhw3GgpICSWwTjYfrQB8mRT1dAJJBEoP7N1sESdp6WH9cTS1T0catWLecG3ayNcjwxVtr3hWfS-dmcBGRTx4xYwI64sAVboYGpIyuDBeMIRC3W8dK35v1nDism9xa595Da5VlXKM7hk7pIXg69lodfiftasIkyD_KUGkxBwxvrmz7dBo10-Y5zvro9hD4QKRjOx7DYj9sumnkyYCDx0m4ImDIIkNswfVTWI2V22wlnpHdvMgdtKYgOIIAU28y9gtdrdDkpkH0GHcDyd15sxQGd9VjwhGZA_mpusUKMsEoGgst2rJ3zA.UWfZupqLlGvlATkPo3wdaw.38d55cd0163610d8ce8c42fcff7b62d8981495cc1afacbb2f14e5a23682a4e13",
    "type": "turnstile",
    "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36"
  }
}
```

### Use SDK Request

::: code-group

```python
# pip install --upgrade capsolver
# export CAPSOLVER_API_KEY='...'

import capsolver

# capsolver.api_key = "..."
solution = capsolver.solve({
  "type": "AntiTurnstileTaskProxyLess",
  "websiteURL": "https://www.yourwebsite.com",
  "websiteKey": "0x4XXXXXXXXXXXXXXXXX",
  "metadata": {
	 "action": "login"  # optional
  }
})
```

```go [golang]
package main

import (
  "fmt"
  capsolver_go "github.com/capsolver/capsolver-go"
  "log"
)

func main() {
  // first you need to install sdk
  //go get github.com/capsolver/capsolver-go

  capSolver := capsolver_go.CapSolver{ApiKey: "..."}
  solution, err := capSolver.Solve(map[string]any{
    "type":       "AntiTurnstileTaskProxyLess",
    "websiteURL": "https://www.yourwebsite.com",
    "websiteKey": "0x4XXXXXXXXXXXXXXXXX",
    "metadata": map[string]string{
	  "action": "login"  // optional
    },
  })
  if err != nil {
    log.Fatal(err)
    return
  }
  fmt.Println(solution)
}

```

## Understanding Cloudflare Chanllenge 5S
It uses the same underlying technology as Turnstile. It helps website owners to embed non-intrusive Cloudflare challenges on their websites to effectively prevent bot attacks. Also Cloudflare Challenge 5s introduces a brief 5-second delay before granting access to a website. Its purpose is to deter automated bots by requiring users to wait for a short period.

## Chanlleges types Supported by CapSolver
There is no need to specify subtypes during your call. It is not necessary to provide your own custom `User-Agent` yet,
we will ignore this parameter.

![1713496773366](https://github.com/javapuppteernodejs/Cloudflare-Solver-/assets/167292643/763f2636-decf-47a6-8b24-4611aa7b8b7f)


The task type `type` is as follows

- `AntiCloudflareTask` Proxy required

## How to Solve Cloudflare Challenge 
Firstly, as with Turnstile, we use CapSolver to create the task, (the steps are largely the same)

### Step 1 Create Task

Create the task with the [createTask](../api-createtask.md).

In the process of using challenge, we must input `websiteURL`,`proxy` other parameters are optional.

#### Task Object Structure

| Properties | Type   | Required | Description                                       |
|------------|--------|----------|---------------------------------------------------|
| type       | String | Required | `AntiCloudflareTask`                              |
| websiteURL | String | Required | The address of the target page.                   |
| proxy      | String | Required | Learn [using proxies](../api-how-to-use-proxy.md) |

#### **Example request**

```txt
POST https://api.capsolver.com/createTask
Host: api.capsolver.com
Content-Type: application/json
```

```json lines
{
  "clientKey": "YOUR_API_KEY",
  "task": {
    "type": "AntiCloudflareTask",
    "websiteURL": "https://www.yourwebsite.com",
    "proxy": "158.120.100.23:334:user:pass"
  }
}
```

#### Example Response

```json lines
{
  "errorId": 0,
  "status": "idle",
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"  // record taskId
}

```

### Step 2 **Getting Result**

Use the [getTaskResult](../api-gettaskresult.md) method to get the recognition results

Depending on the system load, you will get the results within the interval of `1s` to `20s`

#### **Example Request**

```txt
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json
```

```json lines
{
  "clientKey": "YOUR_API_KEY",
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"
}
```

#### Example Response

```json lines
{
  "errorId": 0,
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006",
  "status": "ready",
  "solution": {
    "cookies": {
      "cf_clearance": "..."
    },
    "proxy": "...",
    "token": "...",
    "type": "challenge",
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
  }
}
```

### Use SDK Request

::: code-group

```python
# pip install --upgrade capsolver
# export CAPSOLVER_API_KEY='...'

import capsolver

# capsolver.api_key = "..."
solution = capsolver.solve({
    "type": "AntiCloudflareTask",
    "websiteURL": "https://www.yourwebsite.com",
    "proxy": "158.120.100.23:334:user:pass"
})
```

```go [golang]
package main

import (
	"fmt"
	capsolver_go "github.com/capsolver/capsolver-go"
	"log"
)

func main() {
	// first you need to install sdk
	//go get github.com/capsolver/capsolver-go

    capSolver := capsolver_go.CapSolver{ApiKey: "..."}
	solution, err := capSolver.Solve(map[string]any{
		"type":       "AntiCloudflareTask",
		"websiteURL": "https://www.yourwebsite.com",
		"proxy":      "158.120.100.23:334:user:pass"
	})
	if err != nil {
		log.Fatal(err)
		return
	}
	fmt.Println(solution)
}

```
## Conclusion
In 2024, we can leverage CapSolver as the best Cloudflare solution to deal with Cloudflare's Turnstile and Challenge 5s, two security mechanisms.CapSolver is a leading automated CAPTCHA resolution tool with excellent CAPTCHA resolution capabilities. Through its advanced automation technology and robust infrastructure, CapSolver is able to resolve CAPTCHA accurately and efficiently, making it an ideal choice to address Turnstile and other CAPTCHA challenges in 2024 and beyond.

