
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
- country_prefix: this prefix is what differentiate the region you are calling e.g usa, uk, australia, spain, france, india, italy.
- Record Url: this url contains two way mixed audio record file recorded during call session


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
  POST /v1/transfer
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `to` | `string` | **Required**. Number you are calling E.G [17205490435] |
| `from` | `string` | **Required**. Your Caller ID E.G [14563805355] |
| `uuid` | `string` | **Required**. Your call uuid you intend transfering the call to |


#### Hanging up an existing Call

```http
  POST /v1/hangup
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |


#### Play Hold Music on Existing Call
```http
  POST /v1/hold
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |



#### Stop Hold Music 
```http
  POST /v1/unhold
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |

#### To gather DTMF Input On a transferred Call.
```http
  POST /v1/gather 
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |
| `length` | `Number` | **Required**. Digit length |


#### To gather DTMF Input and Play voice tts text on Call.
```http
  POST /v1/gather_tts 
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
  POST /v1/tts 
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |
| `uuid` | `string` | **Required**. Your Call UUID |
| `voice` | `string` | **Required**. Voice Name E.g [en-AU-NatashaNeural] |
| `text` | `string` | **Required**. Your Text E.g Hi, we are texis voice Api company |


#### Check your API Balance.
```http
  POST /v1/balance 
```
| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `apikey` | `string` | **Required**. Your API key |




#### ALL COUNTRY PREFIX.
```http
  Mandatory prefix to make an outgoing to call any of your prefered destination
```
| Country | Prefix    | Description                |
| :-------- | :------- | :------------------------- |
| `UNITED STATE - US` | `77, 76, 88, 75, 59, 104, 50, 80` | **Required** Calling USA |
| `UNITED KINGDOM - UK` | `004, 075, 020, 04471` | **Required** Calling UK |
| `INDIA - IN` | `024, 048, 015, 028, 042, 0910` | **Required** Calling IN |
| `FRANCE - FR` | `005, 006, 014, 017, 018` | **Required** Calling FR |
| `AUSTRALIA - AU` | `002, 008, 06140, 020, 025, 067` | **Required** Calling AU|
| `ITALY - IT` | `000, 005, 009, 010` | **Required** Calling IT |
| `SPAIN - SP` | `031` | **Required** Calling IN |





## Documentation

[Documentation](https://linktodocumentation)
- EACH CALL YOU MAKE HAS A UUID ASSIGNED TO IT
- HOW TO MAKE A SIMPLE CALL USING YOUR PREFERED REGION PREFIX AND PLAY A VOICE TEXT AND HANGUP THE CALL {USING PYTHON}
- WE WILL BE MAKING USE OF V1/CALL AND /V1/TTS endpoint

Since we will be making a test call on our usa phone number, so we use any of the usa prefix mentioned above.

Note: incase a choosen prefix is not calling out, you can categorically choose among other prefixes under the same regions e.g prefix 77 not calling on usa, you can switch to prefix 76 and the likes.

WE ARE MAKING USE OF PREFIX 77 USA FOR OUR CODE SAMPLE!!!!!!

import requests

url = 'texisserver/v1/call'

headers = {

    'Content-Type': 'application/json',
}



data = {

    "to": "771xxxxxxxxxx",
    "from": "1xxxxxxxxxx",
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


## FETCH AUDIO RECORD , SAVE TO TEXIS SERVER AND FORWARD TO YOUR LOCAL HOST / BOT

**Record url Link Path:** http://IP:3001/v1/rec

**Data Parameter Needed to save recname generated by your call sessions:** 

```python
 "apikey": API_KEY,
 "recname": f'{recname}',

```


**FULL SAMPLE CODE TO SAVE RECNAME:**
```python
 def action_Save_Audio(recname):
    url = 'http://IP:3001/v1/rec'
    headers = {

        'Content-Type': 'application/json',
    }
    data = {

        "apikey": API_KEY,
        "recname": f'{recname}',

    }
    response = requests.post(url, headers=headers, json=data)
    record_url = response.json()['url']
    return record_url


```
**FETCH AND FORWARD THE SAVED AUDIO FILE TO YOUR LOCAL HOST :**
```python
def action_Fecth_Audio_To_My_Local_Host(url, recname):
    doc = requests.get(url, stream = True)
    f = open(f"recs/{recname}.wav", "wb")
    see = f.write(doc.content)
    print(see)
    f.close()


```

### NOW YOU CAN FINALLY SEND YOUR PRESAVED AUDIO FILE ON YOUR LOCAL HOST TO YOUR TELEGRAM BOT / FINAL DESTINATION

#### IN THIS STANCE WE ARE FORWARDING THE AUDIO FILE TO OUR BOT AND IN THAT CASE SCENERIO WE WILL BE USING TELEGRAM <bot.send.audio> method/functions

#### SAMPLES CODE

```python
            bot.send_audio(chat_id=userid, audio=open(f"recs/{recording_url}.wav", 'rb'))
```

### FULL CODE SAMPLE COMBINING ALL STEPS 

```python
recording_url = request.json['recname']

url = class_action_Save_Audio(recording_url)   

class_action_Fecth_Audio_To_My_Local_Host(url, recording_url)

bot.send_audio(chat_id=userid, audio=open(f"recs/{recording_url}.wav", 'rb'))

```


## API Event and Response
## Event And CallBack
- success: Call Initiated
- ringing: Call is ringing 
- answered: Call has been 
- voicemail: voicemail detected hence hangup is trigger
- Human: human detected 
- unknown: neither human nor voicemail, can't determine
- bridging: connected two call way, call transfer 
- bridged: call was connected successfully 
- recname: audio record file name 
- busy: not picking or busy mode
- dtmf.received: received digit 
- dtmf.completed: the later has been completed with lenght == user_length
- digits: digits completed after dtmf.completed Event
- digit: digit received after dtmf.received 


## Authors

- [@greyxec](https://t.me/greyxec)
- TO BUY API KEY FOR OUR ENDPOINT VOICE CALL CONTACT  [@greyxec](https://t.me/greyxec)

