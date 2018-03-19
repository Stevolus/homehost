# homehost (in beta)

[![contributions](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/ridhwaans/homehost/issues)
[![release](https://img.shields.io/github/release/ridhwaans/homehost.svg)](https://gitHub.com/ridhwaans/homehost/releases/)
[![tag](https://img.shields.io/github/tag/ridhwaans/homehost.svg)](https://gitHub.com/ridhwaans/homehost/tags/)
[![commits-since](https://img.shields.io/github/commits-since/ridhwaans/homehost/v1.0.0-beta.svg)](https://gitHub.com/ridhwaans/homehost/commit/)
[![license](https://img.shields.io/github/license/ridhwaans/homehost.svg)](https://github.com/ridhwaans/homehost/blob/master/LICENSE)

Self-hosted Netflix-like app in React

![homehost](https://raw.githubusercontent.com/ridhwaans/homehost/master/media/music-page-beta-3.PNG)
![homehost](https://raw.githubusercontent.com/ridhwaans/homehost/master/media/movies-page-beta.PNG)

## 1.0.0-BETA

### What's new

- New react soundplayer controls in album Detail view
- react streaming audio from homehost albums or fallback to preview urls
- new webpack for homehost client works as expected
- added chain processing for movies and music metadata

### Improvements

- Rewrote musicPlayer component and interface to fit homehost
- Removed unused app resources
- various minor fixes
- better naming everywhere
- more readme documentation

### Bugs

- ~~Music playbutton toggle doesnt work correctly~~
- ~~track urls in certain albums are null and crashing~~
- ~~css module loader doesnt change based on Detail View change~~
- view height misaligned for deluxe albums

### v1.0.0 Launch milestones

- ~~Finish Album detail view redesign v1~~
- ~~React Music currently plays cdn previews. add album streaming support from host server~~
- ~~complete music api routes for album and tracks~~
- ~~get music player controls to work in react component~~
- ~~add support for single-disc and compilation albums~~
- ~~cleanup utils & dependencies~~
- improve cover page and navbar

### Backlog  

- music apiClient mixes client options with request header options  
- use helmetjs or privatise admin-specific api routes (/api/generate)  
- use filename instead of filepath when regex processing movie metadata 
- music readStream pipe doesnt allow fastforward like preview urls

## Setup

### Naming conventions

**Movies**  
`movie_file_name<TMDB_movieID>(.mp4|.mkv)`  
**Music**  
`album_folder_name <Spotify_albumID> \ (<disc_number>-)?<track_number> track_file_name(.mp3)`

### Server-side

In `./config.yml`, set the media paths, and specify a working API key for TMDB and Spotify Web API
```yaml
# Server-side configs
movies:
  path  : '/path/to/directory'
  api   : 'api.themoviedb.org/3'
  key   : '<api_key>'
music:
  path  : '/path/to/directory'
  api   : 'api.spotify.com/v1'
  key   : '<auth_token>'
```

Start homehost by running `yarn dev` from the base directory. Server should open at `http://localhost:5000/`  
Server requires `<media>.json` file data at startup. Initial json state should be empty
```json
./movies.json
{
  "movies": []
}
./music.json
{
  "music": []
}
```
On the server, call `/api/generate` **once**. Wait for the async operation to finish and save  
**NOTE:** `nodemon` interrupts data generation in async after filesave. Use `node server` instead for generating metadata  
By default, `5000` is the nodejs server port, `3000` is the react client port

## Routes

### Server-side

**GET** `/api/hello` 
**GET** `/api/generate` 
**GET** `/api/movies`  
**GET** `/api/movies/<id>`  
**GET** `/movies/<id>`  
**GET** `/api/music/`  
**GET** `/api/music/albums/<id>`  
**GET** `/music/albums/:album_id/tracks/:track_id`

### Client-side

`/Movies` and `/Music` are scheduled for v1.0 release. `/Books`, `/Comics`, `/Podcasts`, `/TV` are TODO

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Powered by
<p><img src="/media/spotify_green.svg"  width="200" height="150">&emsp;<img src="/media/tmdb_green.svg"  width="150" height="150"></p>

