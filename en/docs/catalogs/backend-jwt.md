# BackendJWT Custom Resource

 This is the CR which is used to describe the backend JWT generation and it's configurations

```
apiVersion: dp.wso2.com/v1alpha1
kind: BackendJWT
metadata:
  name: backendjwt
spec:
  enabled: true
  encoding: "base64"
  signingAlgorithm: "SHA256withRSA"
  header: "X-JWT-Assertion"
  tokenTTL: 3600
  customClaims:
    - claim: "admin"
      value: "http://wso2.org/claims/enduser"
    - claim: "test"
      value: "1"
      type: float
```

Refer [Learn to attach API Policies for Backend JWT Token Manipulation](../create-api/create-and-attach-api-policies/backend-jwt-token-manipulation/backend-jwt-token-manipulation-via-crs.md) for more information on how to configure backend JWT in APK.