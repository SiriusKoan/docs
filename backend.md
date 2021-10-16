# backend
by siriuskoan

## Setup
`config.py` is the main configuration file, which contains `admin_username`, `admin_password`, `host_ip_address`.  
Admin can turn on ssh tunnel server with a specified port. Once it is turned on, a password is generated. Admin has to give the password to users to allow them to login.  

## Routes
`/admin/login`
 - Allow admin to login with the password set in `config.py`.

`/dashboard`  
 - Turn on/off ssh tunnel service.
 - View all connections, including their user token, uptime and so on.

`/admin/plugins`
 - Show all plugins in `plugins/` directory.

`/admin/plugins/add`
 - Add new plugin by submitting GitHub repo URL.


## Database
`users`  
 - `id`
 - `ssh_key`: Hashed ssh key
 - `token`: User authentication
 - `status`: `active` or `inactive`
