To create key:-
command:- openssl genrsa -out mykey.key 2048

To create certificate:-
Command:- openssl req -new -x509 -key mykey.key -out mycert.crt -days 365 -s
ubj /CN=oleoleapp.in
 
To create tls secret:-
Command:- kubectl create secret tls mytls-secret --cert=mycert.crt --key=mykey.key
