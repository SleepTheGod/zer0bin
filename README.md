<div align="center">
    <img src="zero.png" height="110px"/>
	<br>
    <img src="zer0bin.svg" height="100"/>
	<br>
    Just a place to paste
    <br>
	<br>
    <p align="center">
	<a href="https://github.com/domterion/zer0bin/stargazers">
		<img alt="Stargazers" src="https://custom-icon-badges.herokuapp.com/github/stars/domterion/zer0bin?style=for-the-badge&logo=star&color=f6c177&logoColor=31748f&labelColor=12101F"></a>
<!-- 	<a href="https://github.com/domterion/zer0bin/releases/latest">
		<img alt="Releases" src="https://img.shields.io/github/release/domterion/zer0bin?style=for-the-badge&logo=github&color=31748f&logoColor=ebbcba&labelColor=12101F"/></a> -->
	<a href="https://github.com/domterion/zer0bin/issues">
		<img alt="Issues" src="https://custom-icon-badges.herokuapp.com/github/issues/domterion/zer0bin?style=for-the-badge&logo=issue-opened&color=9ccfd8&logoColor=eb6f92&labelColor=12101F"></a>
	<a href="https://github.com/Domterion/zer0bin/blob/main/LICENSE">
		<img alt="License" src="https://custom-icon-badges.herokuapp.com/github/license/domterion/zer0bin?style=for-the-badge&logo=law&color=c4a7e7&logoColor=ebbcba&labelColor=12101F"></a>
</p>
    <br>
</div>

# API

**GET** /p/:id - Get a paste by ID

**POST** /p/n - Post a new paste

**GET** /s - Get stats about the zer0bin instance

# Public instances

Submit your public instance [here](https://github.com/Domterion/zer0bin/issues/new?assignees=&labels=&template=03_public_instance.md&title=%F0%9F%9A%80+)!

| Website                                        | Country | Expiration | Max paste size | Version      |
| ---------------------------------------------- | ------- | ---------- | -------------- | ------------ |
| zer0b.in (not up yet)                          | ?       | 7 days     | 40,000 chars   | vx.x.x       |
| [stepbro.voring.me](https://stepbro.voring.me) | 🇺🇸      | 365 days   | 100,000 chars  | v0.1.0       |

# Instructions

### Requirements

- Rust >= 1.58.0
- Postgresql >= 12.0
- Nginx >= 1.18.0
- NodeJS + Yarn (`sudo npm i -g yarn`)
- \*nix OS

### Steps

1. `git clone https://github.com/Domterion/zer0bin && cd zer0bin`
2. `cp config.example.json config.json` and edit as appropriate
3. `cp example.nginx /etc/nginx/sites-avaliable/yoursite.tld`, edit as appropriate, `sudo cp /etc/nginx/sites-avaliable/yoursite.tld /etc/nginx/sites-enabled/yoursite.tld && systemctl nginx restart`
4. `psql -d postgres`
5. `CREATE DATABSE zer0bin;` and `\c zer0bin`
6. Paste contents of `schema.sql`
7. `\q`
8. `cd ../frontend`
9. `yarn && yarn run build`
10. `cd backend`
11. `cargo build --release`
14. `./target/release/backend` (preferably in a tmux session)

### Configuration

| Key                                        | Values                    | Description                                                                    |
| ------------------------------------------ | ------------------------- | ------------------------------------------------------------------------------ |
| server.backend_host                        | 127.0.0.1 or 0.0.0.0      | The host to run the backend on                                                 |
| server.backend_port                        | Any open port             | The port to run the backend on                                                 |
| pastes.character_limit                     | Number up to 2^64 - 1     | The amount of characters allowed in a single paste                             |
| pastes.days_til_expiration                 | Number up to 2^63 or -1   | The days till a paste is to expire. If set to -1 then pastes will never expire |
| pastes.id_length                           | Number up to 2^64 - 1     | The length of the ID for each paste                                            |
| databases.postgres_uri                     | PostreSQL Connection URI  | The URI to use when connecting to a PostgreSQL database                        |
| ratelimits.seconds_in_between_pastes       | Number up to 2^64 - 1     | The seconds between paste uploads                                              |
| ratelimits.allowed_pastes_before_ratelimit | Number up to 2^32 - 1     | Amount of requests that can be made before they are blocked and have to wait   |
| frontend.api_url                           | Your public facing API URL| The URL that the frontend will post to, most likely `https://domain.tld/api`   |
