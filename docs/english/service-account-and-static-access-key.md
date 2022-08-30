# Create a service account in Yandex.Cloud

1. Log in to your personal account 
   https://console.cloud.yandex.ru/cloud

2. Choose the desired folder in the list.

3. In the menu on the center, click `Service accounts`.

4. Click on the top right corner `Create service account`.

5. Come up with a name for the account, you won't need it. Add Roles: `iam.serviceAccounts.user`, `editor`. Save.

6. Click on a service account to open it.

7. Click on the top right corner `Create new key` -> `Create static access key`.

8. Come up with a description. Create it.

9. You have a window with 2 fields. Copy this values somewhere, because the value of `secret key` field is issued one time and you won't see `secret key` again in Yandex.Cloud.

Congratulation! Now you have 
- `ID` that is our `accessKeyId` 
- `Secret key` that is our `secretAccessKey`