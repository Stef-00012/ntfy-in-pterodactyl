# Setup
your pterodactyl panel must use the [AIO egg](https://github.com/DanBot-Hosting/pterodactyl-eggs/blob/main/egg-a-i-o.json) *(not tested on any other egg)*

1. Download the `ntfy.zip`
2. Upload it on your pterodactyl panel and unarchive it
3. Setup your config file (see [here](https://github.com/Stef-00012/ntfy-in-pterodactyl/edit/main/README.md#config))
4. Set the startup command to `bash /home/container/setup/start.sh`

to make sure all Ntfy commands work and show correct data, I made a custom shell file (`/home/container/commands/ntfy`), that file sets the auth file and config file on the commands that might use it
the actual Ntfy CLI is `/home/container/commands/ntfycli`

### `start.sh`
What this file does is:
If it's the first run, show some information on how to setup and what ti does, otherwise
1. Add `/home/container/commands` to the $PATH variable
2. Add executale permission to all files in `/home/container/commands`
3. Start the ntfy server as a background process
4. Start a usable shell (`bash`) so you can run any command directly in the pterodactyl console

# Config
The config file is located in `/home/container/data/server.yml`

#### before you start the ntfy server you must change those config:
- `base-url`: The url used to access your ntfy server (this is used for attachments, email sending, iOS push notifications, matrix push gateway)
- `listen-http`: The port where ntfy will listen

#### if you want to use web push notifications you must set those 4 config:
- `web-push-public-key`: Webpush public key (can be obtained by running `ntfy webpush keys`)
- `web-push-private-key`: Webpush private key (can be obtained by running `ntfy webpush keys`)
- `web-push-file`: Where the webpush file is stored, must be inside `/home/container` (defaults to `/home/container/data/webpush.db`)
- `web-push-email-address`: Your email

#### other default config:
- `cache-file`: Where the messages are cached, if unset are only stored in the ram (defaults to `/home/container/data/cache.db`)
- `auth-file`: Where the auth file is stored, it's required to have users (defaults to `/home/container/data/auth.db`)
- `auth-default-access`: Default access to topics for any non-logged user (defaults to `deny-all`, meaning no read and write access to any topic)
- `behind-proxy`: If the ntfy server is behind a proxy (defaults to `false`)
- `attachment-cache-dir`: Where attachments are stored (defaults to `/home/container/data/attachments`)
- `upstream-base-url`: The url of the Firebase/APNS-connected ntfy server, this server will receive only the message ID and the iOS app will fetch the message from your server, it's required for iOS notifications (defaults to `https://ntfy.sh`)
- `log-level`: Ntfy log level (defaults to `info`)

additional Ntfy configs are avaible [here](https://ntfy.sh/docs/config/)

*(that's until someone actually makes a good egg for ntfy with console support to use the cli)*
