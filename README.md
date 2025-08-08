# Huami-token

[![status-badge](https://ci.codeberg.org/api/badges/argrento/huami-token/status.svg)](https://ci.codeberg.org/argrento/huami-token)

Script to obtain watch or band bluetooth access token from Huami servers.
It will also download AGPS data packs `cep_alm_pak.zip` and `cep_7days.zip`.

## About

To use new versions of Amazfit watches and bands with Gadgetbridge you need special unique key.
Read more here: https://codeberg.org/Freeyourgadget/Gadgetbridge/wiki/Huami-Server-Pairing.

## Community

If you would like to get in touch 
* Matrix: [`#huami-token:matrix.org`](https://matrix.to/#/#huami-token:matrix.org)

## Preparation

1. Ensure that you login in Amazfit App with Amazfit account --
because only this login methods are supported. If not, create new Amazfit account
with e-mail and password.
2. Pair, sync and update your watch with Amazfit App. Your pairing key will be stored on
Huami servers.
3. `pip3 install huami_token`
4. Use like this: `python3 -m huami_token ...`

## Usage
```
usage: huami_token.py [-h] [-e EMAIL] [-p PASSWORD] [-b]
                      [-g] [-a] [-n]

Obtain Bluetooth Auth key from Amazfit servers and download AGPS data.

optional arguments:
  -h, --help            show this help message and exit
  -e EMAIL, --email EMAIL
                        Account e-mail address
  -p PASSWORD, --password PASSWORD
                        Account Password
  -b, --bt_keys         Get bluetooth tokens of paired devices
  -g, --gps             Download A-GPS files
  -f, --firmware        Request firmware updates. Works only with -b/--bt_keys
                        argument. Extremely dangerous
  -a, --all             Do everything: get bluetooth tokens, download A-GPS
                        files. But do NOT download firmware updates
  -n, --no_logout       Do not logout, keep active session and display app
                        token and access token
```


## Logging in with Amazfit account
Run script with your credentials: `python3 huami_token.py --email youemail@example.com --password your_password --bt_keys`.

Sample output:
```bash
> python3 huami_token.py --email my_email --password password --bt_keys
Getting access token with amazfit login method...
Token: ['UaFHW53RJVYwqXaa7ncPQ']
Logging in...
Logged in! User id: 1234567890
Getting linked wearables...

╓───Device 0
║  MAC: AB:CD:EF:12:34:56, active: Yes
║  Key: 0xa3c10e34e5c14637eea6b9efc06106
╙────────────

Logged out.
```

Here the `auth_key` is the unique pairing key for your watch. The `ACT` tab shows whether a device is
active or not.


## Experimental: updates download

This is extremely dangerous: flashing the wrong version can brick your device!
I am not responsible for any of problems that might arise.

Can be enabled with `-f/--firmware` argument. Will work only with `-b/--bt_keys` argument.
You should input the ID of a device, or `-1` to check for all.
Script will try to find updates for the firmware and the font pack for the device from 
the table above.

Use the downloaded files at your own risk!

## Dependencies

* Python 3.7.7
* argparse
* requests
* urllib
* random
* uuid
* json
* shutil

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
