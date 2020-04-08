# brij
A client api for brij fintech

## installation
```pip install brij-fintech```

## getting started
in order to use brij services,you'll need to follow these simple steps
- create an account with them
- create a service/application under your brij account dashboard
- note down your app ID and appKey

## Integration

load the API 
``` 
from brij.loader import BrijLoader
fintech = BrijLoader(app_id=os.environ.get('BRIJ_APP_ID'), app_key=os.environ.get('BRIJ_APP_KEY'))
```

***Direct Payment:***
sending direct payment from your customer to your brij account using M-Pesa
```
mpesa_service = fintech.get_mpesa_services()
response = mpesa_service.mpesa_to_acc(amount, sender, MPESA-NUMBER, description='short description')
if r:
    print(r.json())
else:
    print('error')
```
- the description text must not exceed 16 chars
- MPESA-NUMBER is the number making the transaction. the supported format starts is 254712345678
- 
***Escrow:***
sending escrow payment between your customers with your account acting as an escrow account, using M-pesa
```
service = fintech.get_mpesa_services()
r = service.mpesa_to_escrow(amount, 'sender email or phone', 'recepient email or phone', MPESA-NUMBER, 'short deacription')
print(r.json())
```
- the MPESA-NUMBER is the number making the transaction. the supported format is 254712345678
- short description must not exceed 16 chars
- sender email or phone are required in order to reach both parties with updates on the transaction

