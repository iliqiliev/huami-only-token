# huami-only-token
Forked from huami-token by `argrento`. Click button bellow to visit his repo.

<a href="https://codeberg.org/argrento/huami-token/">
    <img alt="Get it on Codeberg" src="https://get-it-on.codeberg.org/get-it-on-white-on-black.png" height="60">
</a>

## About

To use new versions of Amazfit watches and bands with Gadgetbridge you need special unique key.

Read more here: [gadgetbridge.org/basics/pairing/huami-xiaomi-server](https://gadgetbridge.org/basics/pairing/huami-xiaomi-server/)

## Preparation

1. Ensure that you login in Amazfit App with Amazfit account.
If not, create new Amazfit account with e-mail and password.
2. Pair, sync and update your watch with Amazfit App. Your pairing key will be stored on Huami servers.
3. Clone this repo.
4. Create a python virtual environment inside.
5. Install dependencies from `requirements.txt`.
6. Use like this: `python huami_token.py --email {YOUR EMAIL HERE} -- password {YOUR PASSWORD HERE} --all`

## Usage
```
usage: huami_token.py [-h] [-e EMAIL] [-p PASSWORD]
                      [-b] [-g] [-a] [-n]

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
Run script with your credentials: `python huami_token.py --email {YOUR EMAIL HERE} -- password {YOUR PASSWORD HERE} --bt_keys`.

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
This has been tested to work with Python 3.13.

* requests
* types-requests
