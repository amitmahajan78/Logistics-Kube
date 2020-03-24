Auth Token

curl -X POST \
 http://ab0eeff656de311eaab5802c43b171f6-1286383641.eu-west-2.elb.amazonaws.com:8090/oauth/token \
 -H 'Authorization: Basic c2VydmVyLXNlcnZlcjpzZXJ2ZXItc2VydmVy' \
 -H 'Cache-Control: no-cache' \
 -H 'Content-Type: application/x-www-form-urlencoded' \
 -d grant_type=client_credentials

Add Stock

curl -X POST \
 http://ab98382946de811eaa80e0aaa98f7126-1496903415.eu-west-2.elb.amazonaws.com:9004/v2/stock \
 -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsicmVzb3VyY2VfaWQiXSwic2NvcGUiOlsicmVhZCIsIndyaXRlIiwidHJ1c3QiXSwiZXhwIjoxNTg1MDcwODYzLCJqdGkiOiJjYzkxNWMxZS01ODE4LTQzMTctYTljMS05Y2FmOGQzYWJmYmUiLCJjbGllbnRfaWQiOiJzZXJ2ZXItc2VydmVyIn0.AuEDpt_g8SbnZX-IeDtCaKw3seKNz089Ca1AsFHcqEBta6j0eoQ6-225xgZeqEAMjBGcNsK3_ZpTKncqVo8amBbWi5wNcsgDXrajBtOe7aonZtRTTfYnTHl87Xgf_WaZNfurmsnQybt6P5jPvQg01m_9po9ROX-jp0n7J84f9JcCuUFzh0gNop4yKfusLGOP_T0imciPnL9hGuD7UEEyRnQ6mdU886blXuD94x-aUjYVxaZlUBh4goVxD6P3I7ag8xN2S-WAmblkVoY-sd4qVD1WA6qmY1o9ETZs_mjM0Tuuk6OFO8WTiv1KHXublfcqjS-7ZWF5aEbm6jiLEx9d7g' \
 -H 'Cache-Control: no-cache' \
 -H 'Content-Type: application/json' \
 -d '{
"sku" : "1234567890",
"quantity" : 1,
"supplier" : "Xcom Ltd",
"category" : "Household",
"productName" : "Washing Powder",
"price" : 7
}'

Post Order

curl -X POST \
 http://ac8b0759f6de711eaab5802c43b171f6-1784157831.eu-west-2.elb.amazonaws.com:9001/v2/orders \
 -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsicmVzb3VyY2VfaWQiXSwic2NvcGUiOlsicmVhZCIsIndyaXRlIiwidHJ1c3QiXSwiZXhwIjoxNTg1MDcwODYzLCJqdGkiOiJjYzkxNWMxZS01ODE4LTQzMTctYTljMS05Y2FmOGQzYWJmYmUiLCJjbGllbnRfaWQiOiJzZXJ2ZXItc2VydmVyIn0.AuEDpt_g8SbnZX-IeDtCaKw3seKNz089Ca1AsFHcqEBta6j0eoQ6-225xgZeqEAMjBGcNsK3_ZpTKncqVo8amBbWi5wNcsgDXrajBtOe7aonZtRTTfYnTHl87Xgf_WaZNfurmsnQybt6P5jPvQg01m_9po9ROX-jp0n7J84f9JcCuUFzh0gNop4yKfusLGOP_T0imciPnL9hGuD7UEEyRnQ6mdU886blXuD94x-aUjYVxaZlUBh4goVxD6P3I7ag8xN2S-WAmblkVoY-sd4qVD1WA6qmY1o9ETZs_mjM0Tuuk6OFO8WTiv1KHXublfcqjS-7ZWF5aEbm6jiLEx9d7g' \
 -H 'Cache-Control: no-cache' \
 -H 'Content-Type: application/json' \
 -d '{
"shipFrom" : "SWINDON",
"shipTo": "Reading",
"booking" : {
"vehicleNumber" : "ABC123",
"appointment" : "2021-03-26T18:25:43.511Z"
},
"orderDetailList" : [
{
"sku" : "1234567890",
"quantity" : 1
}
]
}'

Get Order

curl -X GET \
 http://a21d550706de811eaab5802c43b171f6-1295667565.eu-west-2.elb.amazonaws.com:9003/v2/orders/XXXX \
 -H 'Authorization: Bearer XXXX' \
 -H 'Cache-Control: no-cache' \
 -H 'Content-Type: application/json'

Received Shipment

curl -X POST \
 http://ab0eeff656de311eaab5802c43b171f6-1286383641.eu-west-2.elb.amazonaws.com:9002/v2/shipment/registerArrival/SHIPMENT_ID \
 -H 'Authorization: Bearer ' \
 -H 'Cache-Control: no-cache' \
 -H 'Content-Type: application/json'
