
# TEXIS VOICE API DOCUMENTATION 

We make all your call service needs accessible. No Bans, Quick API Integration. 


## Deployment

This documentation focused mainly on python as a framework using our endpoint, we as well support other framework using the same technique and implementation

```pip
  pip install requests
```


## Features
- View all the Voice supported https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=tts
- Call: To dial an Endpoint to an 164 number format 
- Transfer: an existing call to another endpoint or number of choice, mainly for group call or end to end call
- Hangup: Hangup an existing call
- Hold: Play hold music on a live call 
- Unhold: unhold / stop hold music from playing in the live call background
- Gather: gather input on a Transfer call
- Gather_TTS: this enable you to play voice text to an outgoing call and gather input key follows by the voice [Mainly for IVR]
- TTS: Play voice text to an outgoing call with no gather input, suitable for IVR and performs equally the same function as Gather_TTS but gather not allowed on this
- balance: this enable you to check your api balance


## API Reference

#### Create an outgoing call

```http
  POST /v1/call
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `to` | `string` | **Required**. Number you are calling E.G [17205490435] |
| `from` | `string` | **Required**. Your Caller ID E.G [14563805355] |
| `callback` | `string` | **Required**. http://yourserver.com/callback |


#### Transfer to an existing call

```http
  POST /vi/transfer
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `to` | `string` | **Required**. Number you are calling E.G [17205490435] |
| `from` | `string` | **Required**. Your Caller ID E.G [14563805355] |
| `uuid` | `string` | **Required**. Your call uuid you intend transfering the call to |


#### Hanging up an existing Call

```http
  POST /vi/hangup
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |


#### Play Hold Music on Existing Call
```http
  POST /vi/hold
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |



#### Stop Hold Music 
```http
  POST /vi/unhold
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |

#### To gather DTMF Input On a transferred Call.
```http
  POST /vi/gather 
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |
| `length` | `Number` | **Required**. Digit length |


#### To gather DTMF Input and Play voice tts text on Call.
```http
  POST /vi/gather_tts 
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |
| `voice` | `string` | **Required**. Voice Name E.g [en-AU-NatashaNeural] |
| `text` | `string` | **Required**. Your Text E.g Hi, we are texis voice Api company |
| `length` | `Number` | **Required**. Digit length |



#### Play voice tts text on Call.
```http
  POST /vi/tts 
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |
| `voice` | `string` | **Required**. Voice Name E.g [en-AU-NatashaNeural] |
| `text` | `string` | **Required**. Your Text E.g Hi, we are texis voice Api company |


#### Check your API Balance.
```http
  POST /vi/balance 
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |



Takes two numbers and returns the sum.


## Documentation

[Documentation](https://linktodocumentation)
- EACH CALL YOU MAKE HAS A UUID ASSIGNED TO IT
- HOW TO MAKE A SIMPLE CALL AND PLAY A VOICE TEXT AND HANGUP THE CALL {USING PYTHON}
- WE WILL BE MAKING USE OF V1/CALL AND /V1/TTS endpoint
import requests

url = 'texisserver/v1/call'

headers = {

    'Content-Type': 'application/json',
}



data = {

    "to": "17857680433",
    "from": "18002655158",
    "apikey": "yourapik_key_given_by_texis",
    "callback": "http://yourserver.com/callback",

}

response = requests.post(url, headers=headers, json=data)


print(response.text)

OUTPUT 👇
#### {"uuid":"54e6f924-b744-4597-ae03-f726da1b9b0d","status":"success"}

- This is a simple demonstration of making an outgoing call using the v1/call endpoint and grabbing the uuid of the voice for our next sequence action to play a text audio on the call,
- now copy the uuid of the call for the next steps in order to play an audio text using the v1/tts endpoint 

import requests

url = 'texisserver/v1/tts'

token = "Bearer {token}"

headers = {

    'Content-Type': 'application/json',

}

data = {

    "apikey":"yourapik_key_given_by_texis",
    "voice": "en-ZA-LukeNeural",
    "uuid": "54e6f924-b744-4597-ae03-f726da1b9b0d",
    "text": "Hello Everyone, we are calling to annouce our voiceapi endpoint implementation, so this is a test from us at Texis Voice Api company limited",

}

response = requests.post(url, headers=headers, json=data)
print(response.text)

- ##Now we have successfully play speech to text audio on our existing call using the previous uuid we grabbbed from the outgoing we made.
- ##Make sure the call get answered before lauching using the tts endpoint to play a text to speech audio on the call


### NOW TO THE LAST STATE OF HANGING THE CALL PROGRAMMATICALLY USING THE SAME CALL UUID

import requests


url = 'http://texiserver/v1/hangup'


headers = {

    'Content-Type': 'application/json',

}


data = {

    "apikey":"yourapik_key_given_by_texis",
    "uuid": "54e6f924-b744-4597-ae03-f726da1b9b0d",

}

response = requests.post(url, headers=headers, json=data)

print(response.text)

## API Event and Response
## Event And CallBack
- success: Call Initiated
- ringing: Call is ringing 
- answered: Call has been answered
- bridging: connected two call way, call transfer 
- bridged: call was connected successfully 
- busy: 
- dtmf.received: received digit 
- dtmf.completed: the later has been completed with lenght == user_length
- digits: digits completed after dtmf.completed Event
- digit: digit received after dtmf.received 


## Authors

- [@greyxec](https://t.me/greyxec)
- TO BUY API KEY FOR OUR ENDPOINT VOICE CALL CONTACT  [@greyxec](https://t.me/greyxec)

