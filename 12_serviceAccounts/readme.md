two types f accunt in kubernetes
1) user account
2) serice account

kubectl create serviceaccount <sa name>


tokens are stored in secret


with 1.22 we arte getting bound service Account Tokens

- Audience Bound
- Time Bound
- Object Bound


with version 1.24 when we create a service account tokens are not generated anymore, we need to create token using command
kubectl create token <serviceaccount>

this token will have expiry date